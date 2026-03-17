---
layout:     post
title:      Game Theory with Applications to Finance and Marketing I, Lecture 7 Notes (Nov. 4)
subtitle:   Game Theory
date:       2024-8-11 10:17:24 +0800
author:     czx
toc:        true
math:       true
mermaid:    true
catalog:    true
categories: ['Course Notes', 'Game Theory ( FIN7035 )']
comments:   true
tags:
  - Game Theory
  - Lecture Note
  - Finance
  - Math
---


# Game Theory with Applications to Finance and Marketing I, Lecture 7 Notes (Nov. 4)

In this part, we shall continue to discuss continuous `Lecture 1-1` questions.

## Question 1::并购问题

在商业赛局中，并购是一个很重要的问题。来看下面这个例子。

![image-20240811102208602](https://s2.loli.net/2024/08/11/ByExSYaGbVFrlNM.png)

目前，某个公司有管理者$I$，称为`incubet manager`。在管理者$I$的控制下，公司将获得$Y_I$的收入，管理者自己会拿到$Z_I$的报酬。现在有另一个潜在的管理者，称其为$C$，与管理者$I$竞争。如果让$C$来管理公司，将获得$Y_C$的收入，$C$自己要拿到$Z_C$的报酬。

公司也有两类股东，分别成为$A$与$B$。股东之间会有分红，记为$S_A$与$S_B$。股东有投票权，暂且记录为$V_A$与$V_B$。

如果$C$想要竞争上岗，则要拿到所有股东$100\%$的选票。

> 可以发现，$C$相当于另一家公司的CEO，想要获得公司的控制权。这就是一种典型的并购。
{: .prompt-tip }

这个赛局的进行如下：

1. $C$先给股东出价，承诺会分给股东多少钱。（假设必须出整数的钱）
2. $I$知道了这个消息（要并购），也给股东出价，承诺会分给他们多少钱。（假设必须出整数的钱）
3. 最后股东进行投票，选出到底是$C$还是$I$成为公司的manager。

### Question 1.1

考虑下面的情况：$S_A = S_B = 50\%$，$V_A = 100\%, V_B = 0\%$。假设股东和manager都知道，$Y_I = 200, Y_C = 180, Z_I = 0, Z_C > 0$。

证明：如果$Z_C \geq 11$，$C$可以以$101$的价格买下所有$A$股东的股票，此时公司的市值为$191$。

#### Solution to Question 1.1

可以发现，此时$B$股东不重要，$A$股东才是要解决的对象。

在分红模式下，如果是$I$执掌公司大权，则股东$A$与股东$B$各自分$100$元；如果是$C$执掌公司大权，则则股东$A$与股东$B$各自分到90元。

如果$Z_C \geq 11$，那$C$会有一个计策。就是把自己赚到的$11$全部分给股东$A$，让其拿到$101$元。对股东$A$来说，接受是比不接受严格好的策略。而$Z_I = 0$，manager $I$没有办法反制这种策略，且$C$也不会因此获得负收益。因此并购成功。

公司的市值现在变成了多少？原先是$200$。通过这样的手段并购之后，$A$拿到了$101$；$B$拿到了$90$，相加起来是$191$。并购后，公司的市值**缩水了**。

### Question 1.2

考虑下面的情况：$S_A = 70\%, S_B = 25\%$，$V_A = 100\%, V_B = 0\%$。假设股东和manager都知道，$Y_I = 200, Y_C = 180, Z_I = 0, Z_C > 0$。

证明：如果$Z_C \geq 16$，$C$并购成功，并且公司市值此时为$196$。

#### Solution to Question 1.2

与之前相同，同样专心在解决$A$股东上。

* $I$上台，$A$分到$200 \times 3/4 = 150$；$B$分到$50$；
* $C$上台，$A$分到$180 \times 3 / 4 = 135$；$B$分到$45$。

在这种情况下，$C$补偿给$A$股东$16$，即可让$A$股东获利$151 > 150$，$A$股东有兴趣出售自己的股票。并购成功。

此时，公司市值为$151+45 = 196$，相较于`Question 1.1`，公司市值提升了。

### Question 1.3 (One share, One vote)

现在我们要通过这个例子介绍一个重要的股份原则：One share, One vote。

此时假设$S_A = 100\%, S_B = 0\%$，并且$V_A = 100\%, V_B = 0\%$。

证明：只有$Z_C \geq 21$的情况下，并购成功，且公司市值为201。

### Solution to Question 1.3

很显然，此时在$I$掌权，股东获得$200$的利益；$C$掌权获得$180$的利益。必须要补充21才能够使得股东获利$201 > 200$，并购才能成功。

> One share One vote原则让并购者必须要花更多钱摆平股东，公司的市值也随之提升，公司变好了。
{: .prompt-tip }

### Question 1.4 (free rider problem)

现在仍然假设$S_A = 100\%, S_B = 0\%$，并且$V_A = 100\%, V_B = 0\%$。不过，$I$与$C$的盈利能力发生变化。设$Y_I = 10, Y_C = 100$。

$C$该如何出价以实现并购的目标？

#### Solution to Question 1.4

看起来一个简单的想法是出价$11$元，但是存在很多问题。

* 股东数目很多，收买某一个单独股东并不能获得很多的投票权，不在投票中占优势。
* 存在free rider！一个股东会考虑到，反正自己的投票似乎是微不足道，如果$99.99999999999\%$的人都答应了，那基本上也拿到了$100%$的投票权。我不卖出，不就获利$100$了么？
* 此时每个股东都会这么想，因此$11$并不能收买到任何一个股东。

怎么办？此时$C$不得不出价$100$。公司市值也从$10$成功上升到$100$。

### Question 1.5

现在假如倒反天罡。$S_A = 0\%, S_B = 100\%$。且$V_A = 100\%, V_B = 0\%$。$Y_I = 10, Y_C = 100$，且$Z_I = 0 < 1 < Z_C$。

这个时候该如何出价进行并购？

#### Solution to Question 1.5

这时公司的所有权和投票权完全分离开了。因此，可以通过一系列手段进行操作。

$C$只需要出价$1$即可买下$A$手中的投票权。此时公司的市值又上涨了！到达了$101$。

### Conclusion

这个例子告诉我们：

* one share one note的原则是保护公司市值的重要方法，能最大程度保证在并购时公司的市值至少不下降；
* 如果并购出现，我们希望最大程度榨取并购者的个人所得$Z_C$，让其能吐出更多的钱给到公司使用。

---

## Question 2::Value of Commitment

![image-20240811112632035](https://s2.loli.net/2024/08/11/4Rc3eBIpZL2HTmu.png)

在一个有第三方的情况下，双方可以同时承诺给到第三方一个cost，从而控制自己的payoff比出卖对方来的差，从而达到一个较好的均衡。

---

## Question 3::Hirshleifer Effect

![image-20240811141544584](https://s2.loli.net/2024/08/11/Z14tX2ip3SNEMrj.png)

![image-20240811112838859](https://s2.loli.net/2024/08/11/uEkxTmaK1sNeCnj.png)

下面我们来了解一下所谓的`Hirshleifer Effect`。它告诉我们，即使拥有了更多的资讯，也不一定能得到更多的payoff。

在上面的博弈中，Player是$A$与$B$。双方在$t = 2$时候的payoff由state决定。如果$\text{state} = 1$，则player A收获$2$的payoff；如果$\text{state} = 2$，则player B收获$2$​的payoff。

### Case 1::No extra information arrive at $t = 1$

假如在$t = 1$时候没有新的information（即两人都不知道$t = 2$时将会是什么state），双方可以通过签订一个contract的方式来确保双方的payoff最大化。即：

* 如果$t = 2$时出现$\text{state} = 1$的情况，则player A提供给player B $1$的payoff；
* 如果$t = 2$时出现$\text{state} = 2$的情况，则player B提供给player A 1的payoff。

这样的话双方的expected payoff为：


$$
\begin{align*}
\text{expected payoff of player A}
& = \frac {1} {2} \times u(1) + \frac {1} {2} \times u(1) \\
& = u(\frac {0 + 2} {2}) \\
& > \frac {1} {2} u(0) + \frac {1} {2} u(2)

\end{align*}
$$


（利用Jenson inequality可得）

**发现通过议定contract后，player A的期望payoff一定严格大于未议定contract的期望payoff。**达成contract让双方的情况都变好了。

### Case 2::Extra Information Arrive at $t = 1$

假设在$t = 1$时候，一方获得了information，双方自然无从议定contract。

从获利方的角度，自然$u(2) > u(1) > u(0)$。但是从总福利的角度，$u(0) + u(2) < u(1) + u(1)$。

这便是所谓的**Hirshleifer Effect**。

**有了更多的information，总payoff居然下降了。**

---

This is the end of Lecture 1-1. $\blacksquare$

## Reference
This note is mainly derived from Chyi-mei Chen's `Game Theory with Applications to Marketing and Finance, I` Course @ National Taiwan University.
Thanks him for giving this kind of excellent lecture.
