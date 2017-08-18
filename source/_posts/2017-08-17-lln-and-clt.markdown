---
layout: post
title: "统计释疑(3)：大数定理和中心极限定理"
date: 2017-08-17 23:49:29 -0600
comments: true
categories: statistics
---

两个必须得记住并理解的统计学定理：大数定理和中心极限定理。有相当多的统计学理论是以这两个定理为基础。另外从我个人理解，这两个定理在一定程度上解释了为什么数据越多越好（为什么我们需要大数据）。

### 收敛的类型

为了更加准确的理解上述两个定理，我们需要理解概率层面的收敛，而非微积分里的收敛（如果对与任意$\epsilon>0$和足够大的$n$，$\vert x_n -x \rvert < \epsilon$，那么我们称这一实数列$x_n$收敛于极限$x$）。

在统计中，主要有两种类型的收敛：

<!--more-->

> 令$X_1,X_2,\dots$为一系列随机变量并令$X$为另一个随机变量。令$F_n$表示$X_n$的概率密度函数 (CDF)，$F$表示$X$的概率密度函数。
> 1) $X_n$在概率上收敛于$X$ (converges in probability)，写作$X_n\xrightarrow[]{P} X$，如果对于任意$\epsilon>0$

$$ \mathbb{P}(\vert X_n - X\vert>\epsilon) \rightarrow 0$$

> 当$n\rightarrow\infty$。
> 2) $X_n$在分布上收敛于$X$ (converges in distribution), 写作$X_n\rightsquigarrow X$，如果对于任意在$F$中连续的点$t$，

$$\lim_{n\rightarrow\infty}F_n(t)=F(t)$$

另外由$X_n\xrightarrow[]{P}X$可以推出$X_n\rightsquigarrow X$。

P.S. 其实还有另外两种类型的收敛，他们之间的关系也更加复杂，这里的重点是介绍两个定理，所以这部分从简，想深入了解可参考相关教材。

### 大数定理 (The Law of Large Numbers)

令$X_1,X_2\dots$为独立同分布 (IID) 的样本，令$\mu=\mathbb{E}(X_1)$，$\sigma^2=\mathbb{V}(X_1)$。另外$\bar X_n = n^{-1}\sum_{i=1}^nX_i$为样本均值并且$\mathbb{E}(\bar X_n)=\mu$，$\mathbb{V}(\bar X_n)=\sigma^2/n$。

> **弱大数定理(WLLN)**：如果$X_1,\dots, X_n$为独立同分布，那么$\bar X_n \xrightarrow[]{P} \mu$。

理解：当$n$越来越大时，$\bar X_n$的分布变得越来越聚集于$\mu$附近。

### 中心极限定理 (The Central Limit Theorem)

> **中心极限定理(CLT)**：如果$X_1,\dots,X_n$为独立同分布，那么

$$Z_n=\frac{\sqrt{n}(\bar X_n - \mu)}{\sigma} \rightsquigarrow Z$$

> 其中$Z \sim N(0,1)$，即正态分布。

理解：关于$\bar X_n$的概率表达式可以近似于正态分布。注意并不是随机变量本身近似于正态分布。

然而大多数时候我们并不知道$\sigma$，实际中我们可以用标准差$S_n^2=\frac1{n-1}\sum_{i=1}^n(X_i-\bar X_n)^2$来代替$\sigma$。

> **定理**：在与CLT相同的条件下，

$$\frac{\sqrt{n}(\bar X_n - \mu)}{S_n} \rightsquigarrow N(0,1)$$

### Delta方法 (The Delta Method)

为了能更加广泛有效的利用中心极限定理，掌握Delta方法是相当有必要的。

> **Delta方法**：

$$Y\approx N\left(\mu,\frac{\mu^2}{n}\right) \Rightarrow g(Y_n) \approx N\left(g(\mu),(g'(\mu))^2\frac{\sigma^2}n\right)$$

> 其中$g$是一个可导函数从而$g'(\mu)\ne0$。

P.S. 强大数定理，多元中心极限定理及多元Delta方法由于比较复杂就省略了。另外由于比较懒，所以有助于理解的例子也没用写，纯粹当是记录一下学习的过程了。
