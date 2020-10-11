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

**Background**: 给定users集合 \\( {u} \\) ，Items集合 \\( {i} \\)和交互集合 \\( {y_{ui}} \\)，CF的目的是预测\\( u \\)购买\\( i \\)的可能性 \\( \hat{y_{ui}} \\)。本文的思路是假设有k个因素会对用户购买商品造成不同影响，通过做disentangled，可以对商品推荐结果背后的影响因素进行分析，提高推荐模型的可解释性。

**Model**:  将embedding分为K块，定义 \\( S_k(u, i) \\)来表示intent k下user和item的交互概率， 初始化为1。公式(8)用来描述哪个intent对(u, i)的结果贡献更大，然后通过weighted sum aggregator来得到user对于factor k的representation \\( \mathbf{u}_k \\)。
通过与前两篇相似的迭代更新规则，模型得到每个intent下u,i交互的概率S以及用户的disentangled representation \\(e_{ku} \\)。

![Framework](https://i.loli.net/2020/10/10/HLquIXiGyZsK2NT.png)

**Note**:  文章提到了这种方法与Multi-head Attention Network的关系，确实这种对embedding划分来区别重要性的方式有点像是一种Attention机制，可以学习下作者的论述3.4.4。


### 知识图谱相关论文
(Arxiv 2020, Wechat AI)【Disentangled + Lifelong learning + Knowledge graph】 [**Disentangle-based Continual Graph Representation Learning**](https://arxiv.org/abs/2010.02565)



### VAE相关论文，主要是用在视频数据集上

(ICML 2020) [**Disentangled Representations for Sequence Data using Information Bottleneck Principle**](http://proceedings.mlr.press/v129/yamada20a.html)

(ICML 2018) [**Disentangled Sequential Autoencoder**](http://proceedings.mlr.press/v80/yingzhen18a.html)

(arixiv 2019) [**Disentangled State Space Representationsk**](https://arxiv.org/abs/1906.03255)





### 思考

Disentangled很适合用来做dynamic embedding

1.  (**简单的思路**) 不同factor的embedding，随时间变化程度是不一样的，比如商品推荐中，用户可能存在长期兴趣，也可能存在短期兴趣，可以直接建立多个transfer distribution，结合DisenGCN，可以无监督地发现用户的长短期兴趣和对购买结果的影响。时序推荐系统暂时没看到有人做。

**TODO**: transfer distribution怎么定义，用什么模型，最简单的方式可以为每个facor定义一个不同参数的transfer function。

2. （**思路不够清晰**）无监督time-vary embedding。比如时序知识图谱补全中，能不能不需要额外的学习时间的embedding，就能对中间某一时刻的缺失的fact进行补全。将temporal information作为其中一个factor，对相邻时间的embedding相似度进行建模。