---
title: Machine Learning
date: 2021-09-01 15:14:11
categories:
- R
- Feature Engineering
tags:
- Machine Learning
- Statistics
- R
mathjax: true
---
# Theorical Background

+ Types of Machine Learning
  + Supervised Learning
  + Unsupervised Learning
  + Reinforcement Learning
  + Self Learning
  + Feature Learning
  + Sparse Dictionary Learning
  + Anomaly Detection
  + Association Rules
+ Two Supervised Learning Methods
  + Regression
  + Classification
+ Empirical Risk Minimization
  + Loss and Risk Functions
  + Algorithms

<!-- More -->

## Supervised Learning

> A problem of inferring, estimating or learning a function $f$ for explaining $y$ based on $f(x)$

+ $y\in \mathcal{Y}$: Output (Dependent, Response Variable or Label)
+ $x\in \mathcal{X}$: Input (Independent, Predictive Variable of Feature)
+ $f\in \mathcal{F}$: $\mathcal{X}\rightarrow \mathcal{Y}$: Model (Regression Function or Hypothesis, Machine)

> c.f., Unsupervised Learning

## Regression & Classification

+ Regression
  + $\mathcal{Y}$: Infinite and Ordered ($\mathcal{Y}=\mathbb{R},\mathbb{R}^+,\mathbb{N}\cup\{0\},...$)
  + Linear Regression: $\mathcal{Y}=\mathbb{R}$
  + Poisson Regression: $\mathcal{Y}=\mathbb{N}\cup\{0\}$
+ Classification
  + $\mathcal{Y}$: Finite and Unordered ($\mathcal{Y}=\{0,1\},\{-1,1\},\{1,...,k\},...$)
  + Logistic Regression: $\mathcal{Y}=\{0,1\}$
  + Support Vector Machine: $\mathcal{Y}=\{-1,1\}$
  + Multinomial Regression: $\mathcal{Y}=\{1,...,k\}$
+ Prediction Based on $x$
  + Regression: $y_x=f(x)$
  + Classification: $y_x=\phi(x)$
    + $\phi(x)$: Classifier as a Function of $f(x)$
    + e.g., $\phi(x)=sign(f(x))$

## Loss, Risk and Empirical Risk Minimization

+ Loss (Cost) Function: $L(y,f(x))$
  + It measures `loss` or `cost` for the use of $f$
  + Regression: $y\in \mathbb{R}$
    + Square: $(y-f(x))^2$
    + Quantile: $\rho_\tau(y-f(x)), 0<\tau<1$
    + Huber: $H_\delta(y-f(x)), \delta>0$
  + Classification: $y\in {-1,1}$
    + Zero-One: $I[y\neq\phi]=I[yf(x)<0]$
    + Logistic: $log\{1+exp(-yf(x))\}$
    + Exponential: $exp(-yf(x))$
    + Hinge: $max\{0,1-yf(x)\}$
    + $\psi$: $I[yf(x)\leq0]+max\{0,1-yf(x)\}I[yf(x)>0]$
+ Risk Function: $R(f)=E_{(y,x)}L(y,f(x))$
  + Long-Term average of losses or costs
    + Square Loss: $E(y-f(x))^2$
    + Zero-One Loss: $EI[y\neq \phi(x)]=P[y\neq \phi(x)]$
    + Condition Risk: $R(f)=E_{y|x}[L(y,f(x))|x]$
+ Empirical Risk Minimization: $\hat f=argmin_{f\in \mathcal{F}}R_n(f)$
  + Empirical Risk Function: $R_n(f)=\Sigma^n_{i=1}L(y_i,f(x_i))/n$
    + Training Sample ($y_i,x_i$), $i\leq n$: Independent samples / observations of $(y,x)$
    + Linear Regression with Square Loss: $\hat \beta =argmin_\beta\Sigma^n_{i=1}(y_i-x^T_i\beta)^2/n$
    + Logistic Regression with Logistic Loss: $\hat\beta=argmin_\beta\Sigma^n_{i=1}\{-y_ix^T_i\beta+log(1+exp(x^T_i\beta))\}/n$

***

# Iterative Algorithms

+ Univariate Function Minimization
  + Iterative Grid Search Algorithm
  + Golden Section Algorithm
+ Multivariate Function Minimization
  + Coordinate Descent Algorithm
  + Gradient Descent Algorithm

## Univariate Function Minimization

+ Problem: find $x^*=argmin_{x\in[a,b]}f(x)$
+ Iterative Algorithm: for $n=1,2,...$
  + $x^*\in[a_{n+1},b_{n+1}]\subset[a_n,b_n]$
+ (Lemma) $f$: convex on $[a_n,b_n]$
  + $
\begin{equation}
\left.
\begin{gathered}x^*\in[a_n,b_n]\newline \exists_C\in[a_{n+1},b_{n+1}]\subset[a_n,n_n]\newline s.t.\ \ f(a_{n+1})>f(c)<f(b_{n+1})
\end{gathered}
\right\rbrace\rightarrow x^\ast [a_{n+1},b_{n+1}] \notag
\end{equation}
$

### Grid Search

+ Non-Iterative Grid Search Alhorithm: $x^*\approx argmin_{z\in z_k=a+k(b-a)/m|k=0,...,m}f(z)$
+ Iterative Grid Search Algorithm: for $n=1,2,...$
  + $
\begin{equation}
\left\lbrace
\begin{gathered}
a_{n+1}=a_n+(k_n-1)(b_n-a_n)/m \newline
b_{n+1}=a_n+(k_n+1)(b_n-a_n)/m
\end{gathered}
\right. \notag
\end{equation}
$
  + $k_n=argmin_{k\in\{0,...,m\}}f(a_n+k(b_n-a_n)/m)$

### Golden Section Algorithm

+ Golden Section Algorithm: for $n=1,2,...$
  + Two inner points
    + $
\begin{equation}
\left.
\begin{gathered}
c_n=\gamma a_n+(1-\gamma)b_n \newline
d_n=\gamma b_n+(1-\gamma)a_n
\end{gathered}
\right. \notag
\end{equation}
$
    + Golden Ratio: $\gamma=(\sqrt{5}-1)/2\approx0.618034$
    + $[c_n,d_n]\subset[a_n,b_n]$
  + Update Rule
    + $
\begin{equation}
\left.
\begin{gathered}
f(c_n)>f(d_n)\rightarrow[a_{n+1},b_{n+1}]=[c_n,b_n] \newline
f(c_n)<f(d_n)\rightarrow[a_{n+1},b_{n+1}]=[a_n,d_n]
\end{gathered}
\right. \notag
\end{equation}
$

## Multivariate Function Minimization

+ Problem: $x^*=argmin_{x\in\mathbb{R}^p}f(x)$
+ Iterative Algorithm: for $n=1,2,...$
  + $x_{n+1}=x_n+\alpha_nd_n,\alpha_n>0,f(x_{n+1})<f(x_n)$
  + $\alpha_n\in\mathbb{R}$: Step Size or Learning Rate
  + $d_n\in\mathbb{R}^p$: Descent Direction Vector
+ How to find $\alpha_n$ and $d_n$?
  1. Find a descent direction $d_n$
  2. Find a step size $\alpha_n$
     + $a_n=argmin_{t>0}g_n(t),g_n(t)=f(x_n+td_n)$

### Descent Condtion for Direction Vector

+ Direction Opposite to Current Gradient
  + Let $x_\alpha=x+\alpha d$, then by the first order Taylor's expansion around $x$, we have $f(x_\alpha)$
    + $\begin{equation}\begin{aligned}f(x_\alpha)&=f(x)+\nabla f(x)^T(x_\alpha-x)+o(||x_\alpha-x||)\newline &=f(x)+\alpha\nabla f(x)^Td+o(\alpha||d||)\newline &=f(x)+\alpha\nabla f(x)^Td+o(\alpha)\end{aligned}\notag\end{equation}$
    + $\nabla f(x)=\partial f(x)/\partial x_j,j\leq p$: Gradient vector of $f$ at $x$
  + (Descent Condition) So we have, $f(x_\alpha)-f(x)<\alpha\nabla f(x)^Td<0$, for all sufficiently small $\alpha>0$, if $\nabla f(x)^Td<0$

### Gradient Descent Algorithm

+ General Form with Negative Gradient Direction
  + $x_{n+1}=x_n+\alpha_nd_n=x_n-\alpha_nD_n\nabla f(x_n)$
    + $D_n$: Strictly Positive Definite Matrix
  + $\nabla f(x_n)^TD_n\nabla f(x_n)>0$
+ Various Directions Vectors
  + Steepest Descent: $D_n=I_p\rightarrow x_{n+1}=x_n-\alpha_n\nabla f(x_n)$
  + Newton-Raphson: $D_n=\nabla^2f(x_n)^{-1},\alpha_n=1$
  + Modified Newton's Method: $D_n=\nabla^2f(x_0)$ for some $x_0$
  + Diagonally Scaled Steepest Descent: $D_n=[diag(\nabla^2f(x_n))]^{-1}$

### Step Size of Gradient Descent Algorithm

+ Limited Minimization Rule
  + $f(x_n+\alpha_nd_n)=min_{\alpha\in[0,s]}f(x_n+\alpha d_n)$, for some $s>0$
+ Successive Step Size Reduction (Armijo Rule, Armijo [1996])
  + Find the first integer $m\geq 0$ that satisfies the stopping rule $f(x_n+r^msd_n)-f(x_n)\leq\sigma r^ms\nabla f(x_n)^Td_n$, for some constans $s>0,0<r<1$ and $0<\sigma<1$
  + Practical Choice: Try $\alpha_n=1,1/2,1/4,...$
+ Deterministic Step Size: Small Constant (0.1, 0.01, 0.001)
+ A Sequence: Square summable but not summable ($\propto1/n$), nonsummable diminishing ($\propto1/\sqrt{n}$), ...

### Coordinate Descent Algorithm

+ Successive Minimization of Univariate Functions
+ Iterative Algorithm: for $n=1,2,...$ repeat inner cycling below
  + Inner Cycling: for $j=1,2,...,p$
    + $x_{(n+1)j}argmin_{t\in\mathbb{R}}f(x_{(n+1)1},...,x_{(n+1)(j-1)},t,x_{n(j+1)},...,x_{np}$
    + Direction vector for the $j$th inner cycling step
      + $
\begin{equation}
d_{nk}=
\left\lbrace
\begin{gathered}-sign(\partial f(\tilde x_{nj})/\partial x_j),&k=j\newline 0, &k\neq j
\end{gathered}
\right. \notag
\end{equation}
$
      + $\tilde x_{nj}=(x_{(n+1)1},...,x_{(n+1)(j=1)},x_{nj},x_{n(j+1)},...,x_{np})$
+ Inner Cycling Minimization
  + Closed Form vs Univariate Minimization
  + Invariance to the order of coordinates
  + Individual Corrdinate vs A Block of Coordinates
  + `one-at-a-time` not `all-at-once`
+ Convergence Cases
  + $f$: Convex and Differentiable $\rightarrow$ Always converges to a local minimizer
    + $f(x,y)=x^2+y^2+x+10y$
  + $f$: Convex but Not Differentiable $\rightarrow$ May stuck in a point that is not a local minimizer
    + $f(x,y)=(x-y)^2+(x+y)^2+|x-y|+20|x+y|$
  + CD algorithm always converges if $f(x)=g(x)+\Sigma^p_{j=1}h_j(x_j)$, where $g$ is convex differentiable and $h_j$ is convex but may not differentiable for all $j\leq p$ [Tseng, 2001]
    + $f(x,y)=x^2+y^2+|x|+10|y|$

### Sub-Gradient (Descent) Algorithm

+ $u(x_0)$: Sub-gradient of $f$ at $x_0$ if $f(x)\geq f(x_0)+u(x_0)^T(x-x_0),\forall x\in B(x_0,\delta)$
+ Sub-Gradient Descent Algorithm: $x_{n+1}=x_n-\alpha_nu_n$
  + $u_n$: Sub-gradient at $x_n$
  + $f$: Convex but may not differentiable
  + Not a descent method
  + Stopping rule by tracing $f^{best}_n=min\{f(x_1),...,f(x_n)\}$
  + Deterministic step size
    + $\alpha_n$: Small constant, square summable but not summable ($1/n$), nonsummable diminishing ($1/\sqrt{n}$), ...


### Stochastic Gradient (Descent) Algorithm

+ Minimizing Empirical Risk Function: $R_n(\beta)=\Sigma^n_{i=1}L(y_i,x_i^T\beta)$
  + Batch: Whole Samples
    + $\beta_{t+1}=\beta_t-\alpha_t\Sigma^n_{i=1}\nabla L(y_i,x_i^T\beta_t)$
  + Stochastic: One Random Smaple $(y_i,x_i)$
    + $\beta_{t+1}=\beta_t-\alpha_t\nabla L(y_i,x_i^T\beta_t)$
  + Mini-Batch: A Number of Random Sample $(y_i,x_i),i\in S$
    + $\beta_{t+1}=\beta_t-\alpha_t\Sigma_{i\in S}\nabla L(y_i,x_i^T\beta_t)$

***

# Learning Methods

***

# Model Comparison