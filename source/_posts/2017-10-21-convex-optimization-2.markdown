---
layout: post
title: "Notes on Convex Optimization (2): Convex Functions"
date: 2017-10-21 11:59:09 -0600
comments: true
categories: optimization 
---
### 1. Basic Properties and Examples

#### 1.1 Definition

$f:\mathbb{R}^n \rightarrow \mathbb R$ is convex if $\mathbf{dom}\ f$ is a convex set and

$$f(\theta x+(1-\theta)y)\le\theta f(x)+(1-\theta)f(y)$$

for all $x,y\in \mathbf{dom}\ f, 0\le\theta\le1$

- $f$ is concave if $-f$ is convex
- $f$ is strictly convex if $\mathbf{dom}\ f$ is convex and $$f(\theta x+(1-\theta)y)<\theta f(x)+(1-\theta)f(y)$$ for $x,y\in\mathbf{dom}\ f,x\ne y, 0<\theta<1$

$f:\mathbb{R}^n \rightarrow \mathbb R$ is convex if and only if the function $g: \mathbb{R} \rightarrow \mathbb{R}$,

$$g(t)=f(x+tv),\quad\mathbf{dom}\ g=\{t\mid x+tv\in\mathbf{dom}\ f\}$$

is convex (in $t$) for any $x \in \mathbf{dom}\ f, v\in\mathbb R^n$ 

<!--more-->

#### 1.2 Extended-value extensions

extended-value extension $\tilde f$ of $f$ is 

$$\tilde f(x)=f(x),x\in\mathbf{dom}\ f; \tilde f(x)=\infty,x\ne \mathbf{dom}\ f$$

#### 1.3 First-order conditions

**1st-order condition**: differentiable $f$ with convex domain is convex iff

$$f(y)\ge f(x)+\nabla f(x)^T(y-x)\mathrm{\ for\ all\ } x,y\in\mathbf{dom}\ f$$

#### 1.4 Second-order conditions

**2nd-order conditions**: for twice differentiable $f$ with convex domain
- $f$ if convex if and only if
$$\nabla^2f(x)\succeq0\mathrm{\ for\ all\ } x\in\mathbf{dom}\ f$$
- if $\nabla^2f(x)\succ0$ for all $x\in\mathbf{dom}\ f$, then $f$ is strictly convex

#### 1.5 Sublevel sets and epigraph

$\alpha$**-sublevel set** of $f: \mathbb R^n \rightarrow \mathbb R$:

$$C_\alpha=\{x\in\mathbf{dom}\ f \mid f(x)\le\alpha\}$$

sublevel sets of convex functions are convex (converse if false)

If $f$ is concave, then its $\alpha$**-superlevel set**, given by $\{x\in\mathbf{dom}\ f\mid f(x)\le\alpha\}$, is a convex set

**epigraph** of $f:\mathbb R^n \rightarrow \mathbb R$:

$$\mathbf{epi}\ f=\{(x,t)\in\mathbb R^{n+1}\mid x\in\mathbf{dom}\ f,f(x)\le t\}$$

$f$ is convex if and only if $\mathbf{epi}\ f$ is a convex set

$f$ is concave if and only if its **hypograph**, defined as

$$\mathbf{hypo}\ f= \{(x,t)\in\mathbb R^{n+1}\mid x\in\mathbf{dom}\ f,f(x)\ge t\}$$

is a convex set

#### 1.6 Jensen's inequality and extensions

**Jensen's Inequality**: if $f$ is convex, then for $0\le\theta\le1$,

$$f(\theta x+(1-\theta)y)\le\theta f(x)+(1-\theta)f(y)$$

**extension**: if $f$ is convex, then

$$f(\mathbb E z)\le \mathbb Ef(z)$$

for any random variable $z$

### 2. Operations that Preserve Convexity

#### 2.1 Positive weighted sum & composition with affine function

**nonnegative multiple**: $\alpha f$ is convex if $f$ is convex, $\alpha \ge 0$

**sum**: $f_1+f_2$ convex if $f_1,f_2$ convex (extends to infinite sums, integrals)

**composition with affine function**: $f(Ax+b)$ is convex if $f$ is convex

#### 2.2 Pointwise maximum

**pointwise maximum**: if $f_1,\dots,f_m$ are convex, then $f(x)=\max\{f_1(x),\dots,f_m(x)\}$ is convex

**pointwise supermum**: if $f(x,y)$ is convex in $x$ for each $y\in\mathcal{A}$, then

$$g(x)=\sup_{y\in\mathcal{A}}f(x,y)$$

is convex

similarly, the **pointwise infimum** of a set of concave functions is a concave function

#### 2.3 Composition

**composition with scalar functions**: composition of $g: \mathbb R^n \rightarrow \mathbb R$ and $h: \mathbb R\rightarrow \mathbb R$:

$$f(x)=h(g(x))$$

$f$ is convex if $g$ convex, $h$ convex, $\tilde h$ nondecreasing; $g$ concave, $h$ convex, $\tilde h$ nonincreasing

Note: monotonicity must hold for extended-value extension $\tilde h$

**vector composition**: composition of $g:\mathbb R^n \rightarrow \mathbb R^k$ and $h:\mathbb R^k \rightarrow \mathbb R$:

$$f(x)=h(g(x))=h(g_1(x),g_2(x),\dots,g_k(x))$$

$f$ is convex if $g_i$ convex, $h$ convex, $\tilde h$ nondecreasing in each argument; $g$ concave, $h$ convex, $\tilde h$ nonincreasing in each argument

#### 2.4 Minimization

**minimization**: if $f(x,y)$ is convex in $(x,y)$ and $C$ is a convex set then

$$g(x)=\inf_{y\in C}f(x,y)$$

is convex

#### 2.5 Perspective of a function

**perspective**: the **perspective** of a function $f:\mathbb R^n \rightarrow \mathbb R$ is the function $g:\mathbb R^n \times \mathbb R \rightarrow \mathbb R$,

$$g(x,t)=tf(x/t),\mathbf{dom}\ g=\{(x,t)\mid x/t\in\mathbf{dom}\ f,t>0\}$$

$g$ is convex if $f$ is convex

### 3. The Conjugate Function

#### 3.1 Definition

the **conjugate** of a function $f$ is 

$$f^*(y)=\sup_{x\in\mathbf{dom}\ f}(y^Tx-f(x))$$

- $f^*$ is convex whether or not $f$ is convex

#### 3.2 Basic properties

**conjugate of the conjugate**: if $f$ is convex and closed, then $f^{**}=f$

**differentiable functions**: The conjugate of a differentiable function $f$ is also called the *Legendre transform* of $f$. Let $z\in\mathbb{R}^n$ be arbitrary and define $y=\nabla f(z)$, then we have

$$f^*(y)=z^T\nabla f(z)-f(z)$$

**scaling and composition with affline transformation**: 
For $a>0$ and $b\in\mathbb{R}$, the conjugate of $g(x)=af(x)+b$ is $g^\*(y)=af^\*(y/a)-b$. 

Suppose $A\in\mathbb{R}^{n\times n}$ is nonsingular and $b\in\mathbb{R}^n$. Then the conjugate of $g(x)=f(Ax+b)$ is

$$g^*(y)=f^*(A^{-T}y)-b^TA^{-T}y$$

with $\mathbf{dom}\ g^\*=A^T\mathbf{dom}\ f^\*$

**sums of independent functions**: if $f(u,v)=f_1(u)+f_2(v)$, where $f_1$ and $f_2$ are convex functions with conjugates $f_1^\*$ and $f_2^\*$, respectively, then

$$f^*(w,z)=f_1^*(w)+f_2^*(z)$$

### 4. Quasiconvex Functions

$f:\mathbb R^n\rightarrow \mathbb R$ is quasiconvex if $\mathbf{dom}\ f$ is convex and the sublevel sets

$$S_{\alpha}=\{x\in\mathbf{dom}\ f\mid f(x)\le\alpha\}$$

are convex for all $\alpha$

- $f$ is quasiconcave if $-f$ is quasiconvex
- $f$ is quasilinear if it is quasiconvex and quasiconcave
- convex functions are quasiconvex, but the converse is not true


**modified Jensen inequality**: for quasiconvex $f$

$$0\le\theta\le1\Longrightarrow f(\theta x+(1-\theta)y)\le\max\{f(x),f(y)\}$$

**first-order condition**: differentiable $f$ with convex domain is quasiconvex iff

$$f(y)\le f(x)\Longrightarrow\nabla f(x)^T(y-x)\le0$$

**operations that preserve quasiconvexity**:

- nonnegative weighted maximum
- composition
- minimization

**sum** of quasiconvex functions are not necessarily quasiconvex

### 5. Log-concave and Log-convex Functions

a positive function $f$ is log-concave if $\log f$ is concave:

$$f(\theta x+(1-\theta)y)\ge f(x)^\theta f(y)^{1-\theta}\mathrm{\ for\ }0\le\theta\le1$$

$f$ is log-convex if $\log f$ is convex

**properties of log-concave functions**:

- twice differentiable $f$ with convex domain is log-concave iff 

$$f(x)\nabla^2f(x)\preceq\nabla f(x)\nabla f(x)^T$$

for all $x\in\mathbf{dom}\ f$

- product of log-concave functions is log-concave
- sum of log-concave functions is not always log-concave; however, log-convexity is preserved under sums
- integration: if $f:\mathbb R^n\times\mathbb R^m \rightarrow \mathbb R$ is log-concave, then 

$$g(x)=\int f(x,y)dy$$

is log-concave

**consequences of integration property**:

- convolution $f*g$ of log-concave functions $f,g$ is log-concave 

$$(f*g)(x)=\int f(x-y)g(y)dy$$

- if $C\subseteq \mathbb R^n$ convex and $y$ is a random variable with log-concave pdf then 

$$f(x)=\mathbf{prob}(x+y\in C)$$ 

is log-concave

### 6. Convexity w.r.t. Generalized Inequalities

$f:\mathbb{R}^n\rightarrow\mathbb{R}^m$ is $K$-convex if $\mathbf{dom}\ f$ is convex and

$$f(\theta x+(1-\theta)y)\preceq_K\theta f(x)+(1-\theta)f(y)$$

for $x,y\in\mathbf{dom}\ f,0\le\theta\le1$
