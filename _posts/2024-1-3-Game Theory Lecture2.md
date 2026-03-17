---
layout: post                    # 使用的布局（不需要改）
title: Game Theory with Applications to Finance and Marketing I, Lecture2 Notes (Sep. 29)                # 标题 
subtitle: Game Theory # 副标题
date: 2024-1-7 20:37:22               # 时间
author: czx                       # 作者
math: true
mermaid: true
catalog: true                        # 是否归档
categories: ['Course Notes', 'Game Theory ( FIN7035 )']
tags: # 标签
  - Game Theory
  - Lecture Note
  - Finance
  - Math
---

# Game Theory with Applications to Finance and Marketing Lecture 2 (sep29)

## Thinking: Red-Black Hair Game

```
A village has three residents, and they all know that a resident’s hair can be either red (R) or black (B). A resident can see the color of each neighbor’s hair, but does not know the color of his own hair. The three residents are not allowed to communicate in any way. They must meet (quietly) for 1 hour at 9am each day, trying to figure out the color of his own hair. Suppose that a resident that figured out the color of his own hair by the evening of date t would be allowed (by Trump, unlikely?) to immigrate to the USA in the evening of date t. The three residents all wish to immigrate to the USA as early as they can. Suppose that exactly one of the three resident has black hair.

(i) Suppose that the three residents’ first meeting is at date 1. When
would a red head get to immigrate to the USA?

(ii) Suppose that at date n ≥ 1, an honest person passed through the
village at 9:20am (whose honesty is well known to the residents), and
he told the three residents during their daily meeting that at least one
of them has red hair. At which date would a red head get to immigrate
to the USA? At which date would the black head get to immigrate to
the USA?
```

**Solution:**

(i) 如果只是看，肯定是看不出的，时间为$\infty$。

(ii) 这个时候大家有了**common knowledge**，即，三个人都知道了我们之间至少有一个红头发，并且关键的是这件事情成为了三个人的共识。

假设这个honest man告诉他们这个common knowledge的时间为$n$，三个人分别为$A, B, C$，其中$A, B$是红头发，$C$是黑头发，我们有：

* 第$n+1$天（知道这个事实后的第一天），其实都不知道会怎样，**三个人还是会去广场聚会。**因为：
  * 在$A$眼里：$B$是红头发，$C$是黑头发。自己可能是红头发，可能是黑头发，猜不出来。
  * 在$B$眼里：$A$是红头发，$C$是黑头发。自己可能是红头发，可能是黑头发，猜不出来。
  * 在$C$眼里：$A,B$都是红头发。自己可能是红头发，可能是黑头发，猜不出来。
  * 这个时候，三个人都没有动作。（注意没有动作也是一种common knowledege，表示大家都不知头发会是什么颜色）
  * 但是请注意：
    * 如果$A$猜出了自己是黑头发，$A$就会走了，但是$A$没有走，证明$A$没猜出来；
    * 如果$B$猜出了自己是黑头发，$B$也会走，但是$B$没走，说明$B$也没猜出来；
    * 所以$A,B$都没猜出来自己是什么头发颜色。**如果$A$是黑头发，$B$就会走；$B$是黑头发，$A$就会走。（因为至少有一个红头发，如果$A$和$C$都是黑头发，则$B$一定是红头发；反之也成立）**
    * 所以$A,B$都没走
* 第$n+2$天，大家又回来，发现：
  * $A,B$都没走，说明两个人都没猜出来自己是什么头发颜色 $\Longrightarrow$ 两个人也明白了对方知道自己没猜出来自己头发是什么颜色 $\Longrightarrow$ 所以两个人都是红头发（看到对方来了广场那一眼就知道了）
  * 所以，$A,B$在$n+2$天可以移民美国。
  * $C$还不知道。
* 第$n+3$天，发现只有$C$在广场上了：
  * 这个时候$C$明白，$A,B$都知道自己是红头发了。
  * 如果$C$自己是红头发，那$A,B$在第$n+2$天是无法判断自己的头发颜色的，自然也就不可能去美国了。
  * 但是$A,B$判断出来了，所以$C$不可能是红头发！$C$只可能是黑头发。（注意这里不要倒推因果）
    * 所以$C$在第$n+3$天移民美国。$\blacksquare$

## Review of Definition

## Definition of Game

**Definition 1 (Normal Form)** A game can be described by:

* (i) the set of players,
* (ii) the strategies of players,
* (iii) the payoffs of players as functions of their strategies.

**Hint:**

* 注意赛局中有另一个假设：即假设所有的player都是**理性的**。

### Definitions of knowledge

#### Mutual Knowledge and Common Knowledge

**Definition 2 (mutual knowledge)** An event is the players' *mutual knowledge* if all players know the event.

**Definition 3 (common knowledge)** An event is called the players’ *common knowledge* if all players know it, all players know that they all know it, all players know that they all know that they know it, and so on, and so forth.

**Hint: **

* **mutual knowledge**指的是所有人都知道的东西。
* **common knowledge**在mutual knowledge上更进一层，指的是不但所有人都知道的东西，而且所有人都知道所有人都知道这个东西（互相知道了知道的事实）。

### Definition of Extensive Form

**Definition 4 (Extensive Form)** Extensive Form adds another thing to normal form, which is:

* timing
* information set

## Solution Rules to Games

* Rational players will never adopt *strictly dominated strategies*.
* Common knowledge about each player is, every player is a rational player.
* Common knowledge about each player’s rationality implies that rational players will never adopt *iterated strictly dominated strategies*.
* Common knowledge about each player’s rationality implies that rational players will never adopt *iterated weakly dominated strategies*.
* Rational players will never adopt *weakly dominated strategies*.

## Dominated Strategies

### Weakly dominated strategy

**Definition 4** We say that $\sigma_i$ is weakly dominated by $\sigma_i^\prime$ for player $i$ if:

$$
u_i(\sigma_i, \sigma_{-i}) \leq u_i(\sigma_i^\prime, \sigma_{-i}), \forall \sigma_{-i} \in \Sigma_{-i}
$$

其中，$\Sigma_{-i}$是除了player $i$之外所有player的策略集合的笛卡尔积，即：

$$
\Sigma_{-i} = \Sigma_1 \times \Sigma_2 \times \dots \times \Sigma_{i-1} \times \Sigma_{i+1} \times \dots \times \Sigma_I
$$

如果将公式$(1)$中的不等号变成小于号，则称$\sigma_i$是$\sigma_i^\prime$的**strictly dominated strategy**.

这个公式其实表明的是，自己出招$\sigma_i$和$\sigma_i^\prime$，不管别人出什么招，$\sigma_i^\prime$，那$\sigma_i^\prime$就是一个weakly dominated strategy；如果$\sigma_i^\prime$严格比$\sigma_i$的收益来的好，那就是strictly dominated strategy。

### Example: Find dominated strategy

Let's see the *prisoner's dilemma* question:


**Solution:**

其中，对player1来说，Not Confess相对于Confess是一个*Strictly dominated strategy*，因为：

1. 如果player2选择Not Confess，player1采取Confess得到的收益是1，采取Not Confess得到的收益是0，1比0高；
2. 如果player2选择Confess，player1采取Confess得到的收益是-2，采取Not Confess得到的收益是-3，-2比-3高。

因此，在这一个单一的静态赛局中，Not Confess相对于Confess是一个Strictly dominated strategy。

> 当然，这里无脑选择Strictly dominated strategy肯定不是最优的，最优的肯定是两个人的都Not Confess。

### Method of Finding strategies

基于上面提到的weakly dominated strategy和strictly dominated strategy，我们可以利用理性人不会选择弱势策略的办法来删除一些策略，从而得到双方会使用的策略组合。

不过需要注意：

* 如果删除的都是strictly dominated strategy，则删除的顺序对最终的结果没有影响；

## Reference
This note is mainly derived from Chyi-mei Chen's `Game Theory with Applications to Marketing and Finance, I` Course @ National Taiwan University.
Thanks him for giving this kind of excellent lecture.
