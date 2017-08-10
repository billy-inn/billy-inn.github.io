---
layout: post
title: "统计释疑(2)：概率不等式有什么用？"
date: 2017-08-09 22:38:45 -0600
comments: true
categories: statistics
---

在学习概率论或者一些统计课程的时候，往往会学到一系列各式各样稀奇古怪的不等式 (Inequalities)，然而却对于这些不等式的意义缺乏一个直观的认识。引申*“All of Statistics"*一书中的一个小例子可以给出一个很切合实际的解释。

### 我的神经网络真的有效吗？

假如我们用神经网络在MNIST数据集上训练了一个分类器，我们在测试集上得到了一个错误率，比如$0.05$。那么这是否意味着我们可以保证我们的神经网络一定能达到$95\%$的正确率呢？显然训练一次得出的结果是不可靠的。那么，我们有多大的把握（概率）来相信这一观察到的错误率呢？

这时候就需要一些统计的语言了：假设我们有$n$个测试样本，每个测试样本分类的正确与否都是一个随机变量$X_1,\dots,X_n$。如果分类错误$X_i=1$，否则$X_i=0$。显而易见，$\bar X_n=n^{-1}\sum_{i=1}^nX_i$就是观察到的错误率。我们可以把每个$X_i$当做一个均值为$p$服从Bernoulli分布的随机变量，从而$p$就是真正（但是永远无法准确知晓）的错误率。从我们的角度来看，我们希望$\bar X_n$应该接近$p$。那么$\bar X_n$和$p$的概率超过一个固定值$\epsilon$的概率有多大呢？
这个概率就是$\mathbb{P}(\lvert\bar X_n -p\rvert > \epsilon)$，通常我们很难直接计算出它的值，这时我们就需要不等式来给这个概率设定一些边界 (bound)。

<!--more-->

### 尝试用不等式给出估计

我们的第一个不等式就是马尔科夫不等式 (Markov's inequality)：

> 令$X$为一个非负随机变量并假设$\mathbb{E}(X)$存在。对任何$t>0$，

$$\mathbb{P}(X>t) \le \frac{\mathbb{E}(X)}t。$$


咋一看，我们似乎无法直接运用马尔科夫不等式来限定$\mathbb{P}(\lvert\bar X_n -p\rvert > \epsilon)$的值。但其实只要稍做转换，便可得到另一个可以直接使用的不等式，即切比雪夫不等式 (Chebyshev's inequality)：

> 令$\mu = \mathbb{E}(X)$和$\sigma^2=\mathbb{V}(X)$，从而 

$$\mathbb{P}(\lvert X-\mu\rvert\ge t)\le\frac{\sigma^2}{t^2}。$$

这个不等式可以直接从马尔科夫不等式得出：

$$
\mathbb{P}(|X-\mu| \ge t)=\mathbb{P}(|X-\mu|^2\ge t^2)
\le\frac{\mathbb{E}(X-\mu)^2}{t^2}=\frac{\sigma^2}{t^2}。
$$

由于$X_i$服从Bernoulli分布，所以$\mathbb{V}(\bar X_n)=\mathbb{V}(X_i)/n=p(1-p)/n$，从而

$$\mathbb{P}(|\bar X_n -p|>\epsilon)\le\frac{\mathbb{V}(\bar X_n)}{\epsilon^2}=\frac{p(1-p)}{n\epsilon^2}\le\frac1{4n\epsilon^2}$$

注意对任意$0<p<1$，$p(1-p)\le\frac14$。如果我们希望神经网络的真实错误率与观察到的错误率之间的误差超过$\epsilon=0.05$的概率不超过$0.05$，那么通过简单的计算可得我们需要大约$n=2000$个测试样本。怎么样，是不是觉得不等式变得有用了？

### 一个更贴近的估计？

切比雪夫不等式只是一个相对粗略的估算，其实还有各种更为精确的不等式。当然，随之然来的是各种各样的限制条件，这里给出一个更精确的霍夫丁不等式 (Hoeffding's inequality)：

> 令$X_1\dots X_n \sim \mathrm{Bernoulli}(p)$，对任意$\epsilon>0$，

$$P(\lvert\bar X_n - p\rvert \ge \epsilon) \le 2e^{-2n\epsilon^2}$$ 

> 其中$\bar X_n = n^{-1}\sum_{i=1}^nX_i$。

通过上面的不等式，经过计算发现其实我们只需要$738$个测试样本就足够了。

P.S. 上面的Hoeffding's inequality只是针对Bernoulli变量的特殊形式，完整的不等式可以参考Wikipedia或相关教材。

### 小结

经过一个小例子，我们对不等式的作用有了一个直观的认识。但不等式真正的用武之地是在各种推导证明之中的，虽然我看到那种满篇公式、各种bound来bound去的paper都是自动略过的，而且现在在做的东西也是偏应用层面。但谁知道将来在研究中会不会经常用到呢，至少，现在我学会了估算可靠的测试样本大小的方法。
