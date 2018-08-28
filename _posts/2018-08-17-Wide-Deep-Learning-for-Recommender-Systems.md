---
layout: post
title:  "Wide & Deep Learning for Recommender Systems"
date:   2018-08-17
categories: [Machinelearning]
tags: [paper, deep learning, recommender system]
---

A recommender system can be viewed as a search ranking
system, where the input query is a set of user and contextual
information, and the output is a ranked list of items.

One *challenge* in recommender systems, similar to the general search ranking
problem, is to achieve both **memorization** and **generalization**.

Memorization can be loosely defined as learning the frequent co-occurrence of
items or features and exploiting the correlation available in the historical data.
(more topical and directly relevant to the items on which users have already
preformed actions)

Generalization, on the other hand, is based on transitivity f correlation and
explores new feature combinations that have never or rarely occurred in the past.
(improve the diversity of the recommended items)

Memorization can be achieved effectively using cross-product transformations
over sparse features. One limitation of cross-product transformations is that
they do not generalize to query-item feature pairs that have not appeared in the
training data.

Embedding-based models can generalize to previously unseen query-item feature
pairs by learning a low-dimensional dense embedding vector for each query
and item feature.  However, it is difficult to learn effective low-dimensional
representations for queries and items when the underlying query-item matrix is
sparse and high-rank.

The recommender system returns a list of apps (also referred to as impressions)
on which users can perform certain actions such as clicks or purchases.
These user actions, along with the queries and impressions, are recorded in the
logs as the training data for the learner.

1. retrieval (candidate selection) machine-learned models + human-defined rules
2. ranking

*Wide & Deep learning*, jointly trained wide linear models
and deep neural networks, to combine the benefits of memorization and
generalization for recommender systems.

*The Wide Component*

The wide component is a generalized linear model.

*The Deep Component*

The deep component is a feed-forward neural network.

*Joint Training of Wide & Deep Model*

The wide component and deep component are combined using a weighted sum of
their output log odds as the prediction, which is then fed to one common
logistic loss function for joint training.

The implementation of the model is available in 
[here](https://github.com/tensorflow/models/tree/master/official/wide_deep).

According to the experiments above, the wide and deep model truly shines on larger data
sets with high-cardinality features, where each feature has millions/billions of
unique possible values (which is the specialty of the wide model).

Blog from the author is available in [here](https://ai.googleblog.com/2016/06/wide-deep-learning-better-together-with.html)

Official tutorial is [here](https://www.tensorflow.org/tutorials/representation/linear)
