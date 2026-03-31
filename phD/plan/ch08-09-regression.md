# Chapters 8 & 9 — When Models Meet Data + Linear Regression
> **Book pages:** 251–316 | **Time:** 1 week (5 study days)

---

## The Big Idea (explain it like I'm 10)

You've now learned all the math tools (Part I). Now we use them.

**Chapter 8** explains the general framework: what is a "model," how do we define "learning," and what does "fitting a model" actually mean mathematically?

**Chapter 9** applies this framework to the simplest possible ML model: **linear regression** — drawing the best straight line through a cloud of data points.

---

## Chapter 8 — When Models Meet Data

### 8.1 Data, Models, and Learning (pages 251–258)

**Data** in ML is always a matrix:
```
X ∈ ℝ^(N × D)
```
- N = number of examples (rows)
- D = number of features (columns)

**Model** = a mathematical function f(x; θ) parameterized by θ.

**Learning** = finding θ that makes f as accurate as possible on data.

---

### 8.2 Empirical Risk Minimization (pages 258–265)

**Risk** = expected loss over all possible data.
**Empirical risk** = average loss on your actual training data.

```
R_emp(θ) = (1/N) ∑ L(yₙ, f(xₙ; θ))
```

The idea: if we can't measure true risk (we don't have infinite data), minimize empirical risk (average on training data) instead.

**Danger: overfitting!** A model might memorize training data perfectly (R_emp = 0) but fail on new data. This is why we need train/test splits and regularization.

---

### 8.3 Parameter Estimation (pages 265–272)

**Maximum Likelihood Estimation (MLE):**

Find θ that makes the training data most probable:
```
θ_MLE = argmax_θ p(data | θ)
```

In practice, maximize the log-likelihood (easier to compute):
```
θ_MLE = argmax_θ ∑ log p(yₙ | xₙ, θ)
```

**Why log?** Products become sums. Sums are easier to differentiate.

---

### 8.4 Probabilistic Modeling (pages 272–278)

Instead of predicting one number, predict a **distribution**.
- Not "the price is $500"
- But "the price follows N($500, $50²)"

This captures uncertainty — crucial for real decisions!

**MAP (Maximum A Posteriori):**
Add a prior on θ:
```
θ_MAP = argmax_θ [log p(data | θ) + log p(θ)]
```
The prior acts as **regularization** — it prevents overfitting by saying "θ probably isn't too extreme."

---

### 8.5 Directed Graphical Models (pages 278–283)

A way to visualize how variables depend on each other.
- Node = random variable
- Arrow = dependency ("A causes B")

Simplifies computing complex joint probabilities by factoring them into simple conditional probabilities.

---

### 8.6 Model Selection (pages 283–288)

How do you choose between a simple model (line) and complex model (wiggly curve)?

**Bias-variance tradeoff:**
- Simple model: high bias (systematically wrong), low variance (consistent)
- Complex model: low bias (can fit anything), high variance (unpredictable on new data)

**Cross-validation:** Split data into k folds. Train on k-1, test on 1. Rotate. Average error = honest estimate of performance.

---

## Chapter 9 — Linear Regression

### 9.1 Problem Formulation (pages 291–292)

**Goal:** Predict a real number y from input x.

**Model:**
```
y = xᵀθ + ε,   ε ~ N(0, σ²)
```
- θ = weight vector (parameters)
- ε = noise (unavoidable randomness)

In matrix form for all N training points:
```
y = Xθ + ε
```

---

### 9.2 Parameter Estimation (pages 292–303)

**MLE for linear regression = Ordinary Least Squares (OLS)**

Minimize the sum of squared errors:
```
L(θ) = ‖y - Xθ‖²
```

Take gradient, set to zero:
```
∇_θ L = -2Xᵀ(y - Xθ) = 0
→ XᵀXθ = Xᵀy
→ θ* = (XᵀX)⁻¹Xᵀy
```

This is the **closed-form solution** — no iteration needed! Just one matrix computation.

**Geometric interpretation:** θ* gives the projection of y onto the column space of X. This is orthogonal projection from Chapter 3!

---

### 9.3 Bayesian Linear Regression (pages 303–313)

Instead of finding one θ*, we find a **distribution over θ**.

With a Gaussian prior on θ and Gaussian noise:
- Prior: θ ~ N(m₀, S₀)
- Likelihood: y | X, θ ~ N(Xθ, σ²I)
- Posterior: θ | X, y ~ N(mₙ, Sₙ) (also Gaussian — conjugacy!)

**Why this is powerful:**
- We get uncertainty estimates: "θ is probably around [0.3, 0.7] ± 0.1"
- More data → tighter posterior (less uncertainty)
- Perfect for small datasets where we're uncertain about parameters

---

### 9.4 Maximum Likelihood as Orthogonal Projection (pages 313–315)

The MLE solution θ* = (XᵀX)⁻¹Xᵀy is exactly the **orthogonal projection** of y onto the column space of X.

This ties together:
- Chapter 3 (projections)
- Chapter 9 (regression)

**Ŷ = Xθ* = X(XᵀX)⁻¹Xᵀy = Hy**

Where H = X(XᵀX)⁻¹Xᵀ is the "hat matrix" — it "puts a hat" on y to create predictions ŷ.

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 251–265 | Data/model/learning + empirical risk |
| Day 2 | 265–278 | MLE, MAP, probabilistic modeling |
| Day 3 | 278–292 | Graphical models + regression formulation |
| Day 4 | 292–313 | Least squares + Bayesian regression |
| Day 5 | 313–316 | Projection interpretation + review |

---

## Self-Check Questions

1. What is empirical risk minimization in plain English?
2. What is the closed-form solution for linear regression?
3. What is the difference between MLE and MAP estimation?
4. Why does Bayesian linear regression give a distribution, not a point?
5. How is the least squares solution related to orthogonal projection?
6. What is the bias-variance tradeoff?
