---
layout: post
title: "[Notes on Mathematics for ESL] Chapter 6: Kernel Smoothing Methods"
date: 2017-10-27 16:57:21 -0600
comments: true
categories: machine_learning 
---

### 6.1 One-Dimensional Kernel Smoothers

#### Notes on Local Linear Regression

Locally weighted regression solves a separate weighted least squares problem at each target point $x_0$:

$$\min_{\alpha(x_0),\beta(x_0)}\sum_{i=1}^NK_\lambda(x_0,x_i)[y-\alpha(x_0)-\beta(x_0)x_i]^2$$

The estimate is  $\hat f(x_0)=\hat\alpha(x_0)+\hat\beta(x_0)x_0$. Define the vector-value function $b(x)^T=(1,x)$. Let $\mathbf{B}$ be the $N \times 2$ regression matrix with $i$th row row $b(x_i)^T$, $\mathbf{W}(x_0)$ the $N\times N$ diagonal matrix with $i$th diagonal element $K_\lambda (x_0, x_i)$, and $\theta=(\alpha(x_0), \beta(x_0))^T$.

Then the above optimization problem can be rewritten as

$$\min_\theta(y-\mathbf{B}\theta)^T\mathbf{W}(x_0)(y-\mathbf{B}\theta)$$

Equal the derivative w.r.t $\theta$ as zero, we get

$$\begin{split}
&\mathbf{B}^T\mathbf{W}(x_0)(y-\mathbf{B}\hat\theta)=0 \\
&\mathbf{B}^T\mathbf{W}(x_0)\mathbf{B}\hat\theta = \mathbf{B}^T\mathbf{W}(x_0)y \\
&\hat\theta= (\mathbf{B}^T\mathbf{W}(x_0)\mathbf{B})^{-1}\mathbf{B}\mathbf{W}(x_0)y
\end{split}$$

<!--more-->

Then

$$\begin{split}
\hat f(x_0)&=b(x_0)^T\hat\theta \\
&=b(x_0)^T(\mathbf{B}^T\mathbf{W}(x_0)\mathbf{B})^{-1}\mathbf{B}\mathbf{W}(x_0)y \\
&=\sum_{i=1}^Nl_i(x_0)y_i
\end{split}$$

It's claimed that $\sum_{i=1}^Nl_i(x_0)=1$ and $\sum_{i=1}^N(x-x_0)l_i(x_0)=0$ in the book, so that the bias $\text{E}(\hat f(x_0))-f(x_0)$ depends only on quadratic and higher-order terms in the expansion of $f$. However, the proof is not given. Here I will give the detailed derivations of these two equations.

First, define the following terms:

$$\begin{split}
S_0 &= \sum_{i=1}^NK_\lambda(x_0, x_i) \\
S_1 &= \sum_{i=1}^NK_\lambda(x_0, x_i)x_i \\
S_2 &= \sum_{i=1}^NK_\lambda(x_0, x_i)x_i^2 \\
m_0 &= \sum_{i=1}^NK_\lambda(x_0, x_i)y_i \\
m_1 &= \sum_{i=1}^NK_\lambda(x_0, x_i)x_iy_i
\end{split}$$

Then, we can represent the estimate as

$$\begin{split}
\hat f(x_0) &= b(x_0)^T\begin{bmatrix}S_0& S_1\\S_1& S_2\end{bmatrix}^{-1}\begin{bmatrix}m_0\\m_1\end{bmatrix} \\
&= \frac1{S_0S_2-S_1^2}b(x_0)^T\begin{bmatrix}S_2 &-S_1\\-S_1& S_0\end{bmatrix}\begin{bmatrix}m_0\\m_1\end{bmatrix} \\
&=\frac{(S_2-S_1x_0)m_0-(S_1-S_0x_0)m_1}{S_0S_2-S_1^2}
\end{split}$$

When $y=\mathbf{1}$, $m_0=S_0$ and $m_1=S_1$, we get

$$\hat f(x_0)=\sum_{i=1}^Nl_i(x_0)=\frac{S_0S_2-S_1^2}{S_0S_2-S_1^2}=1$$

When $y=\mathbf{x}-x_0$, 

$$\begin{split}
\hat f(x_0) &= \sum_{i=1}^N(x_i-x_0)l_i(x_0) \\
&= \frac{(S_2-S_1x_0)(S_1-S_0x_0)-(S_1-S_0x_0)(S_2-S_1x_0)}{S_0S_2-S_1^2} \\
&= 0
\end{split}$$

More generally, it's easy to show that $\sum_{i=1}^N(x_i-x_0)^pl_i(x_0)=0$ when $p>0$.

We only prove the case when the input $x$ is one-dimensional. Similar strategy can be used to prove the case for high-dimensional input, but it'll be a little bit complicated if you're interested. Have fun!
