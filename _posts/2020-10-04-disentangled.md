---
title: 【Progess Report】Disentangled Embeddings
author: Sean
date: 2020-10-04 18:00:00 +0800
categories: [Blogging,Report]
tags: [Disentangled]
math: true
---

### 论文集


 (NeurIPS 2018) Learning Deep Disentangled Embeddings With the F-Statistic Loss

(ICLR 2019) [**Disentangled Graph Convolutional Networks**](http://proceedings.mlr.press/v97/ma19a/ma19a.pdf)

[Code](https://github.com/THUDM/cogdl)

**DisenGCN**：首先预设得到的 Disentangled Embeddings包含K个独立的Factor，那么得到的节点embedding可以表示为:

$$ \mathbf{y}_u = [ c_1, c_2, ..., c_K ] $$

首先计算 \\(z_k\\) 为 节点特征\\(x_i\\)乘以\\(W_k\\)得到的不同子空间的投影，然后再利用迭代算法，对节点u的每个邻接节点v，计算factor k是节点u,v之间连接原因的概率\\(p_{v, k} \\) ，根据这个概率对节点u的\\(c_k\\)进行更新。

![Iteration of routing](https://i.loli.net/2020/10/10/15ZHuRfiObrvz2J.png)


**Note**: 这篇文章的写作浅显易懂，很适合入门参考，尤其是可以学习下套用EM算法部分。


(ACL 2020) [**Graph Neural News Recommendation with Unsupervised Preference Disentanglement**](https://www.aclweb.org/anthology/2020.acl-main.392/)

**Background** : 给定一个user-news的历史交互集合\\( { (u, d) } \\)，模型的目标是预测一个user是否会点击某个他以前没有见过的新闻d。 其中新闻文章 \\(d \\) 包含标题 \\( T \\)  以及profile \\( P \\) （即该新闻的关键词集合，带关键词的类型标注，如人名-person）。

**Model**: 假设user的click behaviors是由不同的latent preference factors造成的，定义用户u和新闻d的disentangled representations \\( \mathbf{y_u} \\)和 \\( \mathbf{y}_d \\) 。

![GNUD](https://i.loli.net/2020/10/11/rcRbQSG6wFizxtp.png)

因为数据集包含user点击news和news被多个users点击两种数据，所以相当于是个bipartite graph。 对于\\( \mathbf{y_u} \\)和 \\( \mathbf{y}_d \\) 的学习过程基本上都是跟DisenGCN一样的。

**Note**: 模型跟上一篇基本一样，只是改到了新闻推荐中。未开源。数据集可下载。


(SIGIR 2020) [**Disentangled Graph Collaborative Filtering**](https://dl.acm.org/doi/abs/10.1145/3397271.3401137)

[Code](https://github.com/xiangwang1223/disentangled_graph_collaborative_filtering)

**Background**: 给定users集合 \\( {u} \\) ，Items集合 \\( {i} \\)和交互集合 \\( {y_{ui}} \\)，CF的目的是预测\\( u \\)购买\\( i \\)的可能性 \\( \hat{y_{ui}} \\)。

**Model**: 



![Framework](https://i.loli.net/2020/10/10/HLquIXiGyZsK2NT.png)


**Note**: 


(arixiv 2019) [Disentangled State Space Representationsk](https://arxiv.org/abs/1906.03255)

Note:


(ICML 2018) [Disentangled Sequential Autoencoder](http://proceedings.mlr.press/v80/yingzhen18a.html)



### 思考

Disentangled很适合用来做dynamic embedding

能否将temporal information作为其中一个factor？比如，一个节点的邻居节点和发生变化时，如果采用传统的SSM模型，他不应该是所有的embedding dim都发生Transfer的，如果能做Disentangled，那么应该只有部分维度（部分相关的factor）发生transfer。