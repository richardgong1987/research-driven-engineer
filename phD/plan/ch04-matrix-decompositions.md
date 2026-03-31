# Chapter 4 — Matrix Decompositions
> **Book pages:** 98–138 | **Time:** 1.5 weeks (8 study days)

---

## The Big Idea (explain it like I'm 10)

You know how 12 = 2 × 2 × 3? We **factored** 12 into simpler pieces. Matrix decomposition does the same thing — but for matrices.

Why? Because a matrix might look complicated, but when you break it into simpler pieces, you can:
- Understand what it *does* geometrically (stretch? rotate? squish?)
- Solve equations involving it much faster
- Compress it (throw away unimportant pieces)

---

## Key Concepts

### 4.1 Determinant and Trace (pages 99–105)

**Determinant** = a single number that tells you how much a matrix scales volumes.

For a 2×2 matrix:
```
A = [a  b]     det(A) = ad - bc
    [c  d]
```

**Intuition:**
- det = 1: The transformation preserves size (like a rotation)
- det = 2: Doubles the area
- det = 0: The transformation squishes everything flat (matrix is "singular" — no inverse!)
- det < 0: The transformation also flips orientation (like a mirror)

**Trace** = sum of the diagonal elements.
```
tr(A) = a₁₁ + a₂₂ + ... + aₙₙ
```
The trace equals the sum of eigenvalues (important for later!).

---

### 4.2 Eigenvalues and Eigenvectors (pages 105–114)

This is one of the most important concepts in the whole book. Read it slowly.

**The big question:** Is there a special direction (vector) that a matrix doesn't rotate — only stretches?

**Answer:** Yes! These are **eigenvectors**. The amount of stretching is the **eigenvalue**.

**Definition:**
```
Av = λv
```
- v = eigenvector (the special direction)
- λ (lambda) = eigenvalue (the stretching factor)
- A = the matrix

**Analogy:** Imagine kneading dough. Some directions get stretched a lot. Some barely change. The "barely change" and "stretch a lot" directions are the eigenvectors. The stretch amounts are the eigenvalues.

**How to find eigenvalues:**
Solve `det(A - λI) = 0` — this is called the "characteristic equation."

**Example (2×2):**
```
A = [2  1]
    [0  3]

det(A - λI) = det([2-λ  1  ]) = (2-λ)(3-λ) - 0 = 0
                   [0   3-λ]

→ λ₁ = 2, λ₂ = 3
```

**Why it matters:** Eigendecomposition reveals the "natural axes" of a transformation. PCA, SVD, and many other algorithms are built on this.

---

### 4.3 Cholesky Decomposition (pages 114–115)

For **symmetric positive definite (SPD) matrices**, we can write:
```
A = LL⊤
```
where L is a lower triangular matrix (zeros above the diagonal).

**Analogy:** Like taking the square root of a matrix. If A = LL⊤, then L is a kind of "square root."

**Why it matters:** Much faster and more numerically stable than general matrix inversion. Used heavily in probability/statistics (covariance matrices are SPD).

---

### 4.4 Eigendecomposition and Diagonalization (pages 115–119)

If a matrix A has n linearly independent eigenvectors, we can write:
```
A = PDP⁻¹
```
Where:
- P = matrix of eigenvectors (columns)
- D = diagonal matrix of eigenvalues

**Why this is powerful:**
- Computing Aⁿ (matrix to the nth power) becomes trivial: `Aⁿ = PDⁿP⁻¹`
- Dⁿ is just each diagonal raised to the nth power — trivial!

**Limitation:** Not all matrices can be diagonalized. And it only works for square matrices. SVD (next section) is the universal version.

---

### 4.5 Singular Value Decomposition — SVD (pages 119–129)

**The most important decomposition in machine learning.**

Any matrix A (even non-square!) can be written as:
```
A = UΣV⊤
```
Where:
- U = left singular vectors (orthonormal — like eigenvectors of AA⊤)
- Σ = diagonal matrix of **singular values** (always non-negative)
- V = right singular vectors (orthonormal — like eigenvectors of A⊤A)

**Geometric meaning:** Any linear transformation can be broken into 3 steps:
1. Rotate (V⊤)
2. Scale along axes (Σ)
3. Rotate again (U)

**Why SVD matters in ML:**
- **Data compression:** Keep only the top k singular values → approximate A with much less data
- **PCA** is secretly SVD
- **Recommendation systems** use SVD
- **Image compression** uses SVD

---

### 4.6 Matrix Approximation (pages 129–134)

Using SVD, we can build the **best rank-k approximation** of any matrix:
```
Aₖ = σ₁u₁v₁⊤ + σ₂u₂v₂⊤ + ... + σₖuₖvₖ⊤
```

Each term is a "layer" of information. The singular values σ₁ ≥ σ₂ ≥ ... tell you how important each layer is.

**Analogy:** Imagine a detailed painting. Layer 1 is the rough outline. Layer 2 adds color blocks. Layer 3 adds details. If you stop at layer 5 out of 100, you get a blurry but recognizable version. That's low-rank approximation!

---

## Why This Matters for ML

| Concept | ML application |
|---------|---------------|
| Eigenvalues/eigenvectors | PCA, spectral clustering, graph neural networks |
| SVD | Matrix factorization (recommendation systems), PCA, compression |
| Determinant | Probability densities, solving linear systems |
| Cholesky | Gaussian processes, Kalman filters, efficient sampling |
| Low-rank approx | Reducing model size, noise removal |

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 99–105 | Determinant and trace |
| Day 2 | 105–114 | Eigenvalues — work through the examples by hand |
| Day 3 | 114–119 | Cholesky + eigendecomposition |
| Day 4 | 119–129 | SVD — **read twice, it's dense** |
| Day 5 | 129–138 | Matrix approximation + matrix phylogeny |
| Day 6 | — | Exercises 4.1–4.5 |
| Day 7 | — | Exercises 4.6–4.10 |
| Day 8 | — | Review: explain SVD using the "rotate-scale-rotate" analogy |

---

## Self-Check Questions

1. What does a determinant of 0 tell you about a matrix?
2. Define eigenvector and eigenvalue. Give a physical analogy.
3. What is the characteristic equation, and how do you use it?
4. Write out the SVD decomposition in words: what do U, Σ, V each represent?
5. How would you use SVD to compress an image?
6. What is the difference between eigendecomposition and SVD?

---

## Memory Aid

> **"SVD is eigendecomposition for adults."**
> Eigendecomposition only works on square matrices. SVD works on anything.
> SVD is like the Swiss Army knife of matrix decompositions.
