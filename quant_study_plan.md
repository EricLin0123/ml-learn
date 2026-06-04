# Quant Interview Study Roadmap — Statistics, Machine Learning & Time Series

A time-ordered learning path. Topics are sequenced so that **prerequisites always come before what depends on them**. You already studied calculus, linear algebra, and probability/statistics, so this plan is about *waking those up and adding depth* — not teaching from zero.

> Companion diagram: see `quant_roadmap.svg`. Red chains in the diagram mark **hard dependencies** (you cannot skip ahead).

---

## Phase 0 — Mathematical Foundations
*Estimated time: 2–3 weeks. Refresh all of this first; everything downstream depends on it.*

These three blocks are the bedrock. If you skip them, you will stall in Phases 3 and 4.

**Linear algebra** is the hidden protagonist of quant interviews. The point isn't computation — it's being able to explain things geometrically. The three things to know cold:

Singular Value Decomposition (SVD), the common source of PCA, dimensionality reduction, and low-rank approximation:

$$A = U\Sigma V^{\top}$$

The projection matrix — linear regression is, at heart, "project $y$ onto the column space of $X$":

$$P = X(X^{\top}X)^{-1}X^{\top}$$

Positive (semi)definiteness: $x^{\top}A x \ge 0$ for all $x$. Covariance matrices, Hessians, and the invertibility behind Ridge regression all rely on it.

**Multivariable calculus** — you only need to recover gradients, the Hessian, and Lagrange multipliers. Lagrange is the core tool for portfolio optimization later:

$$\mathcal{L}(x,\lambda) = f(x) - \lambda\, g(x)$$

**Probability foundations** — density functions, the moment generating function (MGF), the exponential family, the memoryless property, and the Central Limit Theorem (CLT). The MGF is a frequent interview shortcut:

$$M_X(t) = \mathbb{E}\!\left[e^{tX}\right]$$

---

## Phase 1 — Core Statistical Inference
*Estimated time: 2 weeks. Prerequisite: all of Phase 0.*

This phase builds the full inferential arc: estimate → judge how good the estimate is → make a decision.

**Estimation & MLE.** Maximum likelihood is the methodology that runs through both statistics and machine learning — internalize it first:

$$\hat\theta_{\text{MLE}} = \arg\max_{\theta}\ \prod_{i=1}^{n} f(x_i;\theta)$$

**Properties of estimators** — bias, efficiency, consistency, sufficiency. The bias definition is simple, but you must be able to articulate the bias–variance tension (it returns in Phase 3):

$$\text{Bias}(\hat\theta) = \mathbb{E}[\hat\theta] - \theta$$

**Hypothesis testing** — correctly interpreting the p-value, Type I error, test power, and multiple-comparison traps. Interviewers love asking "what *is* a p-value, exactly" — be able to state it correctly in one sentence. The CLT underpins large-sample inference here:

$$\sqrt{n}\,(\bar X_n - \mu) \xrightarrow{d} \mathcal{N}(0,\sigma^2)$$

**Multivariate normal / multinomial** — needs linear algebra (covariance matrices) and is the basis for the Kalman filter and factor models later.

---

## Phase 2 — Bayesian Inference & Stochastic Simulation
*Estimated time: 2–3 weeks. Prerequisite: estimation & hypothesis testing from Phase 1.*

**Bayes' theorem & conjugate priors** (the article calls this a guaranteed exam topic). Lock this in first:

$$p(\theta \mid x) \propto p(x \mid \theta)\, p(\theta)$$

A conjugate prior means prior and posterior are in the same family, giving a closed-form update (e.g., Beta–Binomial).

**Bootstrap** — needs estimation and confidence intervals first, since it approximates the sampling distribution by resampling.

Now the **hard dependency chain** you specifically asked about. The order is non-negotiable:

1. **Random variable generation / Acceptance–Rejection** — first learn how to sample from a distribution at all.
2. **Markov Chain** — state transitions and the stationary distribution. This is the bedrock of MCMC.
3. **MCMC** — construct a Markov chain whose stationary distribution is exactly the target you want to sample from.
4. **Metropolis–Hastings** — the concrete MCMC algorithm. Its acceptance probability is:

$$\alpha(x \to x') = \min\!\left(1,\ \frac{p(x')\,q(x \mid x')}{p(x)\,q(x' \mid x)}\right)$$

**You must learn it in the order Markov Chain → MCMC → Metropolis–Hastings.** Jumping straight to M–H is hopeless, because every symbol in it comes from the two layers beneath it.

**Martingales & stochastic calculus** can sit at the end of this phase or be deferred — you can come back for them when you reach Black–Scholes in Phase 6.

---

## Phase 3 — Machine Learning Foundations
*Estimated time: 2–3 weeks. Prerequisite: linear-algebra projection + MLE.*

**Linear regression** should be re-understood through the lens of *projection*; the OLS solution is exactly the projection matrix from Phase 0:

$$\hat\beta_{\text{OLS}} = (X^{\top}X)^{-1}X^{\top}y$$

**Regularization.** Ridge adds $\lambda I$ to the diagonal, guaranteeing invertibility and suppressing overfitting:

$$\hat\beta_{\text{Ridge}} = (X^{\top}X + \lambda I)^{-1}X^{\top}y$$

Lasso uses an $\ell_1$ penalty $\lambda\|\beta\|_1$, which can shrink coefficients to exactly zero for feature selection. Be ready to explain *why Lasso is sparse but Ridge is not* (geometrically: a diamond constraint vs. a circle).

**Logistic regression** — $p = \dfrac{1}{1+e^{-x^{\top}\beta}}$ — and how it relates to linear regression under the generalized-linear-model framework.

**Bias–variance tradeoff, cross-validation, feature engineering, outlier handling** — these are the daily bread of your role (feature mining, model evaluation), so drill them until they're reflexive.

---

## Phase 4 — Advanced Machine Learning
*Estimated time: 3–4 weeks. **This is the most central block for your job.** Prerequisite: all of Phase 3.*

**Bagging / Boosting** maps directly to the LightGBM / XGBoost you'll use at work. Understand that Boosting is an additive model ("one tree after another, each correcting the previous residual") and how that fundamentally differs from Bagging (parallel, variance-reducing).

**EM algorithm** — needs MLE plus Bayesian thinking; it's the standard tool for latent-variable problems. **Kalman filter** — needs the multivariate normal; it's the basis for state estimation in time series.

**Dimensionality reduction** — PCA is built directly on SVD / eigendecomposition (so Phase 0's linear algebra cannot be skipped), then extends to factor analysis and autoencoders.

**Neural networks** — backpropagation (just the chain rule) and the vanishing-gradient problem. Only after this are you ready for Transformers.

**The Transformer track is another hard chain:** sequence models → self-attention → Transformer. The core self-attention formula:

$$\text{Attention}(Q,K,V) = \text{softmax}\!\left(\frac{QK^{\top}}{\sqrt{d_k}}\right)V$$

Don't open the Transformer paper first — understand NNs and sequence modeling, or the motivation for $Q,K,V$ won't make sense.

---

## Phase 5 — Time Series
*Estimated time: 2 weeks. Prerequisite: regression + probability foundations.*

First nail the concepts of **stationarity, random walk, and seasonality**, then move to **ARMA** (the combination of autoregressive and moving-average terms).

Last is another small dependency: **learn heteroscedasticity before GARCH**. GARCH lets the variance evolve over time and carry memory:

$$\sigma_t^2 = \omega + \alpha\,\epsilon_{t-1}^2 + \beta\,\sigma_{t-1}^2$$

The "volatility clustering" of financial returns is modeled by this, and it's highly relevant to the high-frequency data in your job.

---

## Phase 6 — Optimization & Finance Applications
*Estimated time: 2–3 weeks. The finish line. Prerequisite: Lagrange (Phase 0), regression, stochastic calculus.*

**Optimization** — linear programming, Lagrange, KKT conditions, the Hessian determinant for convexity, slack variables. These are the tools for solving portfolio weights.

**Portfolio theory** — mean–variance optimization is just a constrained quadratic program solved with Lagrange:

$$\min_{w}\ w^{\top}\Sigma w \quad \text{s.t.}\quad w^{\top}\mu = \mu_p,\ \ w^{\top}\mathbf{1}=1$$

From this you derive the efficient frontier and the tangency portfolio.

**Asset pricing** — CAPM and the Fama–MacBeth regression (the classic two-step factor test):

$$\mathbb{E}[R_i] = R_f + \beta_i\big(\mathbb{E}[R_m] - R_f\big)$$

**Black–Scholes** needs the stochastic calculus from Phase 2 as a prerequisite. Finally, tie it all together into the **alpha / factor exploration workflow** — which is also the core deliverable of your target role.

---

## Parallel Track — CS & Engineering
*A little every day, throughout the whole period.*

Data structures, algorithms (DP, DFS/BFS, binary search), OOP, and SQL **do not need to wait for the statistics track**. From day one, grind 1–2 Leetcode problems daily (medium–hard) just to keep your hands warm.

---

## Notes on Using This Plan

- The full path takes roughly **4–5 months** for one pass — about the same as the interview cycle described in the article.
- If time is tight, **Phase 4** (Boosting / feature engineering / evaluation) and **Phase 5** (time series, GARCH) give the highest direct payoff for an ML Research Engineer role — weight them more heavily.
- The martingale / stochastic calculus in Phase 2 and Black–Scholes in Phase 6 lean toward derivatives pricing. If you focus on alpha signals rather than option pricing, you can defer or skip them.

Want any single phase expanded into a week-by-week plan with recommended chapters, textbooks, and self-test questions? Just ask.
