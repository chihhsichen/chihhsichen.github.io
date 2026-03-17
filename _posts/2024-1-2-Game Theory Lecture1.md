---
layout:     post   				    # 使用的布局（不需要改）
title:      Game Theory with Applications to Finance and Marketing I, Lecture1 Notes(Sep. 22)				
subtitle:   Game Theory 
date:       2024-1-2 11:57:19				# 时间
author:     czx						# 作者
toc: true
math: true
mermaid: true
catalog: true
categories: ['Course Notes', 'Game Theory ( FIN7035 )'] 						
tags:								
    - Game Theory
    - Lecture Note
    - Finance
    - Math
---

# Game Theory with Applications to Finance and Marketing I, Lecture1 Notes(Sep. 22)

## Category of Game

| | static(靜態賽局) |     dynamic(動態賽局)     |
|:--------------------------:|:----------------:|:-------------------------:|
|    **asymmetric(資訊對稱)**    |        NE        |           SPNE            |
| **non-asymmetric(資訊不對稱)** |        BE        | PBE(The most complicated) |

These are:
* Nash equilibrium (NE)
* subgame perfect Nash equilibrium (SPNE)
* Bayesian equilibrium (BE)
* perfect Bayesian equilibrium (PBE)

## Examples of the Games

### Normal form of a game

描述赛局时，通常包含以下三个部分：
* i. the set of players(赛局参加的玩家/决策者)
* ii. the strategies available to each player(决策者可以作出的决定)
* iii. the payoff of each player as a function of the vector of all players' strategic choices(决策者做出决定后得到的好处)

以上称为一个赛局的*normal form*。

### Example of a Game
![image](https://hackmd.io/_uploads/r1-28mZdT.png)
* Players? Player1 and 2
* Strategies available?
    * For player1, is $\{U, D\}$;
    * For player2, is $\{L, R\}$;
* Players get what?
    * We shall write it as a function:
    * **i.e** If player1 chooses U and player2 chooses L, it shall be written as:
        * $u_1(U, L) = 0$
        * $u_2(U, L) = 1$
* **Hint:** 函数$u_1(., .)$和$u_2(., .)$被称为两个player的效用函数(*payoff functions*)

### Definition of NE(Nash equilibrium)
假设player1的策略集为X，player2的策略集为Y，如果对$x^* \in X$, $y^* \in Y$都有:
$$
u_1(x^*, y^*) \ge u_1(x, y^*)
$$

$$
u_2(x^*, y^*) \ge u_2(x, y)
$$

相当于：
* 从player1的角度：对手出招$y^*$，我无论出招什么，结果都不比$x^*$这一招来的好；
* 从player2的角度：对手出招$x^*$，我无论出招什么，结果都不比$y^*$这一招来的好；
* 其实是一种*站对方立场*考虑的方式

**这样的一个策略对(strategy pair) ($x^*, y^*$)被称为一个赛局的Nash equilibrium。**

### Mixed Strategy
一个混合的策略是说，player不是单纯的出招x，而是在ta可行的策略集合中，以一个概率分布来出招。
例如：
![image](https://hackmd.io/_uploads/r1-28mZdT.png)
* player1 可以设定自己出招U的概率为1/2，出招D的概率为1/2，这就是一个混合策略；
* player2可以设定自己出招L的概率为1/3，出招R的概率为2/3，这也是一个混合策略。

### NE for Mixed Strategy
以下面这个例子为例，求解player1和player2的混合策略？
![image](https://hackmd.io/_uploads/r1-28mZdT.png)

> 解:
> 我们可以设定player1出招U的概率为p，出招D的概率为1-p；player2出招L的概率为q，出招R的概率为1-q。
> 先站在player1的角度考虑，player1的混合策略为：无论player2出招是什么，他出U、D结果要一样好。这样可以解
> 1) 对player1的策略U，player2采取混合策略的情况下，player1获得的payoff为：
> $$ 0 \times q + (-1) \times (1-q)
  $$
> 2) 对player1的策略D，player2采取混合策略的情况下，player1获得的payoff为：
> $$ 2 \times (q) + (-2) \times (1-q) 
> $$
> 二者相等，解得$q = \frac {1} {3}$
    > 同理，可以解得$p= \frac {1} {2}$

### A more complicated Game
Consider a two-player game, where the two must pick an integer from the set {1, 2, ...,  100} at the same time. If they pick the same number, then they each get 1; or else, they each get zero. 
* Find the pure strategy NE’s. 
* Find the mixed strategy NE’s.


## Reference
This note is mainly derived from Chyi-mei Chen's `Game Theory with Applications to Marketing and Finance, I` Course @ National Taiwan University.
Thanks him for giving this kind of excellent lecture.
