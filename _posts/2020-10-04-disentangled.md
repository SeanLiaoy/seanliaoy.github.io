---
title: 【Progess Report】Disentangled Embeddings
author: Sean
date: 2020-10-04 18:00:00 +0800
categories: [Blogging,Report]
tags: [Disentangled]
---

### 论文集


 (NeurIPS 2018), Learning Deep Disentangled Embeddings With the F-Statistic Loss

(ICLR 2019) Disentangled Graph Convolutional Networks
Summary: 
Link: http://proceedings.mlr.press/v97/ma19a/ma19a.pdf

(ACL 2020) Graph Neural News Recommendation with Unsupervised Preference Disentanglement

Link: https://www.aclweb.org/anthology/2020.acl-main.392/

(SIGIR 2020) Disentangled Graph Collaborative Filtering

Link: https://dl.acm.org/doi/abs/10.1145/3397271.3401137

(arixiv 2019) Disentangled State Space Representations

Link: https://arxiv.org/abs/1906.03255



### 思考

Disentangled很适合用来做dynamic embedding

能否将temporal information作为其中一个factor？比如，一个节点的邻居节点和发生变化时，如果采用传统的SSM模型，他不应该是所有的embedding dim都发生Transfer的，如果能做Disentangled，那么应该只有部分维度（部分相关的factor）发生transfer。