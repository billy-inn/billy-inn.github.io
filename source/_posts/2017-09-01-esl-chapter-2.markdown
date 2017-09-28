---
layout: post
title: "[Notes on Mathematics for ESL] Chapter 2: Overview of Supervised Learning"
date: 2017-09-01 01:12:36 -0600
comments: true
categories: machine_learning
---

### 2.4 Statistical Decision Theory

#### Derivation of Equation (2.16)

The expected predicted error (EPE) under the squared error loss:

$$\mathrm{EPE}(\beta) = \int (y-x^T\beta)^2\Pr(dx, dy).$$

Taking derivatives with respect to $\beta$:

$$\begin{split}
\frac{\partial\mathrm{EFE}}{\partial\beta}&=-2\int(y-x^T\beta)x\Pr(dx, dy). \\
&= -2(E[yx]-E[xx^T\beta])
\end{split}$$

In order to minimize the EFE, we make derivatives equal zero which gives **Equation (2.16)**:

$$\beta=E[xx^T]^{-1}E[yx].$$

*Note: $x^T\beta$ is a scalar, and $\beta$ is a constant.*

<!--more-->

### 2.5 Local Methods in High Dimensions

#### Intuition on Equation (2.24)

There are $N$ $p$-dimensional data point $x_1,\dots, x_N$, that is, $N\times p$ dimensions in total. Let $r_i=\Vert x_i \Vert$. Without loss of generality, we assume that $A < r_1 < \dots < r_n < 1$. Let $U(A)$ be the region of all possible sampled data which meet the assumptation:

$$U(A) = \int_{A<r_1<\dots<r_n<1}dx_1\dots dx_N.$$

The goal is to find $A$ such that $U(A)=\frac12U(0)$. It turns out to be a integration problem on a $N \times p$ dimensional space.

With some mathematical techniques (which make me overwhelmed), we can get $U(A)=(1-A^p)^N$. Then $U(0)=1$. Solving $(1-A^p)^N=1/2$, we obtain **Equation (2.24)**:

$$A=\left(1-2^{-\frac1N}\right)^{\frac1p}.$$

#### Derivation of Equation (2.27) and (2.28)

The variation is over all training sets $\mathcal{T}$, and over all values of $y_0$, while keeping $x_0$ fixed. Note that $x_0$ and $y_0$ are chosen independently of $\mathcal{T}$ and so the expectations commute: 
$\mathrm{E}\_{y_0\vert x_0}\mathrm{E}\_{\mathcal{T}}=\mathrm{E}\_{\mathcal{T}}\mathrm{E}\_{y_0 \vert x_0}$.
Also $\mathrm{E}\_\mathcal{T}=\mathrm{E}\_\mathcal{X}\mathrm{E}\_{\mathcal{Y \vert X}}$.

In order to make the derivation more comprehensible, here lists some definitions:

$$\begin{split}
y_0 &= x_0^T\beta + \varepsilon \\
\hat y_0 &= x_0^T\beta + \sum_{i=1}^Nl_i(x_0)\varepsilon_i \\
\mathrm{E}_\mathcal{T}(\hat y_0) &= x_0^T\beta + \mathrm{E}_{\mathcal{T}}((X^TX)^{-1}Xx_0\varepsilon) \\
&= x_0^T\beta+x_0^T\mathrm{E}_\mathcal{X}((X^TX)^{-1}X^T\mathrm{E}_{\mathcal{Y|X}}\varepsilon) \\
&=x_0^T\beta
\end{split}
$$

$y_0-\hat y_0$ can be written as the sum of three terms:

$$(y_0-x_0^T\beta)-(\hat y_0-\mathrm{E}_\mathcal{T}(\hat y_0))-(\mathrm{E}_\mathcal{T}(\hat y_0)-x_0^T\beta)=U_1-U_2-U_3$$

Following above definitions, we have $U_1=\varepsilon$, $U_3=0$. In addition, clearly we have $\mathrm{E}_\mathcal{T}U_2=0$. When squaring $U_1-U_2-U_3$, we can eliminate all three cross terms and one squared terms $U_3^2$.

Following the definition of variance, we have: $\mathrm{E}\_{y_0\vert x_0}\mathrm{E}\_\mathcal{T}U_1^2=\mathrm{Var}(\varepsilon)=\sigma^2$ and $\mathrm{E}\_\mathcal{T}(\hat y_0 - \mathrm{E}\_\mathcal{T}\hat y_0)^2=\mathrm{Var}\_\mathcal{T}(\hat y_0)$. 

Since $U_2=\sum_{i=1}^Nl_i(x_0)\varepsilon_i$, we have $\mathrm{Var}\_\mathcal{T}(\hat y_0)=\mathrm{E}\_\mathcal{T}U_2^2$ as 

$$\mathrm{E}_\mathcal{T}(x_0^T(X_TX)^{-1}X^T\varepsilon\varepsilon^TX(X^TX)^{-1}x_0).$$

Since $\mathrm{E}\_\mathcal{T}\varepsilon\varepsilon^T=\sigma^2I_N$, this is equal to $\mathrm{E}\_\mathcal{T}x_0(X^TX)^{-1}x_0\sigma^2$. This completes the derivation of **Equation (2.27)**.

Under the conditions stated by the authors, $X^TX/N$ is then approximately equal to $\mathrm{Cov}(X)=\mathrm{Cov}(x_0)$. Applying $\mathrm{E}\_{x_0}$ to $\mathrm{E}\_\mathcal{T}x_0(X^TX)^{-1}x_0\sigma^2$, we obtain (approximately)

$$\begin{split}
\sigma^2\mathrm{E}_{x_0}(x_0^T\mathrm{Cov}(X)^{-1}x_0)/N &= \sigma^2\mathrm{E}_{x_0}(\mathrm{trace}(x_0^T\mathrm{Cov}(X)^{-1}x_0))/N \\
&= \sigma^2\mathrm{E}_{x_0}(\mathrm{trace}(\mathrm{Cov}(X)^{-1}x_0x_0^T))/N \\
&= \sigma^2\mathrm{trace}(\mathrm{Cov}(X)^{-1}\mathrm{C ov}(x_0))/N \\
&= \sigma^2\mathrm{trace}(I_p)/N \\
&= \sigma^2p/N.
\end{split}$$

This completes the derivation of **Equation (2.28)**.


#### References

- [Notes on The Elements of Statistical Learning (by John Weatherwax)](http://waxworksmath.com/Authors/G_M/Hastie/hastie.html)
