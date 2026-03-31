# Chapter 3 — Analytic Geometry
> **Book pages:** 70–97 | **Time:** 1 week (5 study days)

---

## The Big Idea (explain it like I'm 10)

In Chapter 2, we learned about arrows (vectors). Now we ask: **how long is an arrow? How far apart are two arrows? What angle is between them?**

This is geometry — but done with algebra. Instead of drawing pictures, we calculate distances, angles, and projections using numbers and formulas. This lets us work in 100-dimensional spaces where drawing is impossible!

---

## Key Concepts

### 3.1 Norms (pages 71–72)

A **norm** measures the **length** of a vector.

**The most familiar norm:** Euclidean norm (straight-line distance)
```
‖x‖ = √(x₁² + x₂² + ... + xₙ²)
```

This is just the Pythagorean theorem extended to many dimensions!

**For 2D:** If x = [3, 4], then ‖x‖ = √(9 + 16) = √25 = 5.

**Other norms exist too:**
- Manhattan norm (‖x‖₁): Add absolute values. Like walking city blocks.
- Max norm (‖x‖∞): Just the biggest absolute value.

**Why it matters:** In ML, norms measure "how wrong" a model is (the error/loss). Minimizing error = minimizing a norm.

---

### 3.2 Inner Products (pages 72–75)

The **inner product** (or dot product) of two vectors tells you **how much they point in the same direction**.

**Formula:**
```
⟨x, y⟩ = x⊤y = x₁y₁ + x₂y₂ + ... + xₙyₙ
```

**Simple example:** x = [1, 2], y = [3, 4]
```
⟨x, y⟩ = 1×3 + 2×4 = 3 + 8 = 11
```

**Intuition:**
- Large positive = vectors point mostly the same way
- Zero = vectors are perpendicular (they don't share any direction)
- Negative = vectors point in opposite directions

---

### 3.3 Lengths and Distances (pages 75–76)

The **length** of a vector x is: `‖x‖ = √⟨x, x⟩`

The **distance** between two vectors x and y is: `d(x, y) = ‖x - y‖`

**Analogy:** Imagine two cities on a map. The distance is the length of the "difference arrow" from one city to the other.

---

### 3.4 Angles and Orthogonality (pages 76–78)

The **angle** θ between two vectors:
```
cos(θ) = ⟨x, y⟩ / (‖x‖ · ‖y‖)
```

This is the generalized version of "cos = adjacent/hypotenuse" from high school.

**Orthogonal** = perpendicular = the inner product is zero:
```
⟨x, y⟩ = 0  →  x and y are orthogonal
```

**Why it matters in ML:** Orthogonality means "these two features carry independent information." When features are orthogonal, your model is much easier to train.

---

### 3.5 Orthonormal Basis (pages 78–79)

A basis where:
1. All vectors are **orthogonal** (perpendicular to each other)
2. All vectors have **length 1** (unit length)

**Example in 2D:** The standard x-axis [1, 0] and y-axis [0, 1] form an orthonormal basis.

**Why it's great:** Math becomes much simpler with orthonormal bases. Coordinates are easy to compute, and transformations preserve distances.

---

### 3.6 Orthogonal Complement (pages 79–80)

The **orthogonal complement** V⊥ of a space V is the set of all vectors perpendicular to everything in V.

**Analogy:** If V is the floor of a room, V⊥ is the vertical direction (pointing straight up). The floor and ceiling direction are perpendicular.

---

### 3.7 Inner Product of Functions (pages 80–81)

Inner products aren't just for vectors — they work for **functions** too!
```
⟨f, g⟩ = ∫ f(x)g(x) dx
```

**Why it matters:** This is used in Fourier analysis (breaking signals into frequencies) and kernel methods in ML.

---

### 3.8 Orthogonal Projections (pages 81–91)

**Projection** = shadow-casting! Imagine the sun shining straight down. Your shadow on the floor is the "projection" of your body onto the 2D floor.

Mathematically: project vector x onto vector b:
```
projection = (⟨x, b⟩ / ‖b‖²) · b
```

**Why it matters:** This is the heart of **PCA** (Chapter 10). PCA finds the direction to project data onto so that the projected data retains as much information (variance) as possible.

---

### 3.9 Rotations (pages 91–94)

A rotation matrix R rotates vectors without changing their length.

**In 2D:**
```
R(θ) = [ cos θ  -sin θ ]
        [ sin θ   cos θ ]
```

**Property:** R is **orthogonal**: R⊤R = I (rotating then un-rotating = nothing).

---

## Why This Matters for ML

| Concept | ML application |
|---------|---------------|
| Norms | Loss functions (MSE = squared L2 norm of errors) |
| Inner product | Similarity between data points (cosine similarity) |
| Angles | How "aligned" two feature vectors are |
| Projection | PCA, least squares regression |
| Orthonormal basis | Numerically stable algorithms, QR decomposition |

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 70–78 | Norms, inner products, lengths, angles |
| Day 2 | 78–87 | Orthonormal basis, projections (read carefully!) |
| Day 3 | 87–97 | Rotations + exercises 3.1–3.4 |
| Day 4 | — | Exercises 3.5–3.8 |
| Day 5 | — | Review: explain projection to yourself using a shadow analogy |

---

## Self-Check Questions

1. What is the Euclidean norm of [3, 4, 0]?
2. What does it mean for two vectors to be orthogonal?
3. How do you calculate the angle between [1, 0] and [1, 1]?
4. Describe orthogonal projection using a real-world analogy.
5. What is an orthonormal basis, and why is it useful?
6. Why does cos(θ) = ⟨x, y⟩ / (‖x‖ · ‖y‖) make sense geometrically?
