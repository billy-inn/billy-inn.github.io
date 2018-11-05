---
layout: post
title: "Notes on Convex Optimization (4): Gradient Descent Method"
date: 2018-11-05 00:29:05 -0500
comments: true
categories: optimization
---

### Descent methods

$$x^{(k+1)}=x^{(k)} + t^{(k)}\Delta x^{(k)}$$

- $f(x^{(k+1)}) < f(x^{(k)})$
- $\Delta x$ is the *step* or *search direction*; $t$ is the *step size* or *step length*
- from convexity, $\nabla f(x)^T \Delta x <0$

> *General descent method*. \\
> **given** a starting point $x \in \mathbf{dom} \enspace f$. \\
> **repeat** \\
> - Determine a descent direction $\Delta x$. \\
> - *Line search*. Choose a step size $t > 0$. \\
> - Update. $x := x+ t\Delta x$.
> 
> **until** stopping criterion is satisfied

<!--more-->

#### Exact line search

$$t = \text{argmin}_{t > 0} \enspace f(x + t\Delta x)$$

#### Backtracking line search

> *Backtracking line search*. \\
> **given** a descent direction $\Delta x$ for $f$ at $x \in \mathbf{dom} f, \alpha \in(0,0.5), \beta\in(0,1)$. \\
> **starting** at $t:=1$. \\
> **while** $f(x+t\Delta x) > f(x) + \alpha t \nabla f(x)^T \Delta x$, $t:=\beta t$

### Gradient descent method

A natural choice for the search direction is the negative gradient $\Delta x = - \nabla f(x)$.

#### Convergence analysis for exact line search

We must have $f(x^(k)) - p^\ast \le \epsilon$ after at most

$$\frac{\log((f(x^{(0)})-p^\ast)/\epsilon)}{\log(1/c)}$$

iterations of the gradient method with exact line search, where $c=1-m/M<1$.

#### Convergence analysis for backtracking line search

Similar to exact line search, except that $c=1 - \min\{2m\alpha, 2\beta\alpha m/M\} < 1.$

#### Conclusions

- The gradient method often exhibits approximately linear convergence, *i.e.*, the error $f(x^{(k)}) - p^\ast$ converges to zeros approximately as a geometric series.
- The choice of backtracking parameters $\alpha, \beta$ has a noticeable but not dramatic effect on the convergence. An exact line search sometimes improves the convergence of the gradient method, but the effect is not large.
- The convergence rate depends greatly on the condition number of the Hessian, or the sublevel sets. Convergence can be very slow, even for problems that are moderately well conditioned. When the condition number is larger the gradient method is so slow that it is useless in practice.

### Steepest descent method

The first-order Taylor approximation of $f(x+v)$ around $x$ is

$$f(x+v)\approx \hat f(x+v)=f(x) + \nabla f(x)^T v.$$

The second term on the righthand side, $\nabla f(x)^T v$, is the *directional derivative* of $f$ at $x$ in the direction $v$. It gives the approximate change in $f$ for a small step $v$. The step $v$ is a descent direction if the directional derivative is negative.

Let $\lVert \cdot \rVert$ be any norm on $\mathbf{R}^n$. We define a *normailzied steepest descent direction* as 

\begin{equation}
\Delta x_{nsd} = \arg\min\{\nabla f(x)^T v\ \vert\ \lVert v \rVert = 1\}.
\tag{1}\label{eq:1}
\end{equation}

It is also convenient to consider a steepest descent step $\Delta x_{sd}$ that is *unnormalized*, by scaling the normalized steepest descent direction in a particular way:

\begin{equation}
\Delta x_{sd} = \lVert \nabla f(x) \rVert_\ast \Delta x_{nsd},
\tag{2}\label{eq:2}
\end{equation}

where $\lVert \cdot \rVert_\ast$ denotes the dual norm. Note that for the steepest descent step, we have

$$
\nabla f(x)^T \Delta x_{sd} = \lVert \nabla f(x) \rVert_\ast \nabla f(x)^T \nabla x_{nsd}=-\lVert \nabla f(x) \rVert_\ast^2.
$$

#### Steepest descent for Euclidean norm

To simplify the notation, we can look at the problem of solving $\min_v\{u^Tv\ \lvert\ \lVert v \rVert \le 1\}$ which ends up being equivalent to find the normalized steepest descent step.

The Cauchy-Schwarz inequality gives $\lvert u^Tv\rvert \le \rVert u \rVert \lVert v \rVert$, hence it is easy to see that the minimum is $\min_v\{u^Tv\ \lvert\ \lVert v \rVert \le 1\}=-\lVert u \rVert$, and the minimizer is $v=-u/\lVert u \rVert$. As a result, the steepest descent direction is simply the negative gradient, *i.e.*, $\Delta x_{sd} = - \nabla f(x)$.

#### Steepest descent for quadratic norm

We consider the quadratic norm

$$\lVert z \rVert_P = (z^TPz)^{1/2}=\lVert P^{1/2}z\rVert_2,$$

where $P \in \mathbf{S}\_{++}^n$. The problem is now $\min_v\{u^Tv\ \vert\ \lVert P^{1/2}v\rVert\le1\}=\min_v\{u^Tv\ \vert\ \lVert\delta\rVert\le1, v=P^{-1/2}\delta\}$.
This is equivalent to $\min_\delta\{((P^{-1/2})^Tu)^T\delta\ \vert\ \lVert\delta\rVert\le1\}$. The problem above shows that the minimum is $-\lVert (P^{-1/2})^Tu\rVert$ while the maximum $\lVert (P^{-1/2})^Tu\rVert$ is the dual norm according to the definition, and the minimizer is $v=P^{-1/2}\delta=-P^{-1}u/\lVert (P^{-1/2})^Tu\rVert$, so the steepest descent desnt is given by

$$\Delta x_{sd} = -P^{-1} \nabla f(x).$$

In addition, the steepest descent method in the quadratic norm $\lVert \cdot \rVert_P$ can be thought of as the gradient method applied to the problem after the change of coordinates $\bar x=P^{1/2}x$.

#### Steepest descent for $l_1$-norm

Let $i$ be any index for which $\lVert \nabla f(x) \rVert\_\infty = \lvert (\nabla f(x))\_i \rvert$. Then a normalized steepest descent direction $\nabla x\_{nsd}$ for the $l_1$-norm is given by

$$\Delta x_{nsd}=-\text{sign}\left(\frac{\partial f(x)}{\partial x_i}\right)e_i,$$

where $e_i$ is the $i$th standard basis vector. An unnormalized steepest descent step is then

$$\Delta x_{sd} = \Delta x_{nsd}\lVert \nabla f(x) \rVert_\infty = - \frac{\partial f(x)}{\partial x_i}e_i.$$

The steepest descent algorithm in the $l_1$-norm has a very natural interpertation: At each iteration we select a component of $\nabla f(x)$ with maximum absolute value, and then decrease or increase the corresponding component of $x$, according to the sign of $(\nabla f(x))_i$. The algorithm is sometimes called a *corrdinate-descent* algorithm, since only one component of the variable $x$ is updated at each iteration.

