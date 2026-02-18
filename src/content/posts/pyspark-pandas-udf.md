---
title: Using PySpark and Pandas UDFs to Train Scikit-Learn Models Distributedly
description: A practical pattern for distributed model training by group in Spark.
pubDate: 2019-02-25T20:09:00Z
tags:
  - python
  - pyspark
  - machine-learning
  - pandas
---

Say you find yourself in the peculiar situation where you need to train a whole bunch of scikit-learn models over different groups from a large amount of data. And say you want to leverage Spark to distribute the process to do it all in a scalable fashion.

Recently I ran into such a use case and found that by using pandas_udf – a PySpark user defined function (UDF) made available through PyArrow – this can be done in a pretty straight-forward fashion. Pandas UDFs allow you to write a UDF that is just like a regular Spark UDF that operates over some grouped or windowed data, except it takes in data as a pandas DataFrame and returns back a pandas DataFrame. We just need to define the schema for the pandas DataFrame returned.

Let’s define this return schema. Assume we have some group_id that we can use to group our data into those portions that will be used to train each model. We’ll return a model with that group_id and since it might good info to have later let’s also return the number of instances within that group that the model was trained with, call it num_instances_trained_with. To store all the trained models we will use the python pickle library to dump the model to a string which we can later load back, call it model_str.

```python
from pyspark.sql.types import *

# define schema for what the pandas udf will return
schema = StructType([
StructField('group_id', IntegerType()),
StructField('num_instances_trained_with', IntegerType()),
StructField('model_str', StringType())
])
```

To define a pandas UDF that will train a scikit-learn model, we need to use the pandas_udf decorator, and since we will take in a pandas DataFrame and return the same we need to define the function as a PandasUDFType.GROUPED_MAP (as opposed to PandasUDFType.SCALAR which would take just a pandas Series). Within the UDF we can then train a scikit-learn model using the data coming in as a pandas DataFrame, just like we would in a regular python application:

```python
import pickle
import pandas as pd
from sklearn.ensemble import RandomForestRegressor
from pyspark.sql.functions import pandas_udf
from pyspark.sql.functions import PandasUDFType

@pandas_udf(schema, functionType=PandasUDFType.GROUPED_MAP)
def train_model(df_pandas):
    '''
    Trains a RandomForestRegressor model on training instances
    in df_pandas.

    Assumes: df_pandas has the columns:
                 ['my_feature_1', 'my_feature_2', 'my_label']

    Returns: a single row pandas DataFrame with columns:
               ['group_id', 'num_instances_trained_with',
                'model_str']
    '''

    # get the value of this group id
    group_id = df_pandas['group_id'].iloc[0]

    # get the number of training instances for this group
    num_instances = df_pandas.shape[0]

    # get features and label for all training instances in this group
    feature_columns = ['my_feature_1', 'my_feature_2']
    label = 'my_label';
    X = df_pandas[feature_columns]
    Y = df_pandas[label]

    # train this model
    model = RandomForestRegressor()
    model.fit(X,Y)

    # get a string representation of our trained model to store
    model_str = pickle.dumps(model)

    # build the DataFrame to return
    df_to_return = pd.DataFrame([group_id, num_instances, model_str],
    columns = ['group_id', 'num_instances_trained_with', 'model_str'])

    return df_to_return
```

Now, assuming we have a PySpark DataFrame (df) with our features and labels and a group_id, we can apply this pandas UDF to all groups of our data and get back a PySpark DataFrame with a model trained (stored as a pickle dumped string) on the data for each group:

```python
df_trained_models = df.groupBy('group_id').apply(train_model)
```

Note that the models will each be trained on a single Spark executor so some caution may be necessary to not blow up the executor memory if the data within each group is too large for a single executor to hold and do the model training in memory.
