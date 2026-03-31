# Chapter 2 — Linear Algebra
> **Book pages:** 17–69 | **Time:** 2 weeks (10 study days)

---

## The Big Idea (explain it like I'm 10)

Imagine you have a toy robot. You want to tell it where to go. You could say "go 3 steps right and 4 steps forward." That's a **vector** — a direction with a size.

Now imagine you want to spin and stretch the robot's world. Maybe you rotate it 45° and zoom in 2x. That transformation is a **matrix**.

Linear algebra is the math of **arrows (vectors)** and **transformation machines (matrices)**. Almost all data in machine learning is stored as vectors and matrices.

---

## Key Concepts

### 2.1 Systems of Linear Equations (pages 19–22)

**Simple version:** You have 2 unknowns and 2 clues. Like:
```
x + y = 5
x - y = 1
```
Solving this is what "solving a system of linear equations" means.

**Why it matters:** Training an ML model often reduces to solving millions of these equations simultaneously.

**Key insight:** A system can have:
- Exactly 1 solution (lines cross at one point)
- No solution (parallel lines never meet)
- Infinite solutions (same line)

---

### 2.2 Matrices (pages 22–27)

A matrix is just a rectangular table of numbers:

```
A = [ 1  2  3 ]
    [ 4  5  6 ]
```

This is a 2×3 matrix (2 rows, 3 columns).

**Operations:**
- **Addition:** Add matching cells. Like adding two spreadsheets.
- **Multiplication:** This is special! AB ≠ BA in general.
  - Think of it as: "apply transformation B first, then A."

**The identity matrix I** is like the number 1 for matrices: AI = IA = A.

---

### 2.3 Solving Systems (pages 27–35)

**Gaussian Elimination** — the main algorithm.

Think of it like this: you have a Sudoku puzzle. You use clues to eliminate options row by row. That's exactly what Gaussian elimination does — it simplifies the system until answers pop out.

Steps:
1. Write equations as an "augmented matrix" [A | b]
2. Swap rows, scale rows, add rows to each other
3. Get the matrix into "staircase" (row-echelon) form
4. Read off the answers from bottom to top

---

### 2.4 Vector Spaces (pages 35–40)

A **vector space** is a universe where:
- You can add any two vectors and stay in the universe
- You can scale any vector and stay in the universe

**Example:** All 2D arrows on a flat table form a vector space. You can add two arrows (tip to tail) and get another arrow on the table. You can make an arrow 3x longer and it's still on the table.

**Why this matters:** Feature spaces in ML are vector spaces. Your data lives in these universes.

---

### 2.5 Linear Independence (pages 40–44)

Vectors are **linearly independent** if none of them can be built from the others.

**Simple analogy:** Imagine you're giving directions. If I say "go North 3 blocks, go East 2 blocks, go NorthEast 1 block" — that third direction is redundant! North + East already covers NorthEast. It's linearly *dependent*.

**Why it matters:** Redundant features waste memory and cause problems in ML models.

---

### 2.6 Basis and Rank (pages 44–48)

A **basis** is the minimum set of independent vectors that can describe your whole space.

Think of it like LEGO bricks. With just a few basic shapes (1x1, 1x2, 2x2), you can build almost anything. Those basic shapes are a "basis."

- **Rank** of a matrix = number of independent directions it spans = how many "real" dimensions of information it contains.

---

### 2.7 Linear Mappings (pages 48–61)

A **linear mapping** is a function that:
1. Preserves addition: f(x + y) = f(x) + f(y)
2. Preserves scaling: f(cx) = c·f(x)

**Example:** Rotating a picture by 30° is a linear mapping. Stretching it 2x is a linear mapping. Every such transformation can be written as a matrix multiplication.

**Key formulas:**
- Matrix representation of a linear map depends on the **choice of basis**
- Changing basis = changing your "coordinate system" (like switching between GPS coordinates and local street addresses — same location, different description)

---

### 2.8 Affine Spaces (pages 61–63)

An affine space is like a vector space, but **shifted away from the origin**.

Think of it as: a vector space is a flat table centered at (0,0). An affine space is that same flat table slid over so it no longer passes through (0,0). Affine transformations = linear transformations + a shift.

---

## Why This Matters for ML

| Concept | Where it shows up in ML |
|---------|------------------------|
| Matrix multiplication | Every neural network layer: output = Wx + b |
| Linear independence | Feature selection — removing redundant inputs |
| Rank | Detecting if your data is really lower-dimensional |
| Basis change | PCA (Chapter 10) — find the "best" directions in data |
| Linear mappings | Every layer transformation in deep learning |

---

## Daily Breakdown

| Day | Pages | Focus |
|-----|-------|-------|
| Day 1 | 17–26 | Systems of equations + matrix basics |
| Day 2 | 27–34 | Gaussian elimination — practice 2 examples by hand |
| Day 3 | 35–44 | Vector spaces + linear independence |
| Day 4 | 44–60 | Basis, rank, linear mappings |
| Day 5 | 61–69 | Affine spaces + chapter exercises (pick 3–5) |
| Day 6–7 | — | Rest + review: re-derive key definitions from memory |
| Day 8 | Exercises | Do exercises 2.1–2.5 |
| Day 9 | Exercises | Do exercises 2.6–2.10 |
| Day 10 | Review | Self-check questions below. Identify weak spots. |

---

## Self-Check Questions

1. What is a vector? Give a real-world example.
2. How do you multiply two matrices? What does it geometrically mean?
3. What does it mean for 3 vectors to be linearly independent?
4. What is the rank of a matrix? Why does it matter?
5. What is the difference between a vector space and an affine space?
6. Can you explain Gaussian elimination in plain English?
7. What is a basis? How many vectors does ℝ³ need as a basis?

---

## Common Mistakes to Avoid

- **Matrix multiplication is NOT commutative:** AB ≠ BA in general!
- **Not every matrix has an inverse:** Only square, full-rank matrices do.
- **The zero vector is always in every vector space** — it's like the "do nothing" direction.
