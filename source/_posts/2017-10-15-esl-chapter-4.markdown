---
layout: post
title: "[Notes on Mathematics for ESL] Chapter 4: Linear Methods for Classification"
date: 2017-10-15 14:30:27 -0600
comments: true
categories: machine_learning
---

### 4.3 Linear Discriminant Analysis

#### Derivation of Equation (4.9)

For that each class's density follows multivariate Gaussian

$$f_k(x) = \frac{1}{(2\pi)^{p/2}\lvert\Sigma\rvert^{1/2}}e^{-\frac12(x-\mu_k)^T\Sigma^{-1}(x-\mu_k)}$$

Take the logarithm of $f_k(x)$, we get

$$\begin{split}
\log f_k(x) &= c - \frac12(x-\mu_k)^T\Sigma^{-1}(x-\mu_k) \\
&= c - \frac12(x^T\Sigma^{-1}x-\mu_k^T\Sigma^{-1}x-x^T\Sigma^{-1}\mu_k+\mu_k\Sigma^{-1}\mu_k) \\
&= c - \frac12(x^T\Sigma^{-1}x+\mu_k\Sigma^{-1}\mu_k) + x^T\Sigma^{-1}\mu_k
\end{split}$$

where $c = -\log [(2\pi)^{p/2}\lvert\Sigma\rvert^{1/2}]$ and $\mu_k^T\Sigma^{-1}x=x^T\Sigma^{-1}\mu_k$. Following the above formula, we can derive **Equation (4.9)** easily

$$\begin{split}
\log\frac{\Pr(G=k|X=x)}{\Pr(G=k|X=x)} &=& \log\frac{f_k(x)}{f_l(x)} + \log\frac{\pi_k}{\pi_l} \\
&=& \log\frac{\pi_k}{\pi_l} - \frac12(\mu_k\Sigma^{-1}\mu_k-\mu_l\Sigma^{-1}\mu_l) \\&&+x^T\Sigma^{-1}(\mu_k-\mu_l) \\
&=& \log\frac{\pi_k}{\pi_l} - \frac12(\mu_k+\mu_l)\Sigma^{-1}(\mu_k-\mu_l) \\&&+x^T\Sigma^{-1}(\mu_k-\mu_l) \\
\end{split}$$

<!--more-->

#### Notes on Computations for LDA

It's stated in the book that the LDA classifier can be implemented by the following pair of steps:

- Sphere the data with respect to the common covariance estimate $\hat \Sigma:X^\*\leftarrow D^{-1/2}U^TX$, where $\hat \Sigma=UDU^T$. The common covariance estimate of $X^*$  will now be the indentity.
- Classify to the closest class centroid in the transformed space, modulo the effect of the class prior probabilities $\pi_k$.

However, detailed explanation is not given in the book. Here, I give some skipped mathematical steps which may help the understanding.

$$\begin{split}
\text{Var}(X^*)&=D^{-1/2}U^T\text{Var}(X)(D^{-1/2}U^T)^T \\
&= D^{-1/2}U^TUDU^TUD^{-1/2} \\
&= D^{-1/2}DD^{-1/2} \\
&= I,
\end{split}$$

which shows that the covariance estimate of $X^*$ is the identity.

Note that the classification for LDA is based on the linear discriminat functions

$$\delta_k(x)=x^T\Sigma^{-1}\mu_k-\frac12\mu_k^T\Sigma^{-1}\mu_k+\log\pi_k$$

which is the **Equation (4.10)** in the book. Since the input $x$ is same for each class, so we can add back a term $\frac12x^T\Sigma^{-1}x$ which is cancelled in the previous derivation. Now the functions are turned into:

$$\begin{split}
\delta_k(x)&=-\frac12(x^T\Sigma^{-1}x-2x^T\Sigma^{-1}\mu_k+\mu_k^T\Sigma^{-1}\mu_k)+\log\pi_k \\
&= -\frac12(x-\mu_k)^T\Sigma^{-1}(x-\mu_k) + \log\pi_k
\end{split}$$

We know that $\Sigma=I$ in the transformed space, so $\delta_k(x)=-1/2\lVert x-\mu_k\rVert_2+\log\pi_k$. And $\mu_k$ is the centroid for the $k$th class. The claimed method to classify is proved.

### 4.4 Logistic Regression

#### Derivation of Equation (4.21) and (4.22)

In the two-class case, $p_1(x;\beta)=p(x;\beta)$ and  $p_2(x;\beta) = 1-p(x;\beta)$ where 

$$p(x;\beta)=\frac{e^{\beta^Tx}}{1+e^{\beta^Tx}}.$$

The **Equation (4.21)** can be derived easily as follows,

$$\begin{split}
\frac{\partial l(\beta)}{\partial \beta} &= \frac{\partial}{\partial\beta}\sum_{i=1}^N\left\{y_i\beta^Tx_i-\log(1+e^{\beta^Tx_i})\right\}\\
&= \sum_{i=1}^N(y_ix_i-\frac{x_ie^{\beta^Tx_i}}{1+e^{\beta^Tx_i}}) \\
&= \sum_{i=1}x_i(y_i-p(x_i;\beta))
\end{split}$$

Note that

$$\frac{\partial p(x;\beta)}{\partial\beta}=xp(x;\beta)(1-p(x;\beta)).$$

Plug it into **Equation (4.21)**, we get 

$$\frac{\partial^2l(\beta)}{\partial\beta\partial\beta^T} = -\sum_{i=1}^Nx_ix_i^Tp(x_i;\beta)(1-p(x_i;\beta)).
$$
