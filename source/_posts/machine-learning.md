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
  + $\mathcal{Y}$: Infinite and Ordered ($\mathcal{Y}=\mathbb{R},\mathbb{R}^+,\mathbb{N}\cup\lbrace0\rbrace,...$)
  + Linear Regression: $\mathcal{Y}=\mathbb{R}$
  + Poisson Regression: $\mathcal{Y}=\mathbb{N}\cup\lbrace0\rbrace$
+ Classification
  + $\mathcal{Y}$: Finite and Unordered ($\mathcal{Y}=\lbrace0,1\rbrace,\lbrace-1,1\rbrace,\lbrace1,...,k\rbrace,...$)
  + Logistic Regression: $\mathcal{Y}=\lbrace0,1\rbrace$
  + Support Vector Machine: $\mathcal{Y}=\lbrace-1,1\rbrace$
  + Multinomial Regression: $\mathcal{Y}=\lbrace1,...,k\rbrace$
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
    + Logistic: $log\lbrace1+exp(-yf(x))\rbrace$
    + Exponential: $exp(-yf(x))$
    + Hinge: $max\lbrace0,1-yf(x)\rbrace$
    + $\psi$: $I[yf(x)\leq0]+max\lbrace0,1-yf(x)\rbrace I[yf(x)>0]$
+ Risk Function: $R(f)=E_{(y,x)}L(y,f(x))$
  + Long-Term average of losses or costs
    + Square Loss: $E(y-f(x))^2$
    + Zero-One Loss: $EI[y\neq \phi(x)]=P[y\neq \phi(x)]$
    + Condition Risk: $R(f)=E_{y|x}[L(y,f(x))|x]$
+ Empirical Risk Minimization: $\hat f=arg\min_{f\in \mathcal{F}}R_n(f)$
  + Empirical Risk Function: $R_n(f)=\Sigma^n_{i=1}L(y_i,f(x_i))/n$
    + Training Sample ($y_i,x_i$), $i\leq n$: Independent samples / observations of $(y,x)$
    + Linear Regression with Square Loss: $\hat \beta =arg\min_\beta\Sigma^n_{i=1}(y_i-x^T_i\beta)^2/n$
    + Logistic Regression with Logistic Loss: $\hat\beta=arg\min_\beta\Sigma^n_{i=1}\lbrace-y_ix^T_i\beta+log(1+exp(x^T_i\beta))\rbrace/n$

***

# Iterative Algorithms

+ Univariate Function Minimization
  + Iterative Grid Search Algorithm
  + Golden Section Algorithm
+ Multivariate Function Minimization
  + Coordinate Descent Algorithm
  + Gradient Descent Algorithm

## Univariate Function Minimization

+ Problem: find $x^*=arg\min_{x\in[a,b]}f(x)$
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

+ Non-Iterative Grid Search Alhorithm: $x^*\approx arg\min_{z\in z_k=a+k(b-a)/m|k=0,...,m}f(z)$
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
  + $k_n=arg\min_{k\in\lbrace0,...,m\rbrace}f(a_n+k(b_n-a_n)/m)$

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

+ Problem: $x^*=arg\min_{x\in\mathbb{R}^p}f(x)$
+ Iterative Algorithm: for $n=1,2,...$
  + $x_{n+1}=x_n+\alpha_nd_n,\alpha_n>0,f(x_{n+1})<f(x_n)$
  + $\alpha_n\in\mathbb{R}$: Step Size or Learning Rate
  + $d_n\in\mathbb{R}^p$: Descent Direction Vector
+ How to find $\alpha_n$ and $d_n$?
  1. Find a descent direction $d_n$
  2. Find a step size $\alpha_n$
     + $a_n=arg\min_{t>0}g_n(t),g_n(t)=f(x_n+td_n)$

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
  + $f(x_n+\alpha_nd_n)=\min_{\alpha\in[0,s]}f(x_n+\alpha d_n)$, for some $s>0$
+ Successive Step Size Reduction (Armijo Rule, Armijo [1996])
  + Find the first integer $m\geq 0$ that satisfies the stopping rule $f(x_n+r^msd_n)-f(x_n)\leq\sigma r^ms\nabla f(x_n)^Td_n$, for some constans $s>0,0<r<1$ and $0<\sigma<1$
  + Practical Choice: Try $\alpha_n=1,1/2,1/4,...$
+ Deterministic Step Size: Small Constant (0.1, 0.01, 0.001)
+ A Sequence: Square summable but not summable ($\propto1/n$), nonsummable diminishing ($\propto1/\sqrt{n}$), ...

### Coordinate Descent Algorithm

+ Successive Minimization of Univariate Functions
+ Iterative Algorithm: for $n=1,2,...$ repeat inner cycling below
  + Inner Cycling: for $j=1,2,...,p$
    + $x_{(n+1)j}arg\min_{t\in\mathbb{R}}f(x_{(n+1)1},...,x_{(n+1)(j-1)},t,x_{n(j+1)},...,x_{np}$
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
  + Stopping rule by tracing $f^{best}_n=\min\lbrace f(x_1),...,f(x_n)\rbrace$
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

+ Linear and Logistic Regression
+ High-Dimensional Linear Regression
  + Ridge
  + LASSO
  + SCAD
+ Forward Greedy Methods
  + Forward Selection
  + Stagewise Regression
  + LARS
+ Support Vector Machine
+ Artificial Neural Network
+ Tree and Ensemble
  + Bagging
  + Random Forest
  + Boosting

## Linear and Logistic Regression

### Linear Regression

+ Regression Function and Prediction
  + $f(x)=x^T\beta,y_x=f(x)=x^T\beta$
+ Least Square Estimator, LSE: Empirical Risk Function with Square Loss
  + $R_n(\beta)=\Sigma^n_{i=1}(y_i-x_i^T\beta)^2$
+ Algorithm
  + Direct Calculation
    + $\hat\beta=(\Sigma^n_{i=1}x_ix_i^T)^{-1}\Sigma^n_{i=1}x_iy_i$
  + Gradient Descent Algorithm
    + $\beta_{t+1}=\beta_t+\alpha_t\Sigma^n_{i=1}x_i(y_i-x_i^T\beta_t)$
  + Inner Cycling for Coordinate Descent
    + $\beta\_{(t+1)j}=\Sigma^n\_{i=1}x\_{ij}(y\_i-\Sigma\_{k\neq j}x\_{ik}\tilde{\beta}\_{tk}/\Sigma^n\_{i=1}x^2\_{ij})$

#### Other Empirical Risk Functions

+ Generalized Least Square Estimation
  + $R_n(\beta)=\Sigma_{i,j}(y_i-x_i^T\beta)\Omega_{ij}(y_j-x_j^T\beta)$
+ Quantile Regression
  + $R_n(\beta)=\Sigma^n_{i=1}\rho_\tau(y_i-x_i^T\beta)$
  + Linear Programming
  + Sub-Gradient Descent
+ Regularization (Penalization) via $J_\lambda$
  + $R_n^\lambda(\beta)=R_n(\beta)+\Sigma^p_{i=1}J_\lambda(|\beta_j|),\lambda>0$
  + Coordinate Descent Algorithm
  + Sub-Gradient Descent
  + Convex Concave Procedure

### Logistic Regression

+ Regression Function and Prediction 
  + $f(x)=x^T\beta,y_x=\phi(x)=I(f(x)>0)$
+ Empirical Risk Function
  + $R_n(\beta)=\Sigma^n_{i=1}(-y_ix_i^T\beta+log(1+exp(x_i^T\beta)))$
+ Algorithm
  + Gradient Descent Algorithm
    + $\beta_{t+1}=\beta_t-(\Sigma^n_{i=1}x_ip_{ti}(1-p_{ti})x^T_i)^{-1}\Sigma^n_{i=1}(p_{ti}-y_i)x_i$

### Statistical Interpretation

+ Maximum Likelihood Estimation
  + Empirical Risk Function: Negative Log-Likelihood Function
  + Linear Regression
    + Normal Distribution Assumption with Known Variance
    + $y_i|x_i\sim N(f(x_i),\sigma^2),i\leq n$
  + Logistic Regression
    + Bernoulli Distribution Assumption
    + $y_i|x_i\sim B(1,exp(f(x))/(1+exp(f(x)))),i\leq n$
  + Another Equivalent Form for $y\in \lbrace-1,1\rbrace$
    + Empirical Risk Function with Logistic Loss
    + $R_n(\beta)=\Sigma^n_{i=1}log(1+exp(-y_ix_i^T\beta))$

## High-Dimensional Linear Regression

### Penalized Estimation

+ Penalized Empirical Risk Functrion
  + $R_n^\lambda(f)=R_n(f)+J^\lambda(f)$
  + $R_n$: Empirical Risk Function
  + $f\in\mathcal{F}$: Regression Fuction
  + $J_\lambda$: Penalty Function
  + $\lambda$: Tuning Parameter (Vector)
+ Objectives and Characteristics
  + Regularization
  + Variable Selection
  + High-Dimensional Data Analysis
  + Structure Estimation

### Variable Selection in Linear Regression

+ Penalized Empirical Risk Function for The Square Loss
  + $R_n^\lambda(\beta)=\Sigma^n_{i=1}(y_i-x_i^T\beta)+\Sigma^p_{j=1}J^\lambda(|\beta_j|)$
+ Algorithm: Penalty Functions
  + Ridge: $J^R_\lambda(|\beta|)=\lambda\beta^2$
  + LASSO: $J^L_\lambda(|\beta|)=\lambda|\beta|$
  + Bridge: $J^B_\lambda(|\beta|)=\lambda|\beta|^\nu,\nu>0$
  + SCAD: $\nabla\lambda^S_{\lambda,a}(|\beta|)=\lambda I(|\beta|<\lambda)+(\lambda-a|\beta|)+a/(a-1)I(|\beta|\geq\lambda)$
  + MC: $\nabla J^M_{\lambda,a}(\beta)=(\lambda-\beta/a)_+$
  + Elastic Net: $J^E_{\lambda,\gamma}(\beta)=\lambda\beta+\gamma\beta^2$

### Ridge

+ Example) Simple Linear Regression
  + $\begin{equation}\left\lbrace\begin{gathered}R_n(\beta)=\Sigma^n_{i=1}(y_i-x_i\beta)^2=(\beta-3)^2/2\newline R^\lambda_n(\beta)=(\beta-3)^2/2+\lambda\beta^2\end{gathered}\notag\right.\end{equation}$
  + Least Square Estimator
    + $\tilde{\beta}=arg\min_\beta R_n(\beta)=3$
  + Ridge [Hoerl and Knnard, 1970]
    + $\tilde{\beta}^R=arg\min_\beta R^\lambda_n(\beta)=1/(1+2\lambda)\tilde{\beta}$
+ Results
  + Shrinkage or Biased: $|\hat\beta^R|<|\tilde{\beta}|$ for any $\lambda>0$
  + Better Mean Square Error Under Multicollinearity

### LASSO

+ (Cont.) Simple Linear Regression
  + $R^\lambda_n(\beta)=(\beta-3)^2/2+\lambda|\beta|$
  + Least Square Estimator
    + $\tilde{\beta}=arg\min_\beta R_n(\beta)=3$
  + Least Absolute Shrinkage and Selection Operator (LASSO) [Tibshirani, 1996]
+ Results
  + Shrinkage or Biased: $|\hat\beta^L|<|\tilde{\beta}|$ for any $\lambda>0$
  + Sparsity or Variable Selection: $\hat\beta^L=0$ or $\hat\beta^L\neq0$ for some $\lambda$

### SCAD

+ Smoothly Clipped Absolute Deviation (SCAD) [Fan and Li, 2001]
  + $R_n^\lambda=(\beta-3)^2+J_\lambda(|\beta|)$
+ Solution
  + $\begin{equation}\hat\beta\^2=arg\min_\beta R^\lambda_n(\beta)=\left\lbrace\begin{aligned}0,&\ |\tilde{\beta}|<\lambda\newline u(\tilde{\beta},\lambda),&\ \lambda\leq|\tilde{\beta}|<a\lambda\newline\tilde{\beta},&\ |\tilde{\beta}|\geq a\lambda\end{aligned}\right.\notag\end{equation}$
+ Results
  + No Shrinkage or Unbiased: $\hat\beta^S=\tilde{\beta}$ for any $\lambda\leq|\tilde{\beta}|/a$
  + Sparsity: $\hat\beta^S=0$ or $\hat\beta^S\neq0$ for some $\lambda$

### Coordinate Descent Algorithm

+ LSE
  + Problem: Minimize $R_n(\beta)=\Sigma^n_{i=1}(y_i-x_i^T\beta)^2/2$
  + Coordinate Function of $\beta_j$
    + $R_{nj}(\beta_j)\propto\lbrace\Sigma^n_{i=1}x_{ij}^2/2\rbrace\beta_j^2-\lbrace\Sigma^n_{i=1}x_{ij}(y_i-\Sigma_{k\neq j}x_{ik}\beta_k)\rbrace\beta_j$
  + Coordinate Descent Algorithm
    + $\tilde{\beta}\_{(t+1)j}=\lbrace\Sigma^n\_{i=1}x\_{ij}(y\_i-\Sigma\_{k\neq j}x\_{ik}\tilde{\beta}\_{tk})\rbrace/\lbrace\Sigma^n\_{i=1}x\_{ij}^2\rbrace$
+ LASSO
  + Problem: Minimize $R^\lambda_n(\beta)=R_n(\beta)+\lambda\Sigma^p_{j=1}|\beta_j|$
  + Coordinate Function of $\beta_j$
    + $R_{nj}^\lambda(\beta_j)\propto R_{nj}(\beta_j)+\lambda|\beta_j|$
  + Coordinate Descent Algorithm [Friedman et al., 2007]
    + $\beta\_{(t+1)j}=soft(\tilde{\beta}\_{(t+1)j},\lambda/\Sigma^n\_{i=1}x\_{ij}^2)$
    + Soft-Thresholding Operator
      + $soft(x,\lambda)=arg\min_\beta\lbrace(\beta-x)^2/2+\lambda|\beta|\rbrace=sign(x)(|x|-\lambda)_+$
+ SCAD
  + Problem: Minimize $R_n^\lambda(\beta)=R_n(\beta)+\Sigma^p_{j=1}J_S^\lambda(|\beta_j|)$
  + CCCP + CD Algorithm [Kim et al., 2008], [Lee et al., 2016]
    + $\beta_{t+1}=arg\min_\beta U^{\lambda}_n(\beta|\beta_t)$
    + Conbex-Concave Decomposition of The Penalty
      + $J_S^\lambda(|\beta_j|)=\lambda|\beta_j|+(J_S^\lambda|\beta_j|-\lambda|\beta_j|)$
    + Upper Tight Convex Function of $R_n^\lambda$ at $\beta^c$
      + $U^\lambda_n(\beta|\beta^c)=R_n(\beta)+\Sigma^p_{j=1}\lbrace(\nabla J^\lambda_S(|\beta^c_j|)-\lambda sign(\beta^c_j))\beta_j+\lambda|\beta_j|\rbrace$

### Applications

+ High Dimensional Data Analysis
  + Number of Parameters $\geq$ Number of Samples
  + Allow Various Over-Parameterized Models
+ `Regularization` or `Stabilization`
  + Applied together with almost all learning methods
  + Prevents overfit
  + Structure estimation
+ Structure Construction
  + LASSO: $\lambda\Sigma^p_{j=1}|\beta_j|\leftrightarrow\hat\beta_j=0$ or not
  + Fused LASSO [Tibshirani et al., 2005]
    + $\lambda_1\Sigma^p_{j=1}|\beta_j|+\lambda_2\Sigma^p_{j=2}|\beta_j-\beta_{j-1}|$
      + $\lambda_1$: $\hat\beta_j=0$
      + $\lambda_2$: $\hat\beta_k=\hat\beta_{k+1}=...=\hat\beta_{k'}\neq0$
  + Group LASSO [Yuan and Lin, 2006]
    + $\lambda\Sigma^K\_{k=1}|\sqrt{\Sigma^{p\_k}\_{k=1}\beta^2\_{kj}}$
  + Strong Heredity Interaction LASSO [Choi et al.m 2010]
    + $\lambda\Sigma^p_{j=1}|\beta_j|+\lambda_2\Sigma_{j<k}|\eta_{kj}|,\eta_{jk}=\delta_{jk}\beta_j\beta_k$
      + $\lambda_1$: $\beta_j=0$
      + $\lambda_2$: $\beta_j=0$ or $\beta_k=0\rightarrow\eta_{jk}=0$
      + $\lambda_3$: $\beta_j\neq0$ and $\beta_k\neq0\rightarrow\eta_{jk}\neq0$

## Forward Greedy Methods

### Forward Selection in Linear Regression

+ Algorithm: Residual-Based Forward Selection
  + Let $\beta=0$
  + For $t=1,2,...$ repeat the followings
    1. Calculate residuals $r_i=y_i-x_i^T\beta^t,\ i\leq n$
    2. Find $k=arg\min_j\Sigma_i(r_i-x_{ij}\beta_j)^2$
    3. Find $\beta^{t+1}=arg\min_{\beta^t,\beta_k}\Sigma_i(y_i-\Sigma_Ix_{iI}\beta_I^t-x_{ik}\beta_k)^2$
+ Intuition and Result
  + It iteratively includes the variable $x_k$ that is the most correlated with current residual
  + Sequence of Least Square Estimators: $\beta^0\rightarrow\beta^1\rightarrow\beta^2\rightarrow...$

### Forward Stagewise Regression

+ Originality
  + Stepwise Least Squares [Goldberger, 1961]
  + Residual Analysis [Freund et al., 1961]
+ Algorithm
  + Let $\beta=0$ and fix $\lambda^{FSW}>0$ as a small constant
  + For $t=1,2,...$ repeat the followings
    + Calculate residuals $r_i=y_i-x_i^T\beta^t,i\leq n$
    + Find $(k,\beta_k)=arg\min_{j,\beta_j}\Sigma_i(r_i-x_{ij}\beta_j)^2$
    + Update $\beta^{t+1}=\beta^t+\lambda^{FSW}sign(\beta_k)$
+ Result
  + We get a long sequence of regularized estimators because of the choise $\lambda^{FSW}$

### Least Angle Regression

+ Least Angle Regression (LARS) [Efron et al., 2004]
  + The same as the stragewise regression except that $\beta^{t+1}=\beta^t+\lambda^{LARS}sign(\beta_k)$
    + $\lambda^{LARS}$ makes the new residual equally correlated with all the input variables included
    + $\lambda^{LARS}$ has easy closed from w.r.t. current $\beta^t$
+ Some Connection
  + LARS-LASSO: LARS + Deletion Step = LASSO
  + LARS-Stagewise: Stagewise with $\lambda^{FSW}\rightarrow0=$LARS

## Support Vector Machine

+ Support Vector Machine (SVM) for Binary Classification [Vapnik, 1995]
  + Regression Function and Prediction
    + $f(x)=b+x^Tw,\ y_x=\phi(x)=sign(f(x))$
  + Pernalized Problem: Pernalized Empirical Risk Function
    + $R_n^\lambda(\beta)=\Sigma_{i=1}^n\lbrace1-y_if(x_i)\rbrace_++\lambda||w||^2,\ \lambda>0$
    + Hinge Loss + Ridge Penalty
    + $x_+=\max\lbrace0,x\rbrace$
  + Stochastic: Sub-Gradient Algorithm [Shalev-Shwartz et al., 2007]
    + $w_{t+1}=w_t+\alpha_t\lbrace-\Sigma^n_{i=1}y_ix_iI(y_if(x_i)<1)+2\lambda w_t\rbrace$

### Maximizing Margin

+ Primal Problem: Minimizing $||w||^2/2+\gamma\Sigma^n_{i=1}\xi_i,\gamma>0$ subject to $y_if(x_i)\geq1-\xi_i,\xi_i\geq0,i\leq n$
  + $\xi_i$: Slack Variable for Quantifying Degree of Missclassification
    + $x_i$ with $\xi_i=0$: Support Vector
    + $x_i$ with $0<\xi_i\leq1$: Correctly Classified Sample
    + $x_i$ with $1<\xi_i$: Incorrectly Classified Sample
  + $2/||w||$ (Margin): Distance between $f$ and support vector
+ Equivalence between primal and penalized problem $y_if(x_i)\geq1-\xi_i,\xi_i\geq0\leftrightarrow\xi_i=\max\lbrace0,1-y_if(x_i)\rbrace$

### KKT Conditions

+ Lagrange Primal Function with Multipliers: $||w||^2/2+\gamma\Sigma^n_{i=1}\xi_i-\Sigma^n_{i=1}\alpha_i\lbrace y_if(x_i)-(1-\xi_i)\rbrace-\Sigma^n_{i=1}\mu_i\xi_i$
  + Stationarity: $w=\Sigma^n_{i=1}\alpha_iy_ix_i,\Sigma^n_{i=1}\alpha_iy_i=0,\gamma=\alpha_i+\mu_i,i\leq n$
  + Primal and Dual Feasibility: $y_if(x_i)-(1-\xi_i)\geq0,\xi_i\geq0,i\leq n$
  + Complementary Slackness: $\alpha_i\lbrace y_if(x_i)-(1-\xi_i)\rbrace=0,\mu_i\xi_i=0,i\leq n$
+ Dual Problem: Minimizing lagrange dual objective function $\Sigma^n_{i=1}\Sigma^n_{j=1}y_iy_j\alpha_i\alpha_j\langle x_i,x_j\rangle-2\Sigma^n_{i=1}\alpha_i$ subject to $Sigma^n_{i=1}\alpha_iy_i=0,-\leq\alpha_i\leq\gamma,i=1,...,n$
  + Quadratic Programming (QP)
  + CD Algorithm [Sequential Minimal Optimization, Platt, 1998]
    + Relation between $\alpha_i$ and $\alpha_j,i\neq j$
      + $y_i\alpha_i+y_j\alpha_j=-\Sigma_{k\neq i,j}y_k\alpha_k=c$
    + Univariate optimization from thje inequality $\alpha_i=(c-y_j\alpha_j)y_i$ under constraints $L\leq\alpha_j\leq H$ for some $0\leq L<H\leq\gamma$
+ Slope: Linear Combination of Samples (Stationarity)
  + $w=\Sigma^n_{i=1}\alpha_iy_ix_i$
+ Implicity of Slope
  + $f(x)=x^Tw+b=\Sigma^n_{i=1}\alpha_iy_ix_i^Tx+b$
  + Inner products are required only
  + Classification depends on non-zero $a_i$s, i.e., support vector $x_i$s (Sparsity)

### Non-Linear Regression Function

+ Linear Solution from Optimization
  + $f(x)=\Sigma^n_{i=1}\alpha_iy_i\langle x_i,x\rangle+b$
+ Non-Linear Feature Transformation
  + $x\rightarrow\Phi(x),f(x)=\Sigma^n_{i=1}\alpha_iy_i<\Phi(x_i),\Phi(x)>+b$
  + Kernel Trick: Kernel Function $K$
    + $K(x,x')=\langle\Phi(x_i),\Phi(x')\rangle\rightarrow f(x)=\Sigma^n_{i=1}\alpha_iy_iK(x_i,x)$
      + Linear Kernel: $K(x,x')=\langle x,x'\rangle$
      + D-th Order Polynomial Kernel: $K(x,x')=(\langle x,x'\rangle+I)^d$
      + Gaussian Kernel: $K(x,x')=exp(-||x-x'||^2/\sigma^2)$
      + Sigmoid Kernel: $K(x,x')=tanh(\kappa_1\langle x,x'\rangle+\kappa_2)$
+ SVM as a penalized estimation $R_n^\lambda(\beta)=\Sigma^n\_{i=1}(1-y\_if(x_i))\_++\lambda||f||^2_{\mathcal{H}_K},\lambda>0$
  + $\mathcal{H}_K$: Reproducing kernel Hilbert space w.r.t. a kernel $K$
  + Representation Theorem: The minimizer of $R_n$ is represented as $f(x)=\Sigma^n_{i=1}\alpha_iy_iK(x_i,x)$
    + Example)
      + $\begin{equation}\left\lbrace\begin{gathered} K(x,x')=\langle\Phi(x),\Phi(x')\rangle\newline\mathcal{H}\_K=\lbrace\Phi(x)^Tw+b|w\in\mathbb{R}^q,b\in\mathbb{R}\rbrace\end{gathered}\right.\notag\rightarrow||f\_{\mathcal(H)\_K}||^2=||w||^2\end{equation}$

## Artificial Neural Network

## Tree and Ensemble
***

# Model Comparison