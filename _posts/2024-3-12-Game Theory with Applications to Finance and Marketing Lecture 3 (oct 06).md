---
layout:     post                    # 使用的布局（不需要改）
title:      Game Theory with Applications to Finance and Marketing I, Lecture 3 & 4 Notes (Oct. 06, Oct. 13)                # 标题 
subtitle:   Game Theory # 副标题
date:       2024-3-12                # 时间
author:     czx                        # 作者
toc: true
math: true
mermaid: true
catalog:    true                        # 是否归档
categories: ['Course Notes', 'Game Theory ( FIN7035 )']
tags: # 标签
  - Game Theory
  - Lecture Note
  - Finance
  - Math
---

# Game Theory with Applications to Finance and Marketing I, Lecture3 Notes(Oct. 06 & Oct. 13)

## Math Review

Let's review some math tools for `Game Theory`.

### Set and Function

#### Set

**Definition 1 (Set, Collection, Family): **

* A well-defined collection of objects (called elements) is a **set**;
* A set of sets is usually referred to as a **collection**;
* A set of collections is usually referred to as a **family**.

**Definition 2 (Empty Set): **A set that contains nothing is called an empty set, denoted by $\phi$.

**Definition 3 (Super set and Sub set): **If two sets $A$ and $B$ are such that $B$ contains each and every element of $A$, then we say that $A$ is a **subset** of $B$ and $B$ a **superset** of $A$, we write $A \subset B$.

**Hint:** If we want to judge whether set $A$ is equal to set $B$, we need:
$$
A \subset B, B \subset A
$$
**Definition 4 (Complement): **A set $A$ has its complement set, denoted by $A^c$, which is,
$$
A^c = \{x: x \in X, x \notin A \}
$$
where set $X$ is a *universal set*.

**Definition 5 (Power set): ** Denote by $2^X$ the collection containing all subsets of $X$, which will be referred to as the power set of $X$.

#### Function

**Definition 6 (Function): **Given two sets $A$ and $B$, an assigning rule $f$ is a (single-valued) function from $A$ into $B$, if: $\forall a \in A$, there is $b \in B$, such that

$f(a) = b$. We can write:
$$
f: A \rightarrow B
$$
and 𝐴 and 𝐵 are called the domain and range of 𝑓, respectively.

**Hint:**

* If $A$ is a collection of sets, we say that $f$ is a *set function*.

**Definition 7 (Surjective, injective, and one-to-one): **

1. **Surjective** (满射)

如果有$B \subset f(A)$，则我们称函数$f$是一个**满射**。

2. **Injective** (单射)

如果满足：
$$
x, y \in A, x \neq y \Rightarrow f(x) \neq f(y)
$$
我们称函数$f$是一个**单射**。

3. **Bijective** (双射，又称一一对应, one-to-one correspondence)

如果一个函数又是surjective，也是injective，则称其为**Bijective**.

**Image and Pre-image**

**Definition 8 (Image): **

## Nash Equilibrium存在定理

在求解均衡前，要判断是否存在Nash Equilibrium。因此，需要利用几个定理来判断。

### Theorem 1 (Wilson, 1971; Harsanyi, 1973)  : NE个数

> Almost every finite strategic game has an odd number of NE’s in mixed strategies; more precisely, with the set of players and their strategy spaces fixed, the set of payoff functions that result in a strategic game having an even number of  NE’s has zero Lebesgue measure. 

> * 每一个有限赛局都有奇数个混合策略的Nash均衡
> * 即：混合策略NE+单纯策略NE=奇数

这个定理让我们明白了重要的道理。即，如果要找NE，则必须找出奇数个。如果只找到偶数个，就请再继续接着找。

### Theorem 2 (Nash, 1950)  : 混合策略存在定理

> Every finite normal-form game has at least one mixed-strategy NE (which may or may not be a pure-strategy NE).

> Theorem 2 is actually a special version of the following more general theorem (see Fudenberg and Tirole’s Game Theory, Theorem 1.2).  Which is,
>
> ![image.png](https://s2.loli.net/2024/03/11/2ynZSafYKhxqvQR.png)

> Nash的这个定理告诉我们，只要是有限的赛局必定有至少一个混合策略均衡。

### Theorem 3 (Kakutani, 1941) : 不动点存在定理

![image-20240311171538463](https://s2.loli.net/2024/03/11/yDmqOBgPITVHn2R.png)

> 这个定理是一个不动点存在定理。意思是：
>
> 一个定义在非空、凸集合、紧致集合的函数$r$，如果$r$上半连续，则存在一个不动点$\sigma^*$，使得$r(\sigma^*) = \sigma^*$成立。
>
> 显然，如果r是一个single value的函数，则r必然连续。

> **Function $r(·)$ in Game Theory :: What is "response function" ?**
>
> 所谓的response function，是指player i在其他玩家采取策略时，自己采取什么策略。函数的input可以理解成是其他玩家的策略集合$\sigma_{-i}$，输出的是player i采取的策略$\sigma_i$。

### Proof: Use Thm 3 to proof Thm 2

这部分略过。需要注意的是，NE的概念就是不动点的概念。用数学符号表达应该是：

* 假设$r(·)$是所谓的反应函数，$\sigma_i$是player i使用的混合策略。
* 本身而言，Nash均衡类似于：对方出招1，我出招2，对方必定跟着出招1。
* 假设$\sigma_*$是所有player的策略集合所组成的向量。则有，如果response（反应函数）产生的反应策略结果还是$\sigma_*$，则这个$\sigma_*$一定就是纳什均衡。
* 这就转化成了找不动点的问题。

### 没有Nash Equilibrium的情况？

要证明没有Nash Equilibrium，只要证明反应函数$r(·)$不存在不动点即可。

* 一个典型的例子是，非连续的payoff function可能导致NE不存在。

### Theorem 4 : Mixed Strategy NE?

![image-20240311175706087](https://s2.loli.net/2024/03/11/gLnGo9paKAHYBiz.png)

> 同时选择的赛局(simultaneously choose game)，payoff function连续，则该赛局必定有一个混合策略的NE。

一个类似的定理(Theorem 4')是：

> 对于一个有限赛局，若：
>
> * 只有有限个player
> * 策略集合是非空紧致集合(nonempty compact set)
> * 对所有的player i，效用$u_i$是连续函数
>
> 则赛局有一个混合策略的NE。

### Theorem 5 : NE in Symmetric game

> A finite symmetric game has a symmetric Nash equilibrium in mixed strategy.  

## Reference
This note is mainly derived from Chyi-mei Chen's `Game Theory with Applications to Marketing and Finance, I` Course @ National Taiwan University.
Thanks him for giving this kind of excellent lecture.
