---
title: Evolutionary Graph Theory and Community Detection in Networks
description: Notes on collaborative work in evolutionary graph analytics and geo-spatial community detection.
pubDate: 2014-01-11T00:00:00Z
tags:
  - evolutionary-game-theory
  - networks
  - graph-theory
  - data-mining
---

Over the past two years or so, I’ve been exploring various problems related to evolutionary graph theory and network science with my colleague Paulo Shakarian (now at ASU). I’m grateful for having had the opportunity to do this work with such a brilliant and hard-working colleague as Paulo and wanted to highlight some of that work here.

## Evolutionary Graph Analytics

In this work we studied diffusion in graphs or networks, inspired by the framework outlined by Martin Nowak in his book *Evolutionary Dynamics*. This framework of evolutionary graph theory is elegant and broadly applicable, whether to study diffusion in biological networks or to understand how the structure of human or technological social networks influences the spread and dynamics of cultural and social information and behavior. The basic idea is that, given a graph or network of nodes and edges connecting the nodes, “mutant” nodes compete against “resident” nodes via their connections, which allow for the opportunity for nodes to “infect” or spread their type to other nodes.

Relatedly, we developed new analytical methods to quickly compute fixation probabilities, which is the probability that a mutant node takes over the entire population of a given graph or network. We also provided a rather comprehensive review of evolutionary graph theory and its applications within game theory. Here are the relevant publications:

- P. Shakarian, P. Roos, G. Moores. [A Novel Analytical Method for Evolutionary Graph Theory Problems](https://www.sciencedirect.com/science/article/abs/pii/S030326471300021X). *Biosystems*, Elsevier, Vol. 111, No. 2, Feb. 2013.
- P. Shakarian and P. Roos. [Fast and Deterministic Computation of Fixation Probability in Evolutionary Graphs](https://www.researchgate.net/publication/230898142_Fast_and_Deterministic_Computation_of_Fixation_Probability_in_Evolutionary_Graphs). In Sixth IASTED International Conference on Computational Intelligence and Bioinformatics. Pittsburgh, PA. Nov. 2011.
- P. Shakarian, P. Roos, and A. Johnson. [A Review of Evolutionary Graph Theory With Applications to Game Theory](https://www.sciencedirect.com/science/article/abs/pii/S0303264711001675). *Biosystems*, Elsevier, Vol. 107, No. 2, Feb. 2012.

## Community Detection in Geo-Spatial Networks

Unrelated to evolutionary graph theory, we also studied the discovery of communities in networks. Specifically, we developed data mining algorithms that can be used to find communities within networks while considering geo-spatial characteristics in addition to the network connection structure. For instance, given a network of electronic communications, one might be interested in identifying communities that are geo-spatially distant, to identify higher-level organizational structures. The following papers outline the approach:

- J. Hannigan, G. Hernandez, R. M. Medina, P. Roos, P. Shakarian. [Mining for Spatially-Near Communities in Geo-Located Social Networks](https://arxiv.org/abs/1309.2900). AAAI Fall Symposium. Nov. 2013.
- P. Shakarian, P. Roos, D. Callahan, C. Kirk. [Mining for Geographically Disperse Communities in Social Networks by Leveraging Distance Modularity](https://arxiv.org/abs/1305.3668). 19th ACM SIGKDD Conference on Knowledge Discovery and Data Mining (KDD 2013). Chicago, Aug. 2013.
