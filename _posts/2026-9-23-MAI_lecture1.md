---
layout:     post
title:      Multimodal Artificial Intelligence Lecture 1
subtitle:   MAI
date:       2026-9-22 23:37:45 +0800
author:     czx
toc:        true
math:       true
mermaid:    true
catalog:    true
categories: ['Course Notes', 'Multimodal AI (CSIE5412)']
comments:   true
tags:
  - Lecture Note
  - Multimodal AI
---

# CSIE5412 Multimodal AI Lecture 01: Introduction and Review of Deep Learning

In this lecture, we will go through the essentials of deep learning by reviewing the most famous paper *Deep Residual Learning for Image Recognition* in deep learning.



For this lecture, the core is illustrating us how to read a research paper rather than teaching the deep learning basics.

## How to Read a Paper?

一般来讲，go through 一篇 paper 的大致方向或做法可以是

$$
\boxed{\text{Authors} \rightarrow \text{Abstract} \rightarrow \text{Introduction} \rightarrow \text{Related Work} \rightarrow \text{Method Details} }
$$

Make sure that **DO NOT** check all technical details at the very begging of reading a paper.

## Authors

就像中学时代的语文课老师让你了解作者一样，读 paper 的时候**看到熟悉的名字也是很重要的**。

## Abstract

我们先从这篇文章的 Abstract 部分开始讲起。一般可以发现，Abstract 大致上是三个部分组成的：1) 前提，讲自己这篇 paper 大概做了什么；2) 目的，或者说 contribution 大概是什么；3) 实验的结果



It can be written as the following diagram / trajectory:


$$
\boxed{
\text{Motivation}
\rightarrow
\text{Approach / Contribution}
\rightarrow
\text{Findings}
}
$$

Let's see the paper.



### Motivation

Motivation, 或者讲成*铺陈*，主要是想表达在这个 paper 中，面临的问题是什么。比如在这里，是这么写的



> Deeper neural networks are more difficult to train.

就这样简单的一句话。当然， kaiming 的写作风格不一定正确，但这一句话就讲出来了 `为什么要有这篇文章` 的大哉问。

### Contribution

Contribution 的部分主要是**<u>讲 paper 的贡献是什么</u>**，重点是要和 Motivation 呼应上。这篇 paper 的contribution主要就是三个：

> 1. We present a residual learning framework to ease the training of networks that are substantially deeper than those used previously.
>    
> 简单讲就是 propose 了一个 learning framework 用来解 Motivation 中间讲的很难 train 的问题
> 2. We explicitly reformulate the layers as learning residual functions with reference to the layer inputs, instead of learning unreferenced functions.
>    
> 这里在1的基础上更加细节，讲的是 paper 是怎么做的 $\rightarrow$ 方式就是重新构建 layer 来 learn residual functions 而不是直接 learn 整个 function
> 3. We provide comprehensive empirical evidence showing that these residual networks are easier to optimize, and can gain accuracy from considerably increased depth. 
>    
> 最后一个 contribution 就是实验结果了，实验结果很好，用了什么方法。你可以发现 easier to optimize 这里又和 Motivation 呼应上了

### Findings

在这篇文章里，结果，或者是 Findings ，Abstract 的写法大致就是在什么 dataset 上做了什么实验，compare to 别的 model 在相同 dataset 结果如何。



![image-20260922235539832](https://files.seeusercontent.com/2026/09/22/M5kc/image-20260922235539832.png)



当然这篇文章写的很神奇的点是，kaiming 又花了第二段进行他的火力展示，也就是讲在另一个 benchmark COCO 上的实验结果。当然了，他是 kaiming 他想怎么写就怎么写。



![image-20260922235809757](https://files.seeusercontent.com/2026/09/22/5sAf/image-20260922235809757.png)



## Introduction

In one research paper, we can view the introduction part as a detailed abstraction. This means that, each component in introduction should be aligned with the abstract.



换句话说，在 Introduction 这个 part ，最好是要和 Abstract 的写法一致。上面提到的东西这里最好也提到，而且是应该展开来讲，而不是泛泛而谈。我们看 kaiming 是怎么写的。

### Motivation in Introduction

首先来看对应 motivation 的部分。这里是扩写了一下。我们看第一段



先铺陈一下故事背景：
Deep convolutional neural networks [22, 21] have led to a series of breakthroughs for image classification [21, 50, 40].Deep networks naturally integrate low/mid/highlevel features [50] and classifiers in an end-to-end multilayer fashion, and the “levels” of features can be enriched by the number of stacked layers (depth). 



随后点出问题，就是在 deep learning 中发现

Recent evidence [41, 44] reveals that network depth is of crucial importance.

也就是说 network 的深度是很重要的。



and the leading results [40, 43, 12, 16] on the challenging ImageNet dataset [35] all exploit “very deep” [40] models.

这里就是说现在的研究者 focus 在哪，很明显点出了 motivation 里的方向是现在大家研究的方向，显得很有价值。



$\longrightarrow$ 总的来说，第一段就是点出 depth of neural network is important 。有点像作文里的**点明主题**。



第二段，就开始自问自答了，进一步讲述。比如这里是通过下面的话来提问题的

Driven by the significance of depth, a question arises: Is learning better networks as easy as stacking more layers?

当然在 paper 里发问绝对不是真的问你问题，而是作者早有答案 :)



接着开始点出几个目前的现状，为了引出 contribution 。这里大概是可以看成两个点。



1. **Vanishing / Exploding gradients**
   An obstacle to answering this question was the notorious problem of vanishing/exploding gradients [1, 9], which hamper convergence from the beginning
   然后介绍一下现在的人在这里的工作
2. **Degradation Problem**
   When deeper networks are able to start converging, a degradation problem has been exposed: with the network depth increasing, accuracy gets saturated (which might be unsurprising) and then degrades rapidly.  Unexpectedly, such degradation is not caused by overfitting, and adding more layers to a suitably deep model leads to higher training error, as reported in [11, 42] and thoroughly verified by our experiments. Fig. 1 shows a typical example.



这里的1和2当然就是我们 paper **提出来**并且**想解决**的问题。



这里对于这个 degradation 问题，又进行了一些详细说明。这是第四段的内容。这里主要讲的问题是，理论上model虽然很deep，但model如果只是一个identity mapping，总不能比shallow的model差吧？因为直接复制粘贴input到output就好了。

但是Figure 1推翻了这一点。他们发现layer层数变多，training的error和testing的error反而是会变大的。



![image-20260923102006777](https://files.seeusercontent.com/2026/09/23/J3wi/image-20260923102006777.png)



### Contribution

第五段就开始讲 paper 提的方法了。也就是从 learn $\mathcal{H}(x)$ 转化为 $\mathcal{H}(x) = \mathcal{F}(x) + x$。在这种 settings 之下，$x$ 本身是一个 identity mapping，我们只要关心怎么 learn $\mathcal{F}(x)$ 即可。



![image-20260923103826749](https://files.seeusercontent.com/2026/09/23/dpJ6/image-20260923103826749.png)



随后又补充一下机制，也就是 Figure 2. 的部分



![image-20260923103902613](https://files.seeusercontent.com/2026/09/23/Lp8h/image-20260923103902613.png)



这里就讲了两个好处 of residual connection / shortcut connection

* Shortcut connections simply perform identity mapping
* Moreover, the shortcut connections will not add any extra parameter or computational complexity. Still can be trained end-to-end by SGD with back propagation



随即讲了一下贡献



![image-20260923104122504](https://files.seeusercontent.com/2026/09/23/Pc0a/image-20260923104122504.png)



这也是一种常见的写法了，就是 show 出来大概做了两个事情。

### Findings

最后又是火力展示一遍，这也符合在 abstract 里讲过的东西。



![image-20260923104214432](https://files.seeusercontent.com/2026/09/23/v4vU/image-20260923104214432.png)



### Figure 1. of Introduction

在 Introduction 的写作中，我们也可以放一张图。但这张图一般是富有深意的，比如在这里的图是



![image-20260923010021292](https://files.seeusercontent.com/2026/09/22/t8pU/image-20260923010021292.png)



这种图都是 serve as a teaser ，目标就是让读者看到就可以抓到 paper 的 contribution 所在。

### The Writting Essentials

We can find that in this introduction part, the author used a writing structure like,


$$
\boxed{
\underbrace{\text{铺陈}}_{\text{Para. 1}}
\rightarrow
\underbrace{\text{Depth is important in networks}}_{\text{Para. 2}}
\rightarrow
\underbrace{\text{有东西没解决}}_{\text{Paras. 2--4}}
\rightarrow
\underbrace{\text{In this paper, we propose ResNet}}_{\text{Para. 5}}
\rightarrow
\underbrace{\text{Our proposed method has several contributions}}_{\text{Paras. 6--7}}
\rightarrow
\underbrace{\text{展示实验结果}}_{\text{Paras. 8}}
}
$$


## Related Work

写完上面的部分就来到了 related work 。这一个部分的用处其实就是通过翻之前文章的方式，再次证明一篇 paper 在这个 community 所能作出的贡献。

一般来说，讲的就是现有的东西发展到哪里，有什么 pros and cons.



这里有意思的是，之前已经有人提出了 highway networks 了，基本的思路也是有一个不同 implementation 方式的 connection 。这篇文章为了防止撞车，其他人来 challenge 贡献，特意是点出了 ResNet 和之前的 highway networks 的不同之处。



![image-20260923105111582](https://files.seeusercontent.com/2026/09/23/J4sk/image-20260923105111582.png)



## Deep Residual Learning

第三段这里叫 Deep Residual Learning, 其实在现在的文章这就是所谓 Methods 的部分。这一部分主要还是展开讲解提出的 methods 的细节，相关的问题以及是怎么去解决的。

### Residual Learning

比如这里，首先又提了一遍 Residual Learning 。这个毫无疑问是有重复的，但是呢，contribution不停讲好像也是合理的一件事情。至少又保持了一致性。



![image-20260923105551310](https://files.seeusercontent.com/2026/09/23/9orS/image-20260923105551310.png)



接下来就讲了一下 degradation problem 。告诉我们的还是之前的东西，就是理论上
$$
\text{Add Layer} \rightarrow \text{Learn an Identity Mapping will not affact the network} \rightarrow \text{实则不然，就是会有 error } \uparrow
$$


![image-20260923105818856](https://files.seeusercontent.com/2026/09/23/f5Wm/image-20260923105818856.png)



### Network Architecctures

这里稍微提到的就是他们用的baseline，对比的东西和自己 propose 的改进。分别有三种

* **Plain Network**
* **VGG-19**
* **Their ResNet**



![image-20260923110003686](https://files.seeusercontent.com/2026/09/23/tSr4/image-20260923110003686.png)



这里可能值得学习的是 kaiming 的这种图，看起来很简单一目了然。但是现在 agent 画图太强了，这种图还是不太受欢迎。



### Implementation

现在这个部分一般会变成 4.1 的部分，也就是 Experiment Setup 。但还是他是 kaiming 他想怎么写就怎么写。



这里有价值的一个点是，他承认了用这种 10-crop testing ，也就是一种刷榜的好技术。这个可以学。



![image-20260923110204265](https://files.seeusercontent.com/2026/09/23/d0Cj/image-20260923110204265.png)



## Experiment

在这一节里，我们最需要关注的当然是整个的 big table 。作者的文字一般都是补充说明，但是剩下的都是很重要的。比如在这里就直接先讲一下不同parameter的东西



![image-20260923114723629](https://files.seeusercontent.com/2026/09/23/1uVv/image-20260923114723629.png)



然后的话，作者使用的是分析讨论的方式来证明说 ResNet 是有效的。大概是两个方式：

1. 展示 baseline 的 results。通过看 variants 和现有的相比，以及一些 ablation的方式来证明
2. 这是现在的方法。首先放一张特别大的表，来说明和别人比我们的这个是有用的 $\rightarrow$ 再加上 ablation study

比如在这里，首先展示了一下 ResNet 的结果



![image-20260923115702176](https://files.seeusercontent.com/2026/09/23/Jq6v/image-20260923115702176.png)



确实说明了使用 ResNet 之后，deeper network is stronger than plain network regarding to error rate



包括下面这个表格也是一样的道理



![image-20260923115759380](https://files.seeusercontent.com/2026/09/23/3Bfu/image-20260923115759380.png)



接着呢，就是和现有的这些 baseline model 进行 performance 的比较了。



![image-20260923115833852](https://files.seeusercontent.com/2026/09/23/7Gjs/image-20260923115833852.png)



![image-20260923115842869](https://files.seeusercontent.com/2026/09/23/Ak4y/image-20260923115842869.png)



这样就完成了现在 paper 里那个大表的任务。随后在 Table 3 中，主要是讲了三种实现的方式的差别

1. zero-padding shortcuts are used for increasing dimensions, and all shortcuts are parameter-free
2. projection shortcuts are used for increasing dimensions, and other shortcuts are identity
3. all shortcuts are projections

结果是下面这样：

> B is slightly better than A. We argue that this is because the zero-padded dimensions in A indeed have no residual learning. C is marginally better than B, and we attribute this to the extra parameters introduced by many (thirteen) projection shortcuts.

当然，一个 dataset 是不够的。paper 又补充了另一个 dataset CIFAR-10 上的结果



![image-20260923120353480](https://files.seeusercontent.com/2026/09/23/j9eK/image-20260923120353480.png)



![image-20260923120420733](https://files.seeusercontent.com/2026/09/23/ya4X/image-20260923120420733.png)



总之，这篇 paper 大概就提供了这样的一些 writing 的逻辑和 reading 的方式。