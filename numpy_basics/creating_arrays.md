---
title: Creating Arrays
---
# Creating Arrays

## The Problem: You Need 1000 Numbers

Let's say you're simulating heat diffusion along a metal rod. You divide the rod into 100 segments, and you need to track the temperature at each point. That's 100 temperature values.

With Python lists, you might write:

```python
temperatures = [20.0, 20.0, 20.0, 20.0, ...]  # 100 times? No way.
```

Nobody wants to type that. And what if you need 10,000 points for accuracy? Or a million for a serious simulation?

NumPy gives you a simple solution:

```python
import numpy as np

temperatures = np.zeros(100)  # 100 zeros, instantly
```

That's it. One line, any size you want. Let's learn how this works.

---

## Your First Array

An array is like a list, but designed for numbers:

```python
import numpy as np

data = np.array([34, 82, -5, 8])
print(data)
```

Output:
```
[34 82 -5  8]
```

Notice there are no commas in the output. That's how you know it's a NumPy array, not a list.

### But why not just use a list?

For 5 numbers, a list is fine. But watch what happens when you try to do math:

```python
my_list = [1, 2, 3, 4, 5]
print(my_list * 2)  # [1, 2, 3, 4, 5, 1, 2, 3, 4, 5]  Oops! It repeated the list!

my_array = np.array([1, 2, 3, 4, 5])
print(my_array * 2)  # [2 4 6 8 10]  That's what we wanted!
```

Arrays understand math. Lists don't. This is the key difference, and it's why NumPy exists.

---

## Starting with Zeros

Now let's create that temperature array properly. At the start of our simulation, the rod is at 0°C everywhere:

```python
T = np.zeros(10)  # 10 points, all zero
print(T)
```

Output:
```
[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
```

The decimal points tell you these are floating-point numbers. That's what you want for temperatures, concentrations, and most physical quantities.

But wait. We have 10 temperature values, but where exactly on the rod are they located? We need to know the *positions* too.

---

## Creating a Grid of Positions with linspace

This is where `linspace` comes in. If your rod is 1 meter long, you want positions at 0, 0.1, 0.2, ..., 1.0 meters:

```python
x = np.linspace(0, 1, 11)  # 11 points from 0 to 1
print(x)
```

Output:
```
[0.  0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1. ]
```

Read this as: "Give me 11 points, evenly spaced, from 0 to 1."

### The Gotcha: Points vs Segments

This trips up everyone at first:
- 11 points means 10 segments (the gaps between points)
- 10 points means 9 segments

Think of a ruler: to measure 10 centimeters, you need marks at 0, 1, 2, ..., 10. That's 11 marks.

### Getting the Spacing

You'll often need the distance between adjacent points (called $h$ or $\Delta x$):

```python
x = np.linspace(0, 1, 11)
dx = x[1] - x[0]
print(f"Spacing: {dx}")  # 0.1
```

This `dx` appears in almost every finite difference formula.

---

## Okay, But How Do I Get a Specific Value?

Good question. Now that we have arrays, we need to access individual elements. This works just like lists:

```python
T = np.array([100, 80, 60, 40, 20])

print(T[0])    # First element: 100
print(T[-1])   # Last element: 20
print(T[2])    # Third element: 60
```

You can also grab a range of elements:

```python
print(T[1:4])
```
Outupt:
```
 Elements 1, 2, 3: [80 60 40]
```

### The Superpower: Change Multiple Elements at Once

Here's something lists can't do well. Let's say you want to set the middle three values to 75:

```python
T[1:4] = 75
print(T)
```

Output:
```
[100  75  75  75  20]
```

One line. No loop. This becomes essential for setting boundary conditions.

---

## 2D Arrays: When You Need a Grid

So far we've done 1D arrays (a line of points). But what about heat conduction on a *plate*? That's a 2D problem, and you need a 2D array.

```python
T = np.zeros((5, 5))  # 5 rows, 5 columns
print(T)
```

Output:
```
[[0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0.]
 [0. 0. 0. 0. 0.]]
```

Notice the double parentheses: `np.zeros((5, 5))`. The inner parentheses create a tuple `(5, 5)` that specifies the shape.

### Setting Boundary Conditions

Now the real power. In PDE problems, you often fix the temperature at the edges. Let's set the top edge to 100°C:

```python
T[0, :] = 100   # Row 0, all columns
print(T)
```

Output:
```
[[100. 100. 100. 100. 100.]
 [  0.   0.   0.   0.   0.]
 [  0.   0.   0.   0.   0.]
 [  0.   0.   0.   0.   0.]
 [  0.   0.   0.   0.   0.]]
```

The `:` means "all elements in this dimension." So `T[0, :]` means "row 0, every column." Similarly:
- `T[-1, :]` is the bottom row
- `T[:, 0]` is the left column
- `T[:, -1]` is the right column

---

## Quick Reference

| What you want | Code |
|---------------|------|
| Array from list | `np.array([1, 2, 3])` |
| n zeros | `np.zeros(n)` |
| n ones | `np.ones(n)` |
| n points from a to b | `np.linspace(a, b, n)` |
| 2D grid of zeros | `np.zeros((rows, cols))` |
| First element | `x[0]` |
| Last element | `x[-1]` |
| Slice | `x[1:4]` |
| Row i, all columns | `T[i, :]` |
| All rows, column j | `T[:, j]` |

---

## Next Steps

You can now create arrays of any size and access their elements. But the real power of NumPy is doing math on entire arrays at once, without loops. That's what we'll learn in [Array Operations](operations.md).
