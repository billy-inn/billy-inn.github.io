---
layout: post
title: "Notes on Convex Optimization (5): Newton's Method"
date: 2018-11-13 23:25:12 -0500
comments: true
categories: optimization
---

For $x\in\mathbf{dom}\ f$, the vector

$$\Delta x_{nt}=-\nabla^2 f(x)^{-1}\nabla f(x)$$

is called the *Newton step* (for $f$, at $x$).

#### Minimizer of second-order approximation

The second-order Taylor approximation $\hat f$ of $f$ at $x$ is 

\begin{equation}
\hat f(x+v) = f(x) + \nabla f(x)^T v + \frac12 v^T \nabla^2 f(x) v.
\tag{1} \label{eq:1}
\end{equation}

which is a convex quadratic function of $v$, and is minimized when $v=\Delta x_{nt}$. Thus, the Newton step $\Delta x_{nt}$ is what should be added to the point $x$ to minimize the second-order approximation of $f$ at $x$.

<!--more-->

#### Steepest descent direction in Hessian norm

The Newton step is also the steepest descent direction at $x$, for the quadratic norm defined by the Hessian $\nabla^2 f(x)$, *i.e.*,

$$\lVert u \rVert_{\nabla^2f(x)}=(u^T\nabla^2f(x)u)^{1/2}.$$

#### Solution of linearized optimality condition

If we linearize the optimality condition $\nabla f(x^*)=0$ near $x$ we obtain

$$\nabla f(x+v) \approx \nabla f(x) + \nabla^2f(x)v = 0$$

which is a linear equation in $v$, with solution $v=\Delta x_{nt}$. So the Newton step $\Delta x_{nt}$ is what must be added to $x$ so that the linearized optimality condition holds.

#### Affine invariance of the Newton step

An important feature of the Newton step is that it is independent of linear changes of coordinates. Suppose $T\in \mathbf{R}^{n \times n}$ is nonsingular, and define $\bar f(y)=f(Ty)$. Then we have

$$\begin{split}
\nabla\bar f(y) & = \nabla f(Ty)\\
&=\frac{\partial f(Ty)}{\partial(Ty)}\frac{\partial(Ty)}{y} \\
&=T^T\nabla f(x),
\end{split}$$

where $x=Ty$, likewise we have $\nabla^2 \bar f(y) = T^T\nabla^2f(x)T$. The Newton step for $\bar f$ at $y$ is therefore

$$\begin{split}
\Delta y_{nt} &= -(T^T\nabla^2f(x)T)^{-1}(T^T\nabla f(x)) \\
&= -T^{-1} \nabla^2 f(x)^{-1} \nabla f(x) \\
&= T^{-1}\Delta x_{nt},
\end{split}$$

where $\Delta x_{nt}$ is the Newton step for $f$ at $x$. Hence the Newton steps of $f$ and $\bar f$ are related by the same linear transformation, and

$$x + \Delta x_{nt} = T(y + \Delta y_{nt}).$$

#### The Newton decrement

The quantity

$$\lambda(x)=(\nabla f(x)^T \nabla^2 f(x)^{-1} \nabla f(x))^{1/2}$$

is called the *Newton decrement* at $x$. We can relate the Newton decrement to the quantity $f(x) - \inf_y \hat f(y)$, where $\hat y$ is the second-order approximation of $f$ at $x$:

$$f(x) - \inf_y \hat f(y)=f(x)-\hat f(x + \Delta x_{nt})=\frac12\lambda(x)^2.$$

We can also express the Newton decrement as

$$\lambda(x)=(\Delta x_{nt}^T \nabla^2 f(x) \Delta x_{nt})^{1/2}.$$

This shows that $\lambda$ is the norm of the Newton step, in the quadratic norm defined by the Hessian.

### Newton's Method

> *Newton's method*. \\
> **given** a starting point $x \in \mathbf{dom} \enspace f$, tolerance $\epsilon > 0$. \\
> **repeat** \\
> - Compute the Newton step $\Delta x_{nt}$ and decrement $\lambda^2$. \\
> - Stopping criterion. *quit** if $\lambda(x)^2/2 \le \epsilon$. \\
> - *Line search*. Choose a step size $t > 0$ by backtracking line search. \\
> - Update. $x := x+ t\Delta x_{nt}$.

### Summary

Newton's method has several very strong advantages over gradient and steepest descent methods:

- Convergence of Newton's method is rapid in general, and quadratic near $x^\ast$. Once the quadratic convergence phase is reached, at most six or so iterations are required to produce a solution of very high accuracy.
- Newton's method is affine invariant. It is insensitive to the choice of coordinates, or the condition number of the sublevel sets of the objective.
- The good performance of Newton's method is not dependent on the choice of algorithm parameters. In contrast, the choice of norm for steepest descent plays a critical role in its performance.

The main disadvantage of Newton's method is the cost of forming and storing the Hessian, and the cost of computing the Newton step, which requires solving a set of linear equations.
