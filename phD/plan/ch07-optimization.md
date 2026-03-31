# Chapter 7 — Continuous Optimization
> **Book pages:** 225–248 | **Time:** 1 week (5 study days)

---

## The Big Idea (explain it like I'm 10)

You're blindfolded on a hilly landscape. Your goal: find the lowest valley. What do you do? Feel the ground around your feet. Step in the direction that goes down. Repeat.

That's **gradient descent** — the algorithm that trains every neural network.

This chapter teaches you the math behind "find the best answer" — not just for hills, but for any mathematical function.

---

## Key Concepts

### 7.1 Optimization Using Gradient Descent (pages 227–233)

**The goal:** Find x* that minimizes f(x).

**The algorithm:**
```
x_{t+1} = x_t - α · ∇f(x_t)
```

- `x_t` = current position
- `∇f(x_t)` = gradient at current position (direction of steepest ascent)
- `α` (alpha) = **learning rate** = step size

**Why subtract the gradient?** Because we want to go *downhill*, and the gradient points *uphill*.

**Intuition for the learning rate:**
- Too big (α = 10): You overshoot and bounce around
- Too small (α = 0.00001): You take forever to converge
- Just right: You descend smoothly into the valley

**Variants:**
| Method | Description |
|--------|-------------|
| Batch gradient descent | Use all data for each step. Accurate but slow. |
| Stochastic gradient descent (SGD) | Use 1 data point per step. Fast but noisy. |
| Mini-batch gradient descent | Use a small batch (e.g., 32 points). The sweet spot. |

---

### When Does Gradient Descent Work?

A function has a **global minimum** if there's one single lowest point.
A function has **local minima** if there are multiple valleys (gradient descent might get stuck!).

**Convex functions** have only one valley — guaranteed to find the global minimum.
**Non-convex functions** (like neural networks) have many valleys — gradient descent finds a "good enough" local minimum.

---

### 7.2 Constrained Optimization and Lagrange Multipliers (pages 233–236)

Sometimes you want to minimize f(x) but x must satisfy a constraint: g(x) = 0.

**Example:** Minimize the surface area of a box with a fixed volume.

**Lagrange multipliers** turn a constrained problem into an unconstrained one:
```
L(x, λ) = f(x) + λ · g(x)
```

Find where the gradients align:
```
∇L = 0  →  ∇f(x) = -λ ∇g(x)
```

**Geometric intuition:** At the optimum, the gradient of f must be parallel to the gradient of g (the constraint boundary). If they're not parallel, you could slide along the constraint boundary to improve f.

**Why it matters in ML:** Support Vector Machines (Ch 12) are formulated as constrained optimization problems solved with Lagrange multipliers.

---

### 7.3 Convex Optimization (pages 236–246)

**Convex function:** A function where the line segment between any two points on the curve lies above (or on) the curve.

```
f(λx + (1-λ)y) ≤ λf(x) + (1-λ)f(y)   for λ ∈ [0,1]
```

**Why convexity is important:**
- Any local minimum = global minimum
- Gradient descent is guaranteed to find the optimal solution
- Many ML problems are convex (linear regression, logistic regression, SVMs)

**Convex sets:** A set S is convex if the line segment between any two points in S stays in S.
- Circle: convex ✓
- Crescent: not convex ✗

**Checking convexity:**
- Second derivative test: f is convex if f''(x) ≥ 0 everywhere (for 1D)
- Hessian test: f is convex if H(x) is positive semidefinite everywhere (for nD)

**Common convex functions to remember:**
- Any linear function f(x) = ax + b
- f(x) = x² (parabola)
- f(x) = eˣ (exponential)
- f(x) = -ln(x) (negative log, for x > 0)

---

## Why This Matters for ML

| Concept | ML application |
|---------|---------------|
| Gradient descent | Training all neural networks |
| Learning rate | Hyperparameter tuning |
| Convexity | Guarantees for logistic regression, SVMs |
| Lagrange multipliers | SVM formulation (Chapter 12) |
| Local vs global minima | Understanding why deep networks "just work" |

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 225–233 | Gradient descent — implement it mentally on f(x) = x² |
| Day 2 | 233–236 | Lagrange multipliers — work through one example |
| Day 3 | 236–246 | Convex functions and sets |
| Day 4 | — | Exercises 7.1–7.5 |
| Day 5 | — | Review: where do gradient descent, Lagrange, and convexity each appear in ML? |

---

## Self-Check Questions

1. Write the gradient descent update rule from memory.
2. What happens if the learning rate is too large? Too small?
3. What is a convex function? Draw one and a non-convex one.
4. What is the Lagrangian? Why do we introduce λ?
5. Why is convex optimization "easy" compared to non-convex?
6. Where in deep learning training does the gradient appear?

---

## The Three Ideas That Power All of Modern AI

```
1. Loss function L(θ)       — measure how wrong the model is
2. Gradient ∇_θ L           — find the direction to improve
3. Update: θ ← θ - α∇_θ L  — take a step toward better
```

Everything in Chapters 5 and 7 exists to make these three lines rigorous and efficient.
