---
title: Array Operations
---
# Array Operations

## Math on Entire Arrays at Once

With Python lists, you'd need a loop to add two lists element by element. With NumPy, mathematical operations automatically apply to every element. This is called *vectorization*.

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(a + b)        # Element-wise addition
print(a * 2)        # Multiply every element by 2
print(a * b)        # Element-wise multiplication
print(np.dot(a, b)) # Dot product
```

Output:
```
[5 7 9]
[2 4 6]
[4 10 18]
32
```

This is why NumPy is essential for numerical methods: you can express mathematical formulas directly without writing loops.

---

## Numerical Methods: Vectorized Finite Differences

Here's where NumPy really shines. In the explicit finite difference method for the heat equation, you need to update every interior point based on its neighbors:

$$T_i^{new} = T_i + \lambda (T_{i+1} - 2T_i + T_{i-1})$$

With loops, this would be:
```python
# Slow loop version
for i in range(1, n-1):
    T_new[i] = T[i] + lam * (T[i+1] - 2*T[i] + T[i-1])
```

With NumPy slicing, it's one line:
```python
# Fast vectorized version
T_new[1:-1] = T[1:-1] + lam * (T[2:] - 2*T[1:-1] + T[:-2])
```

Both do the same thing, but the NumPy version is much faster for large arrays.

### Understanding the Slicing

- `T[1:-1]` means "all elements except the first and last" (interior points)
- `T[2:]` means "all elements starting from index 2" (right neighbors)
- `T[:-2]` means "all elements except the last two" (left neighbors)

---

## Computing Errors

When comparing numerical results to exact solutions, you often need error norms:

```python
import numpy as np

y_exact = np.array([1.0, 2.0, 3.0, 4.0])
y_numerical = np.array([1.1, 1.9, 3.2, 3.8])

error = y_exact - y_numerical

# Maximum absolute error (L-infinity norm)
max_error = np.max(np.abs(error))

# Root mean square error
rms_error = np.sqrt(np.mean(error**2))

print(f"Max error: {max_error}")
print(f"RMS error: {rms_error:.4f}")
```

Output:
```
Max error: 0.2
RMS error: 0.1581
```

---

## Solving Linear Systems

For systems of linear equations $Ax = b$ (Gauss elimination, LU decomposition topics), NumPy provides a direct solver:

```python
import numpy as np

# System: 4x - y = 1
#        -x + 3y = 5

A = np.array([[4, -1],
              [-1, 3]])
b = np.array([1, 5])

x = np.linalg.solve(A, b)
print(f"Solution: x = {x}")
```

Output:
```
Solution: x = [0.72727273 1.90909091]
```

You'll learn *how* this works in the linear algebra section of the course. For now, know that NumPy can solve these systems efficiently.

---

## Mathematical Functions

NumPy provides versions of math functions that work on entire arrays:

```python
import numpy as np

x = np.linspace(0, 2*np.pi, 5)

print(f"x = {x}")
print(f"sin(x) = {np.sin(x)}")
print(f"exp(x) = {np.exp(x)}")
```

Output:
```
x = [0.         1.57079633 3.14159265 4.71238898 6.28318531]
sin(x) = [ 0.0000e+00  1.0000e+00  1.2246e-16 -1.0000e+00 -2.4493e-16]
exp(x) = [  1.           4.81047738  23.14069263 111.31777849 535.49165552]
```

---

## Quick Reference

| Operation | Syntax | Result |
|-----------|--------|--------|
| Add arrays | `a + b` | Element-wise sum |
| Scalar multiply | `a * 2` | Each element × 2 |
| Element-wise multiply | `a * b` | Each element × corresponding element |
| Dot product | `np.dot(a, b)` | Sum of a[i]*b[i] |
| Sum all elements | `np.sum(a)` | Single number |
| Mean | `np.mean(a)` | Average value |
| Max/Min | `np.max(a)`, `np.min(a)` | Largest/smallest |
| Absolute value | `np.abs(a)` | Element-wise |a[i]| |
| Solve Ax=b | `np.linalg.solve(A, b)` | Solution vector x |
