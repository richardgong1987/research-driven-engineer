# Chapter 6 — Probability and Distributions
> **Book pages:** 172–224 | **Time:** 1.5 weeks (8 study days)

---

## The Big Idea (explain it like I'm 10)

You flip a coin. Will it be heads? You don't know for sure. That uncertainty is **probability**.

Now imagine you have a box of data — some measurements that could vary. How are they spread out? Are they clustered near a middle value, or all over the place? That spread is a **distribution**.

Machine learning has to deal with **uncertainty** everywhere:
- We can't see every possible example
- Our measurements have noise
- The world itself is unpredictable

Probability is the language of uncertainty. This chapter is your dictionary.

---

## Key Concepts

### 6.1 Probability Space (pages 172–178)

The formal foundation of probability has three parts:
1. **Sample space Ω** — all possible outcomes. (Coin: {heads, tails})
2. **Events** — subsets of outcomes we care about. ("Heads" is an event)
3. **Probability measure P** — a function assigning numbers to events (between 0 and 1)

**Rules every probability must follow:**
- P(anything) ≥ 0
- P(everything) = 1
- P(A or B) = P(A) + P(B) if A and B can't both happen

---

### 6.2 Discrete and Continuous Probabilities (pages 178–183)

**Discrete:** Countable outcomes (dice: 1,2,3,4,5,6)
- Use a **probability mass function (PMF)**: P(X = k)

**Continuous:** Uncountable outcomes (height in cm: any real number)
- Use a **probability density function (PDF)**: p(x)
- The probability of being in a range: P(a ≤ X ≤ b) = ∫[a to b] p(x) dx

**Important:** For continuous distributions, P(X = exactly 5.000) = 0. Only intervals have non-zero probability!

**CDF (Cumulative Distribution Function):** P(X ≤ x) — the area under the PDF up to x.

---

### 6.3 Sum Rule, Product Rule, and Bayes' Theorem (pages 183–186)

These three rules are the entire foundation of probabilistic reasoning.

**Sum rule (marginalisation):**
```
p(x) = ∑ p(x, y)   [discrete]
p(x) = ∫ p(x, y) dy  [continuous]
```
"Get the probability of X by summing over all possible values of Y."

**Product rule (chain rule of probability):**
```
p(x, y) = p(y | x) · p(x)
```
"The probability of X and Y is: probability of X, times probability of Y given X."

**Bayes' Theorem:** (the most important formula in this chapter)
```
p(θ | x) = p(x | θ) · p(θ) / p(x)
```

| Term | Name | Plain meaning |
|------|------|---------------|
| p(θ\|x) | Posterior | What I believe AFTER seeing data |
| p(x\|θ) | Likelihood | How probable is the data if θ is true? |
| p(θ) | Prior | What I believed BEFORE seeing data |
| p(x) | Evidence | How probable is the data overall? |

**Analogy:** You wake up and find the grass is wet. Is it because it rained (θ = rain) or because the sprinkler ran (θ = sprinkler)?
- Prior: historically it rains 70% of nights
- Likelihood: if it rained, grass is wet 90% of the time
- Posterior: given the wet grass, what's the probability it rained?

Bayes' theorem combines prior knowledge with observed evidence.

---

### 6.4 Summary Statistics and Independence (pages 186–197)

**Mean (Expected Value):**
```
E[X] = ∑ x · p(x)    [discrete]
E[X] = ∫ x · p(x) dx  [continuous]
```
The "center of mass" of a distribution.

**Variance:**
```
Var[X] = E[(X - E[X])²] = E[X²] - (E[X])²
```
How "spread out" the distribution is. Standard deviation = √Var[X].

**Covariance:**
```
Cov[X, Y] = E[(X - E[X])(Y - E[Y])]
```
Positive: X and Y tend to be large/small together.
Negative: When X is large, Y tends to be small.
Zero: X and Y are uncorrelated.

**Independence:** X and Y are independent if:
```
p(x, y) = p(x) · p(y)
```
Knowing X tells you nothing about Y.

---

### 6.5 Gaussian Distribution (pages 197–205)

**The most important distribution in all of ML.**

```
p(x) = (1 / √(2πσ²)) · exp(-(x - μ)² / 2σ²)
```

Parameters:
- μ (mu) = mean (center)
- σ² (sigma squared) = variance (spread)

**Why the Gaussian is everywhere:**
- **Central Limit Theorem:** The average of many independent random things → Gaussian, regardless of their individual distributions.
- Nature loves it: heights, measurement errors, noise are all approximately Gaussian.
- Math is nice: sum of Gaussians = Gaussian.

**Multivariate Gaussian** (for vectors):
```
p(x) = (1 / |2πΣ|^(1/2)) · exp(-½ (x - μ)ᵀ Σ⁻¹ (x - μ))
```
- μ = mean vector
- Σ = covariance matrix (shape of the "cloud")

---

### 6.6 Conjugacy and the Exponential Family (pages 205–214)

**Conjugate prior:** A prior that, when combined with a likelihood via Bayes' theorem, gives a posterior of the same family.

**Example:** Gaussian prior + Gaussian likelihood → Gaussian posterior. Beautiful!

The **exponential family** is a general form that includes Gaussian, Bernoulli, Poisson, and many others. It has nice mathematical properties for optimization.

---

### 6.7 Change of Variables (pages 214–221)

If X has distribution p_X, and Y = f(X), what is the distribution of Y?

```
p_Y(y) = p_X(f⁻¹(y)) · |df⁻¹/dy|
```

The `|df⁻¹/dy|` term (Jacobian determinant) accounts for stretching/squishing by f.

**Why it matters:** Normalizing flows (a type of deep generative model) are built entirely on this idea.

---

## Why This Matters for ML

| Concept | ML application |
|---------|---------------|
| Bayes' theorem | Bayesian ML, naive Bayes classifier, posterior inference |
| Gaussian distribution | Gaussian processes, variational autoencoders, noise modeling |
| Expectation/variance | Understanding model predictions and uncertainty |
| Independence | Simplifying probabilistic models (Naive Bayes assumption) |
| Change of variables | Normalizing flows, reparameterization trick in VAEs |

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 172–183 | Probability spaces + discrete vs continuous |
| Day 2 | 183–186 | Sum rule, product rule — write them from memory 5 times |
| Day 3 | 183–186 | Bayes' theorem — work through 2 concrete examples |
| Day 4 | 186–197 | Mean, variance, covariance, independence |
| Day 5 | 197–205 | Gaussian distribution — sketch it, understand μ and σ |
| Day 6 | 205–221 | Exponential family + change of variables |
| Day 7 | — | Exercises 6.1–6.6 |
| Day 8 | — | Review: explain Bayes' theorem to yourself with a story |

---

## Self-Check Questions

1. What is a probability density function (PDF)? How does it differ from a PMF?
2. State Bayes' theorem and name each term.
3. What is the mean and variance of a Gaussian N(3, 4)?
4. What does it mean for two random variables to be independent?
5. If X ~ N(0,1) and Y = 2X + 3, what distribution does Y follow?
6. Why is the Gaussian distribution so ubiquitous?

---

## Intuition Checkpoint

> **Probability is always between 0 and 1.**
> **Uncertainty is not ignorance — it's quantified knowledge about what we don't know.**
> The whole point of probability in ML: instead of saying "I don't know," we say "I'm 73% confident it's a cat."
