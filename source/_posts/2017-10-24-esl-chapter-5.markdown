---
layout: post
title: "[Notes on Mathematics for ESL] Chapter 5: Basis Expansions and Regularization"
date: 2017-10-24 18:34:25 -0600
comments: true
categories: machine_learning
---

### 5.4 Smoothing Splines

#### Derivation of Equation (5.12)

Equal the derivative of **Equation (5.11)** as zero, we get

$$\frac{\partial\text{RSS}(\theta,\lambda)}{\partial\theta} = -2N^T(y-N\theta)+2\lambda\Omega_N\theta = 0$$

Put the terms related to $\theta$ on one side and the others on the other side, we get

$$(N^TN+\lambda\Omega_N)\theta = N^Ty$$

Multiply the inverse of $N^TN+\lambda\Omega_N$ on both sides completes the derivation of **Equation (5.12)**

$$\hat\theta = (N^TN+\lambda\Omega_N)^{-1}N^Ty$$

<!--more-->

#### Explanations on Equation (5.17) and (5.18)

It's a little confusing to get **Equation (5.18)** directly from **Equation (5.17)** and its original form **Equation (5.11)**. In order to give a clear explanation, here we give the proof of the equation,

$$\theta^T\Omega_N\theta=\mathbf{f}^TK\mathbf{f}.$$

which are the different terms between **Equation (5.11)** and **Equation (5.18)**.

We know that

$$\begin{split}
\mathbf{f}&=N(N^TN+\lambda\Omega_N)^{-1}N^Ty \\
&=S_{\lambda}y = N\theta
\end{split}$$

following **Equation (5.14)** in the book.

From **Equation (5.17)**, we can get

$$\begin{split}
K&=\frac1\lambda(S_\lambda^{-1}-I)\\
&=\frac1\lambda\left(N^{-T}(N^TN+\lambda\Omega_N)N^{-1}-I\right)\\
&=N^{-T}\Omega_NN^{-1}
\end{split}$$

Plug the above two equation into the right side of the equation remains to be proved, we get

$$\begin{split}
\mathbf{f}^TK\mathbf{f} &= \theta^TN^TN^{-T}\Omega_NN^{-1}N\theta \\
&=\theta^T\Omega_N\theta
\end{split}$$

which completes the proof.
