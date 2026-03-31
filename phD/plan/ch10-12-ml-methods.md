# Chapters 10, 11, 12 — PCA, GMM, and SVM
> **Book pages:** 317–394 | **Time:** 1 week (5 study days)

---

## Overview

These three chapters are the payoff for all your hard work. Each one takes a real ML problem and solves it using the math from Part I.

| Chapter | Algorithm | Core math used |
|---------|-----------|---------------|
| 10 | PCA — find structure in data | SVD, projections, eigenvalues |
| 11 | GMM — cluster data into groups | Gaussian distributions, Bayes' theorem |
| 12 | SVM — draw the best decision boundary | Optimization, Lagrange multipliers, inner products |

---

## Chapter 10 — Dimensionality Reduction with PCA

### The Big Idea (like I'm 10)

You have data with 1000 features. Most are redundant or noisy. PCA finds the **10 most important directions** in the data — the ones that capture the most variation — and projects everything onto those directions.

Like taking a photo of a 3D sculpture: you lose one dimension (depth), but capture the most important visual features.

### 10.1–10.3 Maximum Variance + Projection Perspective (pages 318–333)

**Goal:** Find a direction u₁ such that the projected data has maximum variance.

```
maximize  Var[Xu₁] = u₁ᵀ Su₁
subject to ‖u₁‖ = 1
```

Where S = (1/N) XᵀX is the **data covariance matrix**.

**Solution:** u₁ is the eigenvector of S with the largest eigenvalue!

The second principal component u₂ is the next eigenvector, and so on.

**The math chain:**
1. Compute covariance matrix S (Ch 6)
2. Find its eigenvectors/eigenvalues (Ch 4)
3. Project data onto top eigenvectors (Ch 3)

### 10.6 PCA in Practice

```
Step 1: Center the data: X ← X - mean(X)
Step 2: Compute SVD: X = UΣVᵀ
Step 3: Keep top k columns of V (principal components)
Step 4: Project: Z = XV_k  (low-dimensional representation)
```

### Why It Matters

- Visualize high-dimensional data in 2D/3D
- Remove noise (small eigenvalues = noise directions)
- Speed up downstream ML (fewer features)
- Compression (store k dimensions instead of D)

---

## Chapter 11 — Density Estimation with Gaussian Mixture Models (GMM)

### The Big Idea (like I'm 10)

You have a bag of colorful marbles. You don't know the rule, but you notice they cluster in 3 color groups. A GMM assumes the data comes from K Gaussian "blobs" mixed together.

**Goal:** Find the centers, shapes, and weights of the K blobs.

### 11.1 The Model (pages 349–350)

```
p(x) = ∑_k πₖ · N(x | μₖ, Σₖ)
```

- K = number of clusters
- πₖ = weight of cluster k (how many points belong to it)
- μₖ = center of cluster k
- Σₖ = shape (covariance) of cluster k

### 11.3 The EM Algorithm (pages 360–363)

**Expectation-Maximization (EM)** — the algorithm to fit GMMs.

**Problem:** We don't know which blob generated each data point.

**Solution:** Alternate between two steps:

**E-step (Expectation):** For each data point, compute the probability it came from each cluster.
```
rₙₖ = πₖ N(xₙ | μₖ, Σₖ) / ∑_j πⱼ N(xₙ | μⱼ, Σⱼ)
```

**M-step (Maximization):** Update the blob parameters using those probabilities.
```
μₖ_new = ∑_n rₙₖ xₙ / ∑_n rₙₖ
```

**Repeat** until the parameters stop changing.

**Analogy:** Imagine you're organizing a mess of emails by topic, but the topics aren't labeled.
- E-step: "Probably this email is 70% about sports, 30% about food"
- M-step: "Based on those guesses, here's what a sports email looks like"
- Repeat until stable

### Why It Matters

- Soft clustering (unlike k-means which forces hard assignments)
- Density estimation (learn the distribution of your data)
- Foundation for more complex generative models (VAEs)

---

## Chapter 12 — Classification with Support Vector Machines (SVM)

### The Big Idea (like I'm 10)

You have red and blue dots on a table. Draw a line to separate them. SVMs find the **widest possible gap** between the two groups — the most confident separator.

### 12.1 Separating Hyperplanes (pages 372–374)

A hyperplane in D dimensions: `wᵀx + b = 0`

Points on one side: `wᵀx + b > 0` (class +1)
Points on other side: `wᵀx + b < 0` (class -1)

### 12.2 Primal SVM (pages 374–383)

**Goal:** Find w and b to maximize the margin.

The **margin** = 2/‖w‖ (distance between the two support hyperplanes).

Maximizing margin = minimizing ‖w‖²:

```
minimize    ½ ‖w‖²
subject to  yₙ(wᵀxₙ + b) ≥ 1   for all n
```

This is a **quadratic program with linear constraints** — convex! (Ch 7)

### 12.3 Dual SVM (pages 383–388)

Using Lagrange multipliers (Ch 7), the primal problem converts to the dual:

```
maximize  ∑_n αₙ - ½ ∑_n ∑_m αₙαₘ yₙyₘ xₙᵀxₘ
subject to αₙ ≥ 0,   ∑_n αₙyₙ = 0
```

**Key insight:** The solution only depends on **inner products** xₙᵀxₘ between data points!

### 12.4 Kernels (pages 388–390)

Since we only need inner products, we can replace xₙᵀxₘ with a **kernel function** k(xₙ, xₘ):

```
k(x, x') = ⟨φ(x), φ(x')⟩
```

This implicitly maps data into a higher-dimensional space φ(x) where it becomes linearly separable — without actually computing φ!

**Popular kernels:**
- Linear: k(x, x') = xᵀx'
- RBF/Gaussian: k(x, x') = exp(-‖x - x'‖² / 2σ²)
- Polynomial: k(x, x') = (xᵀx' + c)^d

### Why It Matters

- SVMs work very well on small datasets
- The kernel trick enables non-linear classification
- The math is elegant and theoretically well-understood
- SVMs were state-of-the-art before deep learning

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 317–333 | PCA: maximum variance + projection perspective |
| Day 2 | 333–368 | PCA in practice + GMM model + EM algorithm |
| Day 3 | 368–383 | GMM latent variables + SVM primal formulation |
| Day 4 | 383–394 | SVM dual + kernels |
| Day 5 | — | Review all 4 algorithms: how does each connect back to Part I math? |

---

## The Grand Unified View

```
PCA:  Σ (covariance)  →  eigenvectors  →  project data
GMM:  EM algorithm    →  Bayes' rule   →  soft cluster data
SVM:  Lagrangian      →  dual problem  →  maximum margin classifier
LR:   Least squares   →  projection    →  best-fit line
```

Every algorithm in Part II is just Part I math applied cleverly to a specific problem.

---

## Self-Check Questions

1. What does PCA maximize? What math tool solves this?
2. What does the EM algorithm do in E-step vs M-step?
3. What is the "margin" in an SVM?
4. Why does the SVM dual formulation only require inner products?
5. What is a kernel, and why is it useful?
6. How are GMM and k-means clustering related?

---

## Congratulations!

If you reach this point and can answer all self-check questions in all guides, you have completed a **graduate-level mathematical foundation for machine learning**. You are now ready to read papers, understand PyTorch internals, and design your own ML methods.
