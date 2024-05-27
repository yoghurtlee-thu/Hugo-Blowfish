---
title: 1.1-n维Euclid 空间
date: 2024-02-19 19:45:03
category: 微积分
description: 微积分第一节
summary: 微积分第一节
tags:
  - 微积分
draft: false
slug: calculus-a2-1-1
---

各位老友们好，我是 Chlorine。

这是我的微积分 A（2）——多元函数微积分与级数的学习笔记，希望能给同样被微积分折磨的老友带来一点帮助。

（(1)哪去了？答：全鸽了🤣）

本系列封面图来自 [Unsplash](https://unsplash.com/) 的 [Dhru J](https://unsplash.com/@dhruj)。

## n 维 Euclid 空间

多元函数的研究对象是 n 维 Euclid 空间，也就是我们常说的 $\mathbb{R}^{n}$。一个 n 维有序实数组 $X = (x_1, x_2,\cdots,x_n)^T$ 称为 $\mathbb{R}^{n}$ 中的一个点，或者向量。[^1]

$\mathbb{R}^{n}$ 中可以定义加法，数乘和 Euclid 距离 $\Vert X_1 - X_2 \Vert$，这都是线代里面玩烂了的东西了，略过。

为了简单起见，我们后续直接用大写字母表示点（向量）。

### 开集与闭集

更新：才发现落了一个概念，可能是觉得太自然了给略了（）补上：

在 $\mathbb{R}^n$ 中，邻域指与点的 Euclid 距离小于某一值的点的集合：

$$
B(X_0,\delta) \operatorname{:=} \{X \ \vert \  \lVert X - X_0 \rVert < \delta\},\delta > 0
$$

(MathJax 渲染不了 `\coloneqq`，先拿 `\operatorname{:=}` 凑合下吧)

而去心邻域则定义为：

$$
\mathring{B}(X_0, \delta) \operatorname{:=} B(X_0,\delta) \backslash \{X_0\}
$$

---

在上学期的 VA 课程中，我曾经给这门课起了一个别名：《高等拓扑学与数理逻辑》（逃）。

因为，我们高中熟知的开闭区间，居然需要用拓扑学的概念才能进行说明。

现在我们继续用拓扑学说明一些问题（doge）。

笼统地说，下面的概念主要研究的是一个图形的边界到底属不属于自己的问题。概念很多，慢慢理解。

我们统一将点记为 X，集合记为 A：

容易证明下面几个命题：

1. 任意集合的内部都是开集。
2. 任意集合的闭包都是闭集。
3. 单点集是闭集。
4. 集合是开集的充要条件是集合与自身的内部相等。
5. 集合是闭集的充要条件是集合与自身的闭包相等。
6. 任意多个开集的并集是开集，有限多个开集的交集是开集。
7. 任意多个闭集的交集是闭集，有限多个闭集的并集是闭集。

随便挑个第一个证一下：

反证法，假设存在集合 A 的内部 $\mathring{A}$ 不是开集（注意，不是“是闭集”）。

那么 $\exists X \in \mathring{A}, \operatorname{s.t.} \forall \delta _ 0 > 0, \exists X_1, X_2 \in B (X,\delta _ 0) ,\operatorname{s.t.} X_1 \in \mathring{A}, X_2 \in A \backslash \mathring{A}$。

显然可以取一个足够小的 $\rho$，使得 $B (X_2,\rho) \subsetneq  A \backslash \mathring{A}$，这样的 $X_2$ 显然是 A 的内点，矛盾。◾︎

### $\mathbb{R}^n$ 和 $\emptyset$ 的开闭

先说结论：这俩货既是开集又是闭集。

![黑人问号.webp|400](https://chlorinedemo.s3.bitiful.net/emoji/EMJ-confused.webp)

别急，听我说。

首先 $\mathbb{R}^n$ 肯定是开集，这个容易证，那 $\emptyset$ 就是闭集。

前方高能预警！

如果空集是闭集，那就可以找到一个 $X \in \emptyset$, 使得 X 不是空集的内点（“您真是被上帝派来的——罗辑”），然而我们找不到，矛盾，所以空集是开集，那 $\mathbb{R}^n$ 就是闭集。

这种现象在数理逻辑中称为**空真命题（vacuously true）**：一个命题前提条件为 $X \in \emptyset$ 的时候，这个命题一定为真。

当然，这种“真”，很可能只具有形式上的意义了。

没错，我大一上学个有界闭区间上函数的连续性就得学这玩意。

![乐.webp|400](https://chlorinedemo.s3.bitiful.net/emoji/EMJ-Kennedy.webp)

### 集合的连通性

这个词用专业的数学语言比较难描述，我们就从直观上理解一下吧。

最直观的连通是道路连通，也就是对于集合里任意的两个点，能不能用一条全在集合内的折线段连起来，能的话就是道路连通的。

道路连通的开（闭）集称为**开（闭）区域**。容易看出，开（闭）区间实际上就是一维的开（闭）区域。

## 点列，极限和收敛性

### 点列

这也没什么新奇的，就是序列而已。为了方便，我们通常把点列 $\{ X_i \}$ 的第 j 个分量记作 $X_i ^{(j)}$。

### n 维 Euclid 空间的极限和收敛性

简单来说，我们用 Euclid 距离代替绝对值（一维 Euclid 距离），直接推广就好了。我们这里只列出当 $X \to X_0$ 时 $f (X) \to A$ 的概念。下面给的是角标无限、极限有限的定义，剩下的是类似的。

$$
\lim_{i \to \infty}X_i = A := \forall \epsilon > 0,\exists N >0,\operatorname{s.t.}\forall i > N,\lvert X_i-A\rvert < \epsilon
$$

这个极限概念和一维的最大的区别可能就是：**它没有限制方向**。在一维世界里，我们只能从左右两个方向对点进行逼近；但是在二维或者更高维度中，我们可以从无数个方向进行逼近。后面我们会看到，这会给我们研究极限带来极大的复杂性。

有极限的点列称为收敛点列。若 $\lVert X_i \rVert$ 有界，则称为有界点列。

显然，

$$
\lim_{i \to \infty}X_i = A \iff \forall 1 \leq j \leq n,\lim_{i \to \infty}x_j = a_j
$$

### Cauchy 列

与一维相似，我们有 Cauchy 列的概念。

点列 $\{ X_i \}$ 称为 Cauchy 列，当且仅当 $\forall \varepsilon > 0,\exists m \in \mathbb{N},\operatorname{s.t.} \forall m_1,m_2 > m,\lVert X_{m_1} - X _{m_2} \rVert < \varepsilon .$

显然，点列 $\{ X_i \}$ 是 Cauchy 列的充要条件是其每一个分量序列都是 Cauchy 列。

此外，我们有一个直观且喜人的结论：

$\mathbb{R}^n$ 中的 Cauchy 列收敛于一个 $\mathbb{R}^n$ 中的点。

这个性质也叫 $\mathbb{R}^n$ 的**完备性**。

## n 维 Euclid 空间的其他性质

在一维的情况下，我们有很多奇形怪状的定理，例如确界原理、单调收敛原理、闭区间套定理、有限覆盖定理等。下面我们研究一下它们在高维的推广。

### 确界原理和单调收敛原理

由于两个 $\mathbb{R}^n$ 中的点不能直接比较大小，所以点列 $\{ X_i \}$ 没有单调性的概念，因此单调收敛原理和确界原理无法推广。

不过或许有人会想：能不能用相对某个点的 Euclid 距离代替大小呢？

emmm，看起来很合理，实际上很蠢。我们随便举个二维的例子：

一个点列，先沿着直线向某个点靠近，但是距离到达 R 之后就一直在以参考点为圆心，R 为半径的圆上滑。如果用相对参考点的 Euclid 距离代替大小，那这绝对是（非严格）单调点列，但是它不收敛。这种现象本质上还是来自高维下的多方向性。

### 闭集套定理

闭区间套定理的进化，注意名字换了。我们首先要定义一个概念：直径。

$$
d(A) \operatorname{:=} \sup \{\ \lVert X - Y \rVert \ \vert \ X,Y \in A\ \}
$$

设 $\{ F_k \}(k=1,2,3, \cdots)$ 为闭集族, 满足 $F_1 \supset F_2 \supset F_3 \supset \cdots \supset F_k \supset \cdots$ 且均非空. 如果 $\lim_{k \to +\infty} d (F_k)=0$ ，则 $\bigcap_{k=1}^{+\infty} F_k$ 中有且只有一点.

证明我不放了，和一维差不多。

### 有限覆盖定理

设 $\Omega \subset \mathbb{R}^n$ 为有界闭集, $\{ G_{\alpha} \} (\alpha \in I)$ 为 $\Omega$ 的一个开覆盖, 则在 $\{G_\alpha\}(\alpha \in I)$ 中, 存在有限个开集 $\{G_{\alpha_i}\}, \alpha_i \in I, i=1,2, \cdots, N$ 覆盖 $\Omega$ :

$$
\Omega \subset \bigcup_{i=1}^N G_{a_i}
$$


[^1]: 这种说法是不完全严谨的，主要是为了借助线性代数的一些概念来简化我的说明。在线性代数中，我一般将 $\mathbb{R}^{n}$ 称为向量空间，其元素称为向量，而对推广的向量空间使用“线性空间”和“线性元”这两个名词。