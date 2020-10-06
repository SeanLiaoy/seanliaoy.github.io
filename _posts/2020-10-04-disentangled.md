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
[Paper Link](http://proceedings.mlr.press/v97/ma19a/ma19a.pdf)
[Code](https://github.com/THUDM/cogdl)

Note: 这篇文章的写作浅显易懂，很适合入门参考，尤其是怎么套用EM算法部分

(ACL 2020) Graph Neural News Recommendation with Unsupervised Preference Disentanglement
[Paper Link](https://www.aclweb.org/anthology/2020.acl-main.392/)
Note: 模型跟上一篇基本一样，只是改到了新闻推荐中。未开源。


(SIGIR 2020) Disentangled Graph Collaborative Filtering
[Paper Link](https://dl.acm.org/doi/abs/10.1145/3397271.3401137)



(arixiv 2019) Disentangled State Space Representations
[Paper Link](https://arxiv.org/abs/1906.03255)



### 思考

Disentangled很适合用来做dynamic embedding

能否将temporal information作为其中一个factor？比如，一个节点的邻居节点和发生变化时，如果采用传统的SSM模型，他不应该是所有的embedding dim都发生Transfer的，如果能做Disentangled，那么应该只有部分维度（部分相关的factor）发生transfer。