---
layout: post
title: "Notes on Convex Optimization (3): Unconstrained Minimization Problems"
date: 2018-09-29 15:15:12 -0400
comments: true
categories: optimization
---

Unconstrained optimization problems are defined as follows:

\begin{equation}
\text{minimize}\quad f(x)
\tag{1} \label{eq:1}
\end{equation}

where $f: \mathbf{R}^n \rightarrow \mathbf{R}$ is convex and twice continously differentiable (which implies that $\mathbf{dom}\enspace f$ is open). We denote the optimal value $\inf_xf(x)=f(x^\ast)$, as $p^\ast$. Since $f$ is differentiable and convex, a necessary and sufficient condition for a point $x^\ast$ to be optimal is

\begin{equation}
\nabla f(x^\ast)=0
\tag{2} \label{eq:2}
\end{equation}

. Thus, solving the unconstrained minimization problem \eqref{eq:1} is the same as finding a solution of \eqref{eq:2}, which is a set of $n$ equations in the $n$ variables $x_1, \dots, x_n$. Usually, the problem must be solved by an iterative algorithm. By this we mean an algorithm that computes a sequence of points $x^{(0)}, x^{(1)}, \dots \in \mathbf{dom}\enspace f$ with $f(x^{(k)})\rightarrow p^\ast$ as $k\rightarrow\infty$. The algorithm is terminated when $f(x^{k}) - p^\ast \le \epsilon$, where $\epsilon>0$ is some specified tolerance.

#### Initial point and sublevel set

The starting point $x^{(0)}$ must lie in $\mathbf{dom}\enspace f$, and in addition the sublevel set

$$ S = \{x \in \mathbf{dom}\enspace f \vert f(x) \le f(x^{(0)})\} $$

must be closed. This condition is satisfied for all $x^{(0)}\in\mathbf{dom}\enspace f$ if the function $f$ is closed.

Note: 1) Continuous functions with $\mathbf{dom}\enspace f=\mathbf{R}^n$ are closed; 2) Another important class of closed functions are continuous functions with open domains.

### Examples

#### Quadratic minimization and least-squares

The general convex quadratic minimization problem has the form

$$\text{minimize}\quad (1/2)x^TPx+q^Tx+r, $$

where $P\in\mathbf{S}_+^n$, $q\in\mathbf{R}^n$, and $r\in\mathbf{R}$. This problem can be solved via the optimality conditions, $Px+q=0$, which is a set of linear equations.

One special case of the quadratic minimization problem that arises very frequently is the least-squares problem

$$\text{minimize}\quad \lVert Ax-b\rVert_2^2=x^T(A^TA)x-2(A^Tb)^T+b^Tb.$$

The optimality condition

$$A^TAx^\ast=A^Tb$$

are called the *normal equations* of the least-squares problem. 

#### Unconstrained geometric programming

$$\text{minimize}\quad f(x)=\log(\sum_{i=1}^m\exp(a_i^Tx+b_i))$$

#### Analytic center of linear inequalities

$$\text{minimize} f(x)=-\sum_{i=1}^m\log(b_i - a_i^Tx),$$

where the domain of $f$ is the open set

$$\mathbf{dom}\enspace f=\{x\vert a_i^Tx<b_i,i=1,\dots,m\}.$$

#### Analytic center of a linear matrix inequality

$$\text{minimize}\quad f(x)=\log\det F(x)^{-1}$$

where $F: \mathbf{R}^n\rightarrow\mathbf{S}^p$ is affine. Here the domain of $f$ is 

$$\mathbf{dom}\enspace f=\{x\vert F(x) \succ 0\}.$$

### Strong convexity and implications

The objective function is *strongly convex* on $S$, which means that there exists an $m>0$ such that 

\begin{equation}
\nabla^2f(x) \succeq mI
\tag{3} \label{eq:3}
\end{equation}

for all $x\in S$.  For $x, y \in S$ we have

$$f(y)=f(x)+\nabla f(x)^T(y-x) + \frac12(y-x)^T\nabla^2f(z)(y-x)$$

for some $z$ on the line segement $[x, y]$. By the strong convexity assumption \eqref{eq:3}, the last term on the righthand side is at least $(m/2)\lVert y-x\rVert^2_2$, so we have the inequality

\begin{equation}
f(y) \ge f(x) + \nabla f(x)^T(y-x) + \frac{m}2\lVert y-x \rVert_2^2
\tag{4} \label{eq:4}
\end{equation}

for all $x$ and $y$ in $S$.

#### Bound $f(x)-p^\ast$ in terms of $\lVert \nabla f(x) \rVert_2$

Setting the gradient of the righthand side of \eqref{eq:4} with respect to $y$ equal to zero, we find that $\tilde y = x-(1/m)\nabla f(x)$ minimizes the righthand side. Therefore we have

$$\begin{split}
f(y) &\ge f(x) + \nabla f(x)^T (y-x) + \frac{m}2\lVert y-x \rVert_2^2 \\
& \ge f(x) + \nabla f(x)^T(\tilde y - x) + \frac{m}2\lVert \tilde y - x \rVert_2^2 \\
& = f(x) - \frac1{2m}\lVert \nabla f(x)\rVert_2^2
\end{split}$$

Since this holds for any $y\in S$, we have

\begin{equation}
p^* \ge f(x) - \frac1{2m}\lVert \nabla f(x)\rVert_2^2
\tag{5} \label{eq:5}
\end{equation}

This inequality shows that if the gradient is small at a point, then the point is nearly optimal.

#### Bound $\lVert x-x^\ast\rVert_2^2$ in terms of $\lVert \nabla f(x) \rVert_2$

Apply \eqref{eq:4} with $y=x^\ast$ to obtain

$$\begin{split}
p^* = f(x^\ast)  & \ge f(x) + \nabla f(x)^T (x^\ast - x) + \frac{m}2\lVert x^\ast-x \rVert_2^2 \\
& \ge f(x) - \lVert \nabla f(x) \rVert_2 \lVert x^\ast - x \rVert_2 + \frac{m}2 \lVert x^\ast - x \rVert_2^2,
\end{split}$$

where we use the Cauchy-Schwarz inequality in the second inequality. Since $p^\ast \le f(x)$, we must have

$$-\lVert \nabla f(x) \rVert_2 \lVert x^\ast - x \rVert_2 + \frac{m}2 \lVert x^\ast - x \rVert_2^2 \le 0.$$

Therefore, we have

\begin{equation}
\lVert x - x^\ast \rVert_2 \le \frac2m\lVert \nabla f(x) \rVert_2.
\tag{6}\label{eq:6}
\end{equation}

#### Uniqueness of the optimal point $x^\ast$

If there are two optimal point $x^\ast_1, x^\ast_2$, according to \eqref{eq:6}, 

$$\lVert x_1^\ast - x_2^\ast \rVert \le \frac2m \lVert f(x_1^\ast) \rVert_2 = 0.$$

Hence, $x_1^\ast = x_2^\ast$, the optimal point $x^\ast$ is unique.

#### Upper bound on $\nabla^2f(x)$

There exists a  constant $M$ such that 

$$\nabla^2 f(x) \preceq MI$$

for all $x \in S$. This upper bound on the Hessian implies for any $x, y \in S$,

$$f(y) \le f(x) + \nabla f(x)^T (y-x) + \frac{M}2\lVert y-x \rVert_2^2,$$

minimizing each side over $y$ yields

$$p^\ast \le f(x) - \frac1{2M}\lVert \nabla f(x) \rVert_2^2.$$

#### Condition number of sublevel sets

The ratio $\kappa=M/m$ is an upper bound on the condition number of the matrix $\nabla^2 f(x)$, *i.e.*, the ratio of its largest eigenvalue to its smallest eigenvalue.

We define the *width* of a convex set $C \subseteq \mathbf{R}^n$, in the direction $q$, where $\lVert q \rVert_2 = 1$, as

$$W(C, q) = \sup_{z \in C} q^T z - \inf_{z\in C}q^Tz.$$

The *minimum width* and *maximum width* of $C$ are given by

$$W_{min}=\inf_{\lVert q\rVert_2=1}W(C,q), \qquad W_{max}=\sup_{\lVert q\rVert_2=1}W(C,q).$$

The *condition number* of the convex set $C$ is defined as

$$\mathbf{cond}(C)=\frac{W^2_{max}}{W^2_{min}}.$$

Suppose $f$ satisfies $mI \preceq \nabla^2 f(x) \preceq MI$ for all $x\in S$. The condition number of the $\alpha$-sublevel $C_\alpha=\{x \vert f(x) \le \alpha\}$, where $p^\ast < \alpha \le f(x^{(0)})$, is bounded by

$$\mathbf{cond}(C_\alpha) \le \frac Mm.$$

#### The strong convexity constants

It must be kept in mind that the constants $m$ and $M$ are known only in rare cases, so they cannot be used in a practical stopping criterion.
