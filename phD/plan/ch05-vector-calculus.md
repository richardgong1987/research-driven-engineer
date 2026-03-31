# Chapter 5 — Vector Calculus
> **Book pages:** 139–171 | **Time:** 1 week (5 study days)

---

## The Big Idea (explain it like I'm 10)

Imagine you're lost on a hilly island and you want to reach the lowest valley. You look around and find the direction that goes downhill the fastest, then take a step. Repeat. That's **gradient descent** — the engine of all modern ML training.

But to do that, you need to know the "downhill direction" — the **gradient**. This chapter teaches you how to compute gradients for functions involving vectors and matrices.

---

## Key Concepts

### 5.1 Differentiation of Univariate Functions (pages 141–146)

First, a refresher on single-variable calculus.

**Derivative** = the slope of a function at a point = how fast it's changing.

```
df/dx = lim[h→0] (f(x+h) - f(x)) / h
```

**Key rules you must know:**
| Rule | Formula |
|------|---------|
| Power rule | d/dx [xⁿ] = nxⁿ⁻¹ |
| Product rule | d/dx [f·g] = f'g + fg' |
| Chain rule | d/dx [f(g(x))] = f'(g(x)) · g'(x) |
| Exponential | d/dx [eˣ] = eˣ |
| Log | d/dx [ln x] = 1/x |

**The chain rule is the most important for ML** — neural networks are chains of functions!

---

### 5.2 Partial Differentiation and Gradients (pages 146–149)

When a function takes multiple inputs, we take **partial derivatives** — "how does output change when I wiggle just this one input?"

**Example:** f(x, y) = x² + 3xy

```
∂f/∂x = 2x + 3y   (treat y as constant)
∂f/∂y = 3x         (treat x as constant)
```

The **gradient** collects all partial derivatives into one vector:
```
∇f = [∂f/∂x, ∂f/∂y] = [2x + 3y, 3x]
```

**Intuition:** The gradient points in the direction of steepest ascent. To minimize f, go in the *opposite* direction: `-∇f`.

---

### 5.3 Gradients of Vector-Valued Functions (pages 149–155)

When a function outputs a vector (not just a single number), the collection of all partial derivatives forms a matrix called the **Jacobian**.

```
f: ℝⁿ → ℝᵐ

Jacobian J = [ ∂fᵢ/∂xⱼ ]  (m × n matrix)
```

**Analogy:** The Jacobian tells you: "if I wiggle each input slightly, how much does each output change?"

If f maps 3 inputs to 2 outputs, J is a 2×3 matrix.

---

### 5.4 Gradients of Matrices (pages 155–158)

When the input to a function is a **matrix** (like weights in a neural network), the derivative becomes a higher-dimensional object.

The key concept: we can always "flatten" the matrix into a vector and use the Jacobian.

---

### 5.5 Useful Gradient Identities (pages 158–159)

Memorize these — they appear constantly in ML derivations:

```
∇ₓ (xᵀAx) = (A + Aᵀ)x       (if A symmetric: = 2Ax)
∇ₓ (aᵀx)  = a
∇ₓ (xᵀx)  = 2x
```

---

### 5.6 Backpropagation and Automatic Differentiation (pages 159–164)

**This is the algorithm that trains every neural network.**

**The problem:** A neural network is a big chain of functions. You need to compute the gradient of the loss with respect to every single weight. By hand, this would take forever.

**The solution:** The **chain rule** + smart bookkeeping.

Backpropagation computes gradients from output back to input, layer by layer. At each step, it applies the chain rule:
```
∂L/∂W₁ = ∂L/∂a₂ · ∂a₂/∂a₁ · ∂a₁/∂W₁
```

**Automatic differentiation (autograd)** = a program that applies backprop automatically. This is what PyTorch and TensorFlow do.

---

### 5.7 Higher-Order Derivatives (pages 164–165)

The derivative of a derivative is the **second derivative** — tells you curvature (is this a valley or a peak?).

For multi-variable functions, the matrix of second partial derivatives is the **Hessian**:
```
H = [ ∂²f / ∂xᵢ∂xⱼ ]
```

If H is positive definite at a point → local minimum.
If H is negative definite → local maximum.

---

### 5.8 Linearization and Taylor Series (pages 165–170)

Any smooth function can be approximated near a point x₀ by a polynomial:
```
f(x) ≈ f(x₀) + f'(x₀)(x - x₀) + ½f''(x₀)(x - x₀)² + ...
```

**Why it matters:** Many optimization algorithms (Newton's method) use the Taylor expansion to find better descent directions.

---

## Why This Matters for ML

| Concept | ML application |
|---------|---------------|
| Gradient | Direction to update model weights (gradient descent) |
| Jacobian | Propagating errors through neural network layers |
| Chain rule | Backpropagation algorithm |
| Hessian | Second-order optimizers (Newton's method, L-BFGS) |
| Taylor expansion | Understanding optimizer convergence |

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 141–148 | Review univariate derivatives + partial derivatives |
| Day 2 | 149–158 | Jacobian + gradient of matrices |
| Day 3 | 158–164 | Backpropagation — trace through a small example by hand |
| Day 4 | 164–170 | Hessian + Taylor series |
| Day 5 | — | Exercises 5.1–5.8 (pick 5). Focus on chain rule practice. |

---

## Self-Check Questions

1. What is the gradient of f(x, y) = x² + 2y²?
2. In one sentence, what does backpropagation compute?
3. What is the Jacobian? Give an example with dimensions.
4. If the Hessian at a point is positive definite, what does that mean?
5. Why is the chain rule the most important rule in deep learning?

---

## The Core Loop of ML Training (in 3 lines of calculus)

```
1. Forward pass:  ŷ = f(x; W)           // predict
2. Loss:          L = ‖ŷ - y‖²          // measure error
3. Backward pass: W ← W - α · ∇_W L    // update weights
```

Step 3 requires computing ∇_W L — that's what this entire chapter is about.
