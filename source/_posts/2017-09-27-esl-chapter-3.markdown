---
layout: post
title: "[Notes on Mathematics for ESL] Chapter 3: Linear Regression Models and Least Squares"
date: 2017-09-27 19:30:12 -0600
comments: true
categories: machine_learning 
---

### 3.2 Linear Regression Models and Least Squares

#### Derivation of Equation (3.8)

The least squares estimate of $\beta$ is given by the book's **Equation (3.6)**

$$\hat\beta=(X^TX)^{-1}X^T\mathbf{y}.$$

From the [previous post](/blog/2017/09/01/esl-chapter-2/), we know that $\mathrm{E}(\mathbf{y})=X\beta$. As a result, we obtain

$$\mathrm{E}(\hat\beta)=(X^TX)^{-1}X^TX\beta=\beta.$$

Then, we get

$$\begin{split}
\hat\beta-\mathrm{E}(\hat\beta)&=(X^TX)^{-1}X^T(\mathbf{y}-X\beta) \\
&=(X^TX)^{-1}X^T\varepsilon.
\end{split}$$

The variance of $\hat \beta$ is computed as

$$\begin{split}
\mathrm{Var}(\hat\beta) &= \mathrm{E}[(\hat\beta-\mathrm{E}(\hat\beta)(\hat\beta-\mathrm{E}(\hat\beta))^T] \\
&= (X^TX)^{-1}X^T\mathrm{Var}(\varepsilon)X(X^TX)^{-1}.
\end{split}$$

If we assume that the entries of $\mathbf{y}$ are uncorrelated and all have the same variance of $\sigma^2$, then $\mathrm{Var}(\varepsilon)=\sigma^2I_N$ and the above equation becomes

$$\mathrm{Var}(\hat\beta)=(X^TX)^{-1}\sigma^2.$$

This completes the derivation of **Equation (3.8)**.

<!--more-->

#### Thoughts on Equation (3.12) and (3.13)

There are a lot concepts of statistics in this part. It's better to go through Chapter 6 and Chapter 10 in [*All of Statistics*](http://www.stat.cmu.edu/~larry/all-of-statistics/) to have a taste about hypothesis tests and confidence intervals.

From my own viewpoint, Z-score and F-statistic give a measure about whether the corresponding features are useful or not. They can be used within some feature selection methods. However, they're not very useful in practice. The perferred feature selection methods are discussed in **Section 3.3** in the book. 

#### Interpretations of Equation (3.20) and (3.22)

$$\begin{split}
\text{MSE}(\tilde\theta) &= \text{E}(\tilde\theta-\theta)^2 \\
&= \text{E}(\tilde\theta-\text{E}(\tilde\theta)+\text{E}(\tilde\theta)-\theta)^2 \\
&= \text{Var}(\tilde\theta)+2(\text{E}(\tilde\theta)-\text{E}(\tilde\theta))(\text{E}(\tilde\theta)-\theta)+(\text{E}(\tilde\theta)-\theta)^2 \\
&= \text{Var}(\tilde\theta)+(\text{E}(\tilde\theta)-\theta)^2
\end{split}$$

which completes the derivation of **Equation (3.20)**.

**Equation (3.22)** shows that the expected quadratic error can be broken down into two parts as

$$\text{E}(Y_0-\tilde f(x_0))^2=\sigma^2+\text{MSE}(\tilde f(x_0))$$

The first error component $\sigma^2$ is unrelated to what model is used to describe our data. It cannot be reduced for it exists in the true data generation process. The second source of error corresponding to ther term $\text{MSE}(\tilde f(x_0))$ represents the error in the model and is under control of us. By **Equation (3.20)**, the mean square error can be broken down into two terms: a model variance term and a model bias squared term. How to make these two terms as small as possible while considering the trade-offs between them is the central topic in the book.

#### Notes on Multiple Regression from Simple Univariate Regression

The first thing that comes to my mind when I read this section is that why we need this when we already have the ordinary least square (OLS) estimate of $\beta$:

$$\hat \beta = (X^TX)^{-1}X^TY.$$

It's because we want to study how to obtain orthogonal inputs instead of correlated inputs, since orthogonal inputs have some nice properties.

Following Algorithm 3.1, we can transform the correlated inputs $\mathbf{x}$ to the orthogonal inputs $\mathbf{z}$. Another view is that we form an orthogonal basis by performing the Gram-Schmidt orthogonilization procedure on $X$'s column vectors and obtain an orthogonal basis $\mathbf{z}_{i=1}^p$. With this basis, linear regression can be done simply as in the univariate case as shown in **Equation (3.28)**:

$$\hat \beta_p=\frac{\langle\mathbf{z}_p, \mathbf{y}\rangle}{\langle\mathbf{z}_p, \mathbf{z}_p\rangle}.$$

Following this equation, we can derive **Equation (3.29)**:

$$\begin{split}
\text{Var}(\hat\beta_p)&=\text{Var}\left(\frac{z_p^Ty}{\langle z_p, z_p \rangle}\right)=\frac{z_p^T\text{Var}(y)z_p}{\langle z_p, z_p\rangle^2}=\frac{z_p^T(\sigma^2I)z_p}{\langle z_p, z_p\rangle^2} \\
&=\frac{\sigma^2}{\langle z_p, z_p \rangle}.
\end{split}$$

We can write the Gram-Schmidt result in matrix form using the QR decomposition as 

$$X = QR.$$

In this decomposition $Q$ is a $N\times(p+1)$ matrix with orthonormal columns and $R$ is a $(p+1)\times(p+1)$ upper triangular matrix. In this representation, the OLS estimate for $\beta$ can be written as

$$
\begin{split}
\hat\beta &= (X^TX)^{-1}X^T\mathbf{y} \\
&= (R^TQ^TQR)^{-1}R^TQ^T\mathbf{y} \\
&= (R^TR)^{-1}R^TQ^T\mathbf{y} \\
&= R^{-1}R^{-T}R^TQ^T\mathbf{y} \\
&= R^{-1}Q^T\mathbf{y}
\end{split}
$$

which is **Equation (3.32)** in the book. Following this equation, the fitted value $\mathbf{\hat y}$ can be written as

$$\mathbf{\hat y}=X\hat\beta=QRR^{-1}Q^T\mathbf{y}=QQ^T\mathbf{y}$$

which is **Equation (3.33)** in the book.

### 3.4 Shrinkage Methods

#### Notes on Ridge Regression

If we compute the singular value decomposition (SVD) of the $N\times p$ centered data matrix $X$ as

$$X=UDV^T,$$

where $U$ is a $N \times p$ matrix with orthonormal columns that span the column space of $X$, $V$ is a $p \times p$ orthogonal matrix, and $D$ is a $p \times p$ diagonal matrix with elements $d_j$ ordered such that $d_1\ge d_2 \ge \dots \ge d_p \ge 0$. From this representation of $X$ we can derive a simple expression for $X^TX$:

$$X^TX=VDU^TUDV^T=VD^2V^T,$$

which is the **Equation (3.48)** in the book. Using this expression, we can compute the least squares fitted values as

$$\begin{split}
\hat y^{ls} = X\hat\beta^{ls} &= X(X^TX)^{-1}X^T\mathbf{y}\\
&= UDV^T(VD^2V^T)^{-1}VDU^T\mathbf{y} \\
&= UDV^T(V^{-T}D^{-2}V^{-1})VDU^T\mathbf{y} \\
&= UU^T\mathbf{y} \\
&= \sum_{j=1}^pu_j(u_j^T\mathbf{y})
\end{split}$$

which is the **Equation (3.46)** in the book. Similarly, we can find solutions for ridge regression as

$$\begin{split}
\hat y^{ridge}=X\hat \beta^{ridge}&=X(X^TX+\lambda I)^{-1}X^T\mathbf{y} \\
&= UDV^T(VD^2V^T+\lambda VV^T)^{-1}VDU^T\mathbf{y} \\
&= UD(D^2+\lambda I)^{-1}DU^T\mathbf{y} \\
&= \sum_{j=1}^pu_j\frac{d_j^2}{d_j^2+\lambda}u_j^T\mathbf{y}
\end{split}$$

which is the **Equation (3.47)** in the book. Since we can estimate the sample variance by $X^TX/N$, the variance of $\mathbf{z}_1$ can be derived as follows:

$$\begin{split}
\text{Var}(\mathbf{z}_1)=\text{Var}(Xv_1)&= (Xv_1)^T(Xv_1)/N\\
&= v_1^TVD^TU^TUDV^Tv_1/N \\
&= v_1^TVD^2V^Tv_1/N \\
&= \frac{d_1^2}N
\end{split}$$

which is the **Equation (3.49)** in the book. Note that $v_1$ is the first column of $V$ and $V$ is orthogonal, so that $V^Tv_1$ is $[1,0, \dots, 0]^T$.

#### Notes on degrees-of-freedom formula for LAR and Lasso

The degrees-of-freedom of the fitted vector $\mathbf{\hat y}=(\hat y_1, \dots, \hat y_N)$ is defined as 

$$\text{df}(\mathbf{\hat y})=\frac1{\sigma^2}\sum_{i=1}^N\text{Cov}(\hat y_i, y_i)$$

in the book. Also, it's claimed that $\text{df}(\mathbf{\hat y})$ is $k$ for ordinary least squares regression and $\text{tr}(\mathbf{S}_{\lambda})$ for ridge regresssion without proof in the book. Here, we'll derive these two expressions. First, we define $e_i$ as a $N$-element vector of all zeros with a one in the $i$th spot. It's easy to see that $\hat y_i=e_i^T\mathbf{\hat y}$ and $y_i=e_i^T\mathbf{y}$, so that

$$\text{Cov}(\hat y_i, y_i)=\text{Cov}(e_i^T\mathbf{\hat y}, e_i^T\mathbf{y})=e_i^T\text{Cov}(\mathbf{\hat y},\mathbf{y})e_i.$$

For OLS regression, we have $\mathbf{\hat y}=X(X^TX)^{-1}X^T\mathbf{y}$, so the above expression for $\text{Cov}(\mathbf{\hat y}, \mathbf{y})$ becomes

$$\text{Cov}(\mathbf{\hat y}, \mathbf{y})=X(X^TX)^{-1}X^T\text{Cov}(\mathbf{y}, \mathbf{y})=\sigma^2X(X^TX)^{-1}X^T.$$

Thus,

$$\text{Cov}(\hat y_i, y_i)=\sigma^2e_i^TX(X^TX)^{-1}X^Te_i=\sigma^2x_i^T(X^TX)^{-1}x_i$$

where $x_i=X^Te_i$ is the $i$th row of $X$ or $i$th sample's feature vector. According to the given formula, we get

$$\begin{split}
df(\mathbf{\hat y}) &= \sum_{i=1}^N x_i^T(X^TX)^{-1}x_i \\
&= \sum_{i=1}^N\text{tr}(x_i^T(X^TX)^{-1}x_i) \\
&= \sum_{i=1}^N\text{tr}(x_ix_i^T(X^TX)^{-1}) \\
&= \text{tr}\left(\left(\sum_{i=1}^Nx_ix_i^T\right)(X^TX)^{-1}\right).
\end{split}$$

If you're not familar the basic properties of trace, you can refer to [this page](https://en.wikipedia.org/wiki/Trace_(linear_algebra)#Properties). Note that 

$$\sum_{i=1}^Nx_ix_i^T=[x_1\ x_2\ \dots\ x_N]
\begin{bmatrix}
x_1^T \\
x_2^T \\
\vdots \\
x_N^T\end{bmatrix}=X^TX.
$$

Thus, when there are $k$ predictors we get

$$\text{df}(\mathbf{\hat y})=\text{tr}(I_{k\times k})=k,$$

the claimed result for OLS in the book. Similarly for ridge regression,

$$\text{Cov}(\mathbf{\hat y}, \mathbf{y})=X(X^TX+\lambda I)^{-1}X^T\text{Cov}(\mathbf{y}, \mathbf{y})=\sigma^2X(X^TX+\lambda I)^{-1}X^T.$$

$$\text{Cov}(\hat y_i, y_i)=\sigma^2e_i^TX(X^TX+\lambda I)^{-1}X^Te_i=\sigma^2x_i^T(X^TX+\lambda I)^{-1}x_i$$

$$\begin{split}
df(\mathbf{\hat y})
&= \sum_{i=1}^N\text{tr}(x_ix_i^T(X^TX+\lambda I)^{-1}) \\
&= \text{tr}(X^TX(X^TX+\lambda I)^{-1}) \\
&= \text{tr}(X(X^TX+\lambda I)^{-1}X^T),
\end{split}$$

which is the **Equation (3.50)** in the book.

### References

- [Notes on Mathematics for ESL: Chaper 2](/blog/2017/09/01/esl-chapter-2/)
- [Notes on The Elements of Statistical Learning (by John Weatherwax)](http://waxworksmath.com/Authors/G_M/Hastie/hastie.html)
- [All of Statistics (by Larry Wasserman)](http://www.stat.cmu.edu/~larry/all-of-statistics/)
