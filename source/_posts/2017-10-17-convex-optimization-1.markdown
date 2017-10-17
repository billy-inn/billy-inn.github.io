---
layout: post
title: "Notes on Convex Optimization (1): Convex sets"
date: 2017-10-17 00:22:23 -0600
comments: true
categories: optimization 
---

### 1. Affine and Convex Sets

Suppose $x_1\ne x_2$ are two points in $\mathbb{R}^n$.

#### 1.1 Affine sets

**line** through $x_1$, $x_2$: all points

$$x=\theta x_1 + (1-\theta)x_2\quad(\theta \in \mathbb{R})$$

**affine set**: contains the line through any two distinct points in the set

$$x_1,x_2\in C,\ \theta\in\mathbb{R} \Longrightarrow \theta x_1 + (1-\theta)x_2 \in C$$

<!--more-->

#### 1.2 Convex sets

**line segment** between $x_1$ and $x_2$: all points 

$$x=\theta x_1 + (1-\theta)x_2$$

with $0\leq\theta\leq1$

**convex set**: contains line segment between any two points in the set

$$x_1,x_2\in C,\ 0\leq\theta\leq1 \Longrightarrow \theta x_1 + (1-\theta)x_2 \in C$$

**convex combination** of $x_1,\dots,x_k$: any point $x$ of the form

$$x=\theta_1x_1+\theta_2x_2+\dots+\theta_kx_k$$

with $\theta_1+\dots+\theta_k=1,\theta_i \geq 0$

**convex hull** of a set $C$, denoted $\mathbf{conv}\ C$: set of all convex combinations of points in $C$

#### 1.3 Cones

**conic combination** of $x_1$ and $x_2$: any point of the form

$$x=\theta_1x_1+\theta_2x_2$$

with $\theta_1 \geq 0, \theta_2 \geq 0$

**convex cone**: set that contains all conic combinations of points in the set

$$x_1,x_2\in C,\ \theta_1\ge0, \theta_2\ge0 \Longrightarrow \theta_1 x_1 + \theta_2x_2 \in C$$

### 2. Some Important Examples

#### 2.1 Hyperplanes and halfspaces

**hyperplane**: set of the form \{$x\mid a^Tx=b$}$(a\ne0)$

**halfspace**: set of the form \{$x\mid a^Tx\leq b$}$(a\ne0)$

- $a$ is the normal vector
- hyperplanes are affine and convex; halfspaces are convex

#### 2.2 Euclidean balls and ellipsoids

**(Euclidean) ball** with center $x_c$ and radius $r$:

$$B(x_c,r)=\{x\mid\lVert x-x_c\rVert_2\leq r\}=\{x_c+ru \mid\lVert u \rVert_2 \leq 1 \}$$

**ellipsoid**: set of the form

$$\{x \mid (x-x_c)^TP^{-1}(x-x_c)\leq 1\}$$

with $P\in \mathbf{S}^n_{++}$ (*i.e.*, P symmetric positive definite)

another representation: \{$x_c+Au\mid \lVert u\rVert_2\le1$} with $A$ square and nonsingular

- Euclidean balls and ellipsoids are all convex.

#### 2.3 Norm balls and norm cones

**norm**: a funtion $\lVert \centerdot \rVert$ that satisfies

- $\lVert x \rVert \geq 0$; $\lVert x \rVert=0$ if and only if $x=0$
- $\lVert tx \rVert = \lvert t \rvert \lVert x \rVert$ for $t\in \mathbb{R}$
- $\lVert x+y\rVert \leq \lVert x \rVert+\lVert y \rVert$

**norm ball** with center $x_c$ and radius $$r: \{x \mid \lVert x-x_c \rVert \leq r\}$$

**norm cone**: $$\{(x,t) \mid \lVert x \rVert \leq t\}$$

- norm balls and cones are convex
- norm cores (as the name suggest) are convex cones

#### 2.4 Polyhedra

**polyhedra**: solution set of finitely many linear inequalities and equalities

$$Ax \preceq b, \quad Cx=d$$

($A\in \mathbb{R}^{m\times n}$, $C\in\mathbb{R}^{p\times n}$, $\preceq$ is componentwise inequality)

- polyhedron is intersection of finite number of halfspaces and hyperplances

#### 2.5 The positive semidefinite cone

**positive semidefinite cone**:

- $\mathbf{S}^n$ is set of symmetric $n\times n$ matrices
- $$\mathbf{S}^n_+=\{X\in\mathbf{S}^n\mid X\succeq0\}$$: positive semidefinite $n\times n$ matrices $$X\in\mathbf{S}^n_+ \iff z^TXz \geq 0\ \mathrm{for\ all\ }z$$ $\mathbf{S}^n_+$ is a convex cone
- $$\mathbf{S}^n_{++}=\{X\in\mathbf{S}^n\mid X\succ0\}$$: positive definite $n\times n$ matrices

### 3. Operations that preserve convexity

**intersection**: the interction of (any number of) convex sets is convex

**affine function**: suppose $f: \mathbb{R}^n \rightarrow \mathbb{R}^m$ is affine ($f(x)=Ax+b$ with $A\in\mathbb{R}^{m\times n}, b\in\mathbb{R}^m$)

- the image of a convex set under $f$ is convex 

$$S \subseteq \mathbb{R}^n\ convex \Longrightarrow f(S)=\{f(x)\mid x\in S\}\ convex$$

- the inverse image $f^{-1}(C)$ of a convex set under $f$ is convex 

$$C \subseteq \mathbb{R}^m\ convex \Longrightarrow f^{-1}(C)=\{x\in\mathbb{R}^n\mid f(x)\in C\}\ convex$$

**perspective function** $P: \mathbb{R}^{n+1} \rightarrow \mathbb{R}^n$:

$$P(x,t)=x/t, \quad \mathbf{dom}\ P=\{(x,t)\mid t>0\}$$

images and inverse images of convex sets under perspective are convex

**linear-fractional function** $f:\mathbb{R}^n \rightarrow \mathbb{R}^m$:

$$f(x)=\frac{Ax+b}{c^Tx+d}, \quad \mathbf{dom}\ f=\{x\mid c^Tx+d>0\}$$

images and inverse images of convex sets under linear-fractional functions are convex

### 4. Generalized Inequalities

#### 4.1 Proper cones and generalized inequalities

a convex cone $K\subseteq\mathbb{R}^n$ is a **proper cone** if 

- $K$ is closed (contains its boundary)
- $K$ is solid (has nonempty interior)
- $K$ is pointed (contains no line)

**generalized inequality** defined by a proper cone $K$:

$$\begin{split}
x \preceq_K y &\iff y-x \in K\\
x \prec_K y &\iff y-x \in \mathbf{int}\ K
\end{split}$$

#### 4.2 Minimum and minimal elements

$x\in S$ is **the minimum element** of $S$ with respect to $\preceq_K$ if

$$y \in S \Longrightarrow x \preceq_K y$$

$x\in S$ is **a minimal element** of $S$ with respect to $\preceq_K$ if 

$$y \in S, y \preceq_K x \Longrightarrow y=x$$

### 5. Separating and Supporting Hyperplanes

**separating hyperplane theorem**: if $C$ and $D$ are disjoint convex sets, then there exists $a\ne0$, $b$ such that

$$a^Tx \le b\ \mathrm{for}\ x\in C,\quad a^Tx\ge b\ \mathrm{for}\ x\in D$$

**supporting hyperplane** to set $C$ at boundary point $x_0$:

$$\{x\mid a^Tx=a^Tx_0\}$$

where $a\ne0$ and $a^Tx\le a^Tx_0$ for all $x\in C$

**supporting hyperplance theorem**: if $C$ is convex, then there exists a supporting hyperplane at every boundary point of $C$

### 6. Dual Cones and Generalized Inequalities

#### 6.1 Dual cones

**dual cone** of a cone $K$:

$$K^*=\{y\mid y^T x \ge 0\mathrm{\ for\ all\ } x\in K\}$$

Dual cons satisfy several properties, such as:

- $K^*$ is closed and convex
- $K_1 \subseteq K_2$ imples $K_2^* \subseteq K_1^*$
- $K^{\**}$ is the closure of the convex hull of $K$ (Hence if $K$ is convex and closed, $K^{**}=K$)

Thsese properties show that if $K$ is a proper cone, then so is its dual $K^{*}$, and moreover, that $K^{**}=K$

#### 6.2 Dual generalized inequalities

dual cones of proper cones are proper, hence define generalized inequalities:

$$y\succeq_{K^*}0 \iff y^Tx\ge0\mathrm{\ for\ all\ } x\succeq_K0$$

Some import properties relating a generalized inequality and its dual are:

- $x\preceq_K y$ iff $\lambda^Tx \le \lambda^Ty$ for all $\lambda \succeq_{K^{*}} 0$
- $x\prec_K y$ iff $\lambda^Tx < \lambda^Ty$ for all $\lambda \succ_{K^{*}} 0, \lambda\ne0$

Since $K=K^{\*\*}$, the dual generalized inequality associated with $\preceq_{K^{*}}$ is $\preceq_K$, so these properties hold if the generalized inequality and its dual are swapped

#### 6.3 Minimum and minimal elements via dual inequalities

**dual characterization of minimum element** w.r.t. $\preceq_K$: $X$ is minimum element of $S$ iff for all $\lambda \succ_{K^*}0$, $x$ is the unique minimizer of $\lambda^Tz$ over $z\in S$

**dual characterization of minimal element** w.r.t. $\preceq_K$:

- if $x$ minimizes $\lambda^Tz$ over $S$ for some $\lambda \succ_{K^*}0$, then $x$ is minimal
- if $x$ is a minimal element of a convex set $S$, then there exists a nonzero $\lambda \succeq_{K^*}0$ such that $x$ minimizes $\lambda^Tz$ over $z \in S$
