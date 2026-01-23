---
title: Array Operations
---
# Array Operations

## The Superpower: Math Without Loops

In the previous page, you learned to create arrays. Now let's see why they're so powerful.

Say you have temperature readings from 1000 sensors and need to convert them all from Celsius to Fahrenheit. With a list, you'd write a loop:

```python
temps_c = [20.0, 21.5, 19.8, ...]  # 1000 values
temps_f = []
for t in temps_c:
    temps_f.append(t * 9/5 + 32)
```

With NumPy, you just write the formula:

```python
import numpy as np

temps_c = [20.0, 21.5, 19.8, ...]  # 1000 values
temps_c = np.array(temps_c)  # convert your list to an array
temps_f = temps_c * 9/5 + 32  # Done. All 1000 converted.
```

One line. No loop. And it runs about 100x faster.

This is called **vectorization**: the operation applies to every element automatically. It's not just convenient; it's how you'll write every formula in this course.

---

## All the Math Operators Work

You can use `+`, `-`, `*`, `/`, and `**` directly on arrays:

```python
import numpy as np

list1 = [1, 2, 3, 4]
list2 = [10, 20, 30, 40]
a = np.array(list1)     # convert both lists to array
b = np.array(list2)

print(a + b)
print(a * b)      #   (element-by-element, not matrix multiply!)
print(a ** 2) 
```
Output:
```
[11 22 33 44]
[10 40 90 160]
[1 4 9 16]
```

Notice that `a * b` multiplies each pair of elements. This is exactly what you want when you write formulas like $F = ma$ where both $m$ and $a$ are arrays.

---

## Functions Work on Entire Arrays Too

What if you need $\sin(x)$ for 100 different x-values? NumPy has versions of all the math functions:

```python
import numpy as np

x = np.linspace(0, 2*np.pi, 5)
print("x    =", x)
print("sin(x) =", np.sin(x))
```

Output:
```
x     = [0.         1.57079633 3.14159265 4.71238898 6.28318531]
sin(x) = [ 0.  1.  0. -1. -0.]
```

Use `np.sin`, `np.cos`, `np.exp`, `np.log`, `np.sqrt` instead of the `math` module versions. They work on arrays; the `math` versions don't.

---

## Putting It Together: A Real Formula

Let's see this in action with the falling parachutist. The analytical solution is:

$$v(t) = \frac{gm}{c}\left(1 - e^{-\frac{c}{m}t}\right)$$

Instead of computing this one time value at a time, we compute it for many times at once:

```python
import numpy as np

g, m, c = 9.8, 68.1, 12.5       # Yes, you can write many variable and assign them values in a sinlge line! Just keep them comma separated.
t = np.array([0, 2, 4, 6, 8, 10])

v = (g * m / c) * (1 - np.exp(-c/m * t))

print("Time (s):    ", t)
print("Velocity (m/s):", np.round(v, 2))
```

Output:
```
Time (s):     [ 0  2  4  6  8 10]
Velocity (m/s): [ 0.   16.42 27.77 35.64 41.1  44.87]
```

The formula looks almost identical to the math. No loops, no indexing. This is how you'll implement numerical methods.

---

## Getting a Single Number: Sum, Mean, Max

Sometimes you need to reduce an array to a single value. For example, computing the average temperature or finding the maximum error:

```python
import numpy as np

data = np.array([3.2, 4.1, 2.8, 5.0, 3.9])

print(f"Sum:  {np.sum(data)}")   # 19.0
print(f"Mean: {np.mean(data)}")  # 3.8
print(f"Max:  {np.max(data)}")   # 5.0
print(f"Min:  {np.min(data)}")   # 2.8
```

You'll use these constantly when checking convergence or computing errors:

```python
errors = np.abs(numerical - exact)
max_error = np.max(errors)
print(f"Maximum error: {max_error}")
```

---

## Slicing: Accessing Neighbors

Now here's a pattern that's essential for finite differences. In PDEs, you need to access the left neighbor, current point, and right neighbor of every interior point.

Look at this array of temperatures along a rod:

```python
T = np.array([100, 80, 60, 40, 20, 0])
#              0    1   2   3   4   5  (indices)
```

With slicing, you can grab different parts:

```python
print(T[1:-1])   # Interior points: [80 60 40 20]
print(T[:-2])    # Left neighbors:  [100 80 60 40]
print(T[2:])     # Right neighbors: [60 40 20 0]
```

Why does this matter? The heat equation update formula is:

$$T_i^{new} = T_i + \lambda(T_{i-1} - 2T_i + T_{i+1})$$

With slicing, you write this as one line:

```python
lam = 0.4
T_new = T.copy()
T_new[1:-1] = T[1:-1] + lam * (T[:-2] - 2*T[1:-1] + T[2:])
```

This updates all interior points at once. No loop. You'll learn more when we cover PDEs, but the key idea is: slicing lets you express the math directly.

---

## Solving Linear Systems (Preview)

Later in the course, you'll solve systems of equations like:
- $4x - y = 1$
- $-x + 3y = 5$

NumPy can solve these directly:

```python
import numpy as np

A = np.array([[4, -1],
              [-1, 3]])
b = np.array([1, 5])

x = np.linalg.solve(A, b)
print(f"Solution: x = {x[0]:.4f}, y = {x[1]:.4f}")
```

Output:
```
Solution: x = 0.7273, y = 1.9091
```

You'll learn *how* Gauss elimination works later. For now, just know the tool exists.

---

## Quick Reference

| What you want | Code |
|---------------|------|
| Add arrays | `a + b` |
| Multiply by scalar | `a * 3` |
| Element-wise multiply | `a * b` |
| Power | `a ** 2` |
| Sum all elements | `np.sum(a)` |
| Mean | `np.mean(a)` |
| Max / Min | `np.max(a)`, `np.min(a)` |
| Absolute value | `np.abs(a)` |
| Trig / Exp / Log | `np.sin(a)`, `np.exp(a)`, `np.log(a)` |
| Solve Ax = b | `np.linalg.solve(A, b)` |

---

## What's Next?

You now have the core NumPy skills for numerical methods:
- Create arrays of any size
- Do math on entire arrays at once
- Access slices for neighbor operations

As you progress through the course, you'll use these patterns for:
- **Euler's method**: update velocity array each timestep
- **Finite differences**: use slicing for neighbor access  
- **Linear systems**: set up and solve matrix equations

For additional utilities like reshaping, random numbers, and sorting, see [Useful Functions](useful_functions.md).
