---
title: "Binary quadratic forms"
date: 2020-2-4T00:16:03+08:00
image_webp: images/blog/Suter-banner.webp
image: images/blog/Suter-banner.jpg
isCJKLanguage: true
categories:
  - "Translation"
tags:
  - "Cryptography"
---

# 引子


我们的目的是防止区块链的世界里对手(adversaries)利用10个女人在一个月内就诞生出一个小孩(掌握了足够多资源的对手甚至有可能可以利用9个女人在一个月内就诞生出一个小孩)。为了达到这个目的，我们需要寻找一些本质上是顺序执行的计算过程，使得生小孩这一过程不能由9个女人同时工作来完成。

事实上我们已经有很多耳熟能详的方法来实现这个目标，比如为了防止你的计算机用户密码被对手运用强大的超级计算机快速暴力破解，操作系统会使用密钥派生函数(Key
derivation
function)给你的密码加固，其原理是依次hash上次结果，使得对手没法快速得到真正的密码。再比如说
bitcoin 利用 merkle tree 来计算
hash，这使得对手需要修改本次记录之后的所有记录才能篡改本次记录。这些方案的本质都是让每个计算过程都依赖于它之前的计算结果，使对手没法轻易实现并行处理。另一个
naive 想法是一直对一个数 $n$
一直求平方。直观上我们可以想像不先求出$n^2$，我们便没法求得$(n^2)^2$。

这些方案有一个共同的问题------我们没法有效地验证结果。除非验证者(verifier)可以和证明者(prover)一样重新依次执行所放所有的操作。我们需要一个类似于公钥密钥体系里一样的后门(trapdoor)，利用这个trapdoor，verifier可以快速有效验证prover给出证明。

让我们举一个例子来阐明一下。

最近一个[比利时程序员最近解决了一个密码学难题](https://www.wired.com/story/a-programmer-solved-a-20-year-old-forgotten-crypto-puzzle/)。[这个名叫Time-lock
puzzles的难题](http://people.csail.mit.edu/rivest/pubs/RSW96.pdf)的发起人之二正是
RSA 中的 Rivest和Shamir。Rivest 在 MIT Laborater of Computer
Science成立35周年的时候宣布了一个迷题。想要知道谜底很简单，你只需要一直执行平方操作即可，想要知道谜底也很不简单，你需要重复执行80万亿平方操作。一旦
Rivest
他们公开了当时用的大数的分解方式，任何人都能够快速公开验证我们的答案是不是对的。其奥秘就在于这所谓的平方操作是在一个
$\mathbb{Z}_{pq}^{*}$
的群里反复执行的。如果我们知道这个群的阶，那么我们就极大程度上简化平方操作。因为一方面
$\text{Ord}(G) = n \Rightarrow \forall g \in G, g^n = 1$。另一方面如果我们能知道$n$的素数分解方式，则我们可以得知这个群的阶数，那么问题就可以大简化，因而可以快速验证结果的正确性。

有意思的是这个沉默了20年的难题，在短短的两个月内就有两个团队宣布他们解决了该问题。一个靠的是软件算法，[另外一个团队](https://github.com/supranational/lcs35)用上了FPGA。

区块链的世界里很多这样的需要保证参与者没有做弊的场景，比如我希望一个矿工能够证明它在一段时间内一直拥有某份数据。我们需要一个像timelock
puzzle一样的只有到达某个时间才能得到结果，并且得到的结果可以高效验证真伪的函数。这个time-lock
puzzle让我们看到希望的曙光。然而这个方法在区块链的世界里行不通，因为这个难题依赖于可信第三方的
setup，我们其实没法保证这个比利时程序员没有通过某种方法从 Rivest
那里得到了大数n的分解方式。

下面介绍一种无需trusted setup的方法得到一个[可验证延迟函数(verifiable
delay
function，简称vdf)](https://eprint.iacr.org/2018/601.pdf)。所谓的vdf主要有两个特征，一是不可以并行化处理，二是处理结果能被高效验证。上面的Time-lock
puzzles正满足这两个要求，可惜这个难题需要trusted
setup。我们的方法基于二元二次型。

# 背景

# 二次型

我们称$ f(x, y) = ax^2 + bxy + cy^2 $为一个二次型，如果 $a, b, c$ 不全为
$0$，记$f(x, y) = (a, b, c)$，如果
$a, b, c \in \mathbb{Z}$，则称其为一个整二次形。我们可以将一个二次型改写成如下矩阵形式
$f(x, y) = X M(f) X^t$，其中 $X = (x, y)$, $X^t$
为其$ X $的倒置，$M(f) = \begin{pmatrix} a & b/2 \\ -b/2 & c \end{pmatrix} $。定义二元二次形式$ f = (a, b, c)$的判别式为$ \Delta(f) = b^2 - 4ac$。易知$\Delta(f) = -4 \det(M(f))$。

### 二次形式的等价

我们定义一般线性群$\text{GL}(2,\mathbb{Z})$在二次型$f$如下。令可逆矩阵$T = \begin{pmatrix} r & t \\ s & u \end{pmatrix} \in \text{GL}(2,\mathbb{Z}) $
为从$X = (x, y)$到$X^\prime = (x^\prime, y^\prime)$
的坐标变化矩阵，即$\begin{pmatrix} x^\prime \\ y^\prime \end{pmatrix} = \begin{pmatrix} r & t \\ s & u \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} $
，我们记二次型$g(x,y) = f(x^\prime, y^\prime) = a(x^\prime)^2 + bx^\prime y^\prime + c(y^\prime)^2 =  Ax^2 + Bxy + Cy^2$，记$g = fT$为$T$在$f$上的作用(可以验证定义确为群作用)，并称二次$f$和$g$互相等价。

我们可以将$g$改写成矩阵形式表示$X M(g) X^t  = g(x, y) = X^\prime M(f) X^{\prime T} = XT^t M(f) T X^t$，上式对于任意$x, y$成立，所以$M(g) = T^t M(f) T$与$M(f)$
互为合同变化。

### 二次形式的恰当等价

我们定义特殊线性群$\text{SL}(2,\mathbb{Z})$在二次型$f$如下。令正交矩阵$T = \begin{pmatrix} r & t \\ s & u \end{pmatrix} \in \text{GL}(2,\mathbb{Z}) $
为从$X = (x, y)$到$X^\prime = (x^\prime, y^\prime)$
的坐标变化矩阵，即$\begin{pmatrix} x^\prime \\ y^\prime \end{pmatrix} = \begin{pmatrix} r & t \\ s & u \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} $
，我们记二次型$g(x,y) = f(x^\prime, y^\prime) = a(x^\prime)^2 + bx^\prime y^\prime + c(y^\prime)^2 =  Ax^2 + Bxy + Cy^2$，记$g = fT$为$T$在$f$上的作用(可以验证定义确为群作用)，并称二次$f$和$g$互相恰当等价(properly
equivalent)，记为$f \cong g$。

我们定义一个判别式$\Delta$的二元二次型的等价类$C(\Delta) = F(\Delta)/\cong $，其中$F(\Delta)$为判别式为$\Delta$的全体二次型构成的集合。
由于$ \forall T = \begin{pmatrix} r & t \\ s & u \end{pmatrix} \in \text{GL}(2,\mathbb{Z})$，$\det(T) = \pm 1$，所以$\det(M(g)) = \det(M(f))$，因此$\Delta(f) = \Delta(g)$。上述定义是良定的。

约化二次型
----------

### 正规形式

称一个形式 $ f = (a, b, c) $ 为正规形式，如果
$-a < b \leq a$。令$ f = (a, b, c) $为一二元二次型，定义$ \eta(f) = (a, b + 2ra, ar^2 + br + c)$，其中$r = \lfloor \frac{a-b}{2a} \rfloor $。容易验证$\eta(f)$为正规形式。容易验证$\eta(f) = fU$，其中$U = \begin{pmatrix} 1 & r \\ 0 & 1 \end{pmatrix} \in \text{GL}(2,\mathbb{Z})$。由此可知
$\eta(f) \cong f$，我们记$f_{\text{norm}} = \eta(f)$。

### 正规化算法

1.  $r = \lfloor \frac{a-b}{2a} \rfloor$
2.  返回 $ (a, b + 2ra, ar^2 + br + c) $

### 约化形式

称一个正规形式 $ f = (a, b, c) $ 为约化形式，如果 $ -a \leq c $，且如果
$ a = c $，则有
$b \geq 0 $。可以证明任何正定形式都恰当地等价于一个唯一的约化形式。

令$ f = (a, b, c) $为一二元二次型，定义$ \rho(f) = (a, b + 2ra, ar^2 + br + c)$，其中$s = \lfloor \frac{c+b}{2c} \rfloor$。容易验证$\rho(f) = fU$，其中$U = \begin{pmatrix} 0 & -1 \\ 1 & r \end{pmatrix} \in \text{GL}(2,\mathbb{Z})$。由此可知
$\eta(f) \cong f$。我们记$f_{\text{red}}$为$f$的约化形式。

### 约化算法

1.  $f = f_{\text{norm}}$
2.  如果$f$已经为约化形式，则返回$f$，否则令$f = \rho(f)$
3.  如果$f$已经为约化形式，则返回$f$，否则重复2.

可以证明上述算法会停止，具体可[见此](https://github.com/Chia-Network/vdf-competition/blob/master/classgroups.pdf)。

构造

复合运算


我们的目的是使等价类$C(\Delta)$成为一个群。给定两个相同判别式的二元二次形式
$f_1 = (a, b, c), f_2 = (\alpha, \beta, \gamma)$，我们需要定义一个二元二次形式的乘法运算$\cdot$，并求得$f_3 = f_1 \cdot f_2$。

例如，令$f_1 = X_1^2 + Y_1^2$，$f_2 = X_2^2 + 2X_2Y_2 + 2Y_2^2$，$X = X_1X_2 + Y_2X_1 - Y_1Y_2$，$Y = Y_1X2 + Y_2X_1 + Y_1Y_2$，则可验证$f_1(X_1, Y_1)f_2(X_2Y_2) = X^2 + Y^2$。

事实上可以根据乘性格和格与二次型的对应关系得到如下算法，具体可见[Binary
Quadratic Forms: An Algorithmic
Approach](https://www.springer.com/gp/book/9783540463672)。

1.  令$g  = \frac{1}{2}(b + \beta)$，$ h = -\frac{1}{2}(b-\beta)$，$w = \text{gcd}(a, \alpha, g)$
2.  令$j = w$，$s = \frac{a}{w}$，$t = \frac{a}{w}$，$u = \frac{g}{w}$
3.  解出$ (tu)k \equiv hu+sc \mod st$，其解可以写成$ k = \mu + \nu n$，其中$n \in \mathbb{Z}$，保存$\mu, \nu$。
4.  解出$(t\nu)n \equiv h - t\mu \mod s$，其解可以写成$n =\lambda + \sigma n^\prime$，其中$n^\prime \in \mathbb{Z}$,保存$\lambda$。
5.  令
    $k = \mu + \nu\lambda$，$l = \frac{kt-h}{s}$，$m = \frac{tuk-hu-cs}{st}$。
6.  返回$f_3 = (st, ju-(kt+ls), kl-jm)$

可以证明上述算法得到一个$C(\Delta)$上的乘法运算。通过上面的约化算法我们得到了一个唯一的代表元，因此我们可以直接对比结果，但是我们还有一些重要的疑问可以留着下回分说。

下节预告
========

1.  如何快速验证平方结果？
2.  会不会有某些$\Delta$的值的二元二次型的类数很容易求得，这样我们如同
    timelock
    一样很容易求得反复平方的结果。如果上述问题的答案是否定的，那我们该如何保证我们这个方案不需要
    trusted setup？
3.  代数整数环的分式理想群模去主分式理想得到的商群就是一个代数数域的理想类群。其阶称为类数。这两个类数有何联系？这两个类群有何联系？
4.  复合算法定义得非常人工(artificial)，其背后涉及格与二次型的对应关系，如何用乘性格来描述这个算法？
