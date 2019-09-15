---
title : "Discovering SHACL Constraints in RDF Data"
enddate : 2019-05-09T23:00:00+0530
date : 2019-02-09T23:00:00+0530
author : in-arena
desc : Semi-autonomous algorithm for discovering Integrity constraints on RDF datasets for the purpose of data cleaning. Wrote optimizations and extensions for the algorithm, and experimented the system. 
keyword : data-cleaning, rdf, integrity-constraints 
layout : projectTemplate
---

*This was done as part of the end-term project for the course CS 848: Data Cleaning using Machine Learning*

*The project is still under development at the Data Systems Group Lab. My contribution to the project was limited to system optimization, dataset curation and experimentation scripts*

*Since the project is not yet public, my description of the project will only be limited to idea and not actaul implementation details.*


### # Background:

Data Cleaning has much important when data is extracted from unreliable sources and also when data is combined from multiple sources. There has been much work in finding automated, efficient and reliable ways to clean data in relational databases by means of functional dependendancies, [conditional functional dependencies](https://www.inf.ed.ac.uk/publications/online/0949.pdf) and [denial constraints](http://www.vldb.org/pvldb/vol6/p1498-papotti.pdf). This project brings the idea of denial constraints to RDF data which is composed of interconnected triples and not fixed dimension tuples. By virtue of the structure of data and also the because of the fact that RDF data is schemaless, discovering denial constraints is relatively tough and non-trivial. 

The project, in a larger domain, beigns by defining a concrete semantics of denial constraint rules for RDF datasets using a subset of [SHACL (SHApe Constriant Language)](https://www.w3.org/TR/shacl/). It then traverses the graph node by node enumerating properties that exist and also its value. Based on the datatype of the property and values, it ennumerates features for a property like if its categorical or numerical. Given all the found features, a space of all possible rules can be defined. Finally, a search algorithm searches this space of all denial constraint rules across all the nodes and different types, to list down the handful of rules that have a significant support from the input data.

### # Contributions:

My contribution to the project were manifold:
1. Improve the mechanism used for ranking the generated set of constraint rules. The geenrated rules are then pruned based on a minimum support threshold.
2. Improve the graph exploration mecahnism to consider a larger neighbourhood graph for each node. The idea for this was to get richer rules that are non-trivial but true.
3. Several optimizations in the core rule space searching to reduce the plausible candidates.
4. Dataset curation: I searched for the dataset and manually found a handful set of rules taht served as the golden results against which the output of the algorithm was compared to.
5. Wrote the algorithm for matching golden rules to the generated set of rules and report Precision and Recall.

### # Acknowledgement
I would like to thank [Prof. Ihab Ilyas](https://cs.uwaterloo.ca/~ilyas/) and Mina Farid for giving me the opportunity to work on their project. 