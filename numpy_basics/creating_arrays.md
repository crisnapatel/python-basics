---
title: Creating Arrays
---
# Creating Arrays

## From Lists to Arrays

The simplest way to create a NumPy array is from a Python list:

```python
import numpy as np

# From a list
arr = np.array([1, 2, 3, 4, 5])
print(arr)
print(type(arr))
```

Output:
```
[1 2 3 4 5]
<class 'numpy.ndarray'>
```

## Arrays of Zeros and Ones

When setting up numerical methods, you often need arrays initialized to zero (for accumulating results) or one (for certain algorithms):

```python
import numpy as np

# Array of 10 zeros
zeros = np.zeros(10)
print(zeros)

# 3x3 matrix of ones
ones = np.ones((3, 3))
print(ones)
```

Output:
```
[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
[[1. 1. 1.]
 [1. 1. 1.]
 [1. 1. 1.]]
```

## Creating Grids with linspace

For numerical methods, you constantly need evenly-spaced points. Use `linspace`:

```python
import numpy as np

# 11 points from 0 to 1 (inclusive)
x = np.linspace(0, 1, 11)
print(x)
```

Output:
```
[0.  0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1. ]
```

This is perfect for:
- **Finite differences**: Create a spatial grid with `n` points
- **Numerical integration**: Generate points where you evaluate the function
- **Plotting**: Create smooth x-values for your graphs

### Example: Setting Up a Spatial Grid

```python
import numpy as np

L = 1.0        # Domain length (meters)
n_points = 11  # Number of grid points

x = np.linspace(0, L, n_points)
dx = x[1] - x[0]  # Grid spacing

print(f"Grid points: {x}")
print(f"Grid spacing dx = {dx}")
```

Output:
```
Grid points: [0.  0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1. ]
Grid spacing dx = 0.1
```

## Creating Grids with arange

If you want to specify the step size instead of the number of points, use `arange`:

```python
import numpy as np

# From 0 to 1 with step 0.2
x = np.arange(0, 1.1, 0.2)  # Note: endpoint not included, so use 1.1
print(x)
```

Output:
```
[0.  0.2 0.4 0.6 0.8 1. ]
```

## 2D Arrays for PDEs

When solving partial differential equations, you need 2D grids:

```python
import numpy as np

# Temperature field on a 5x5 grid, initially all zeros
T = np.zeros((5, 5))

# Set boundary conditions
T[0, :] = 100   # Top edge = 100°C
T[-1, :] = 0    # Bottom edge = 0°C
T[:, 0] = 50    # Left edge = 50°C
T[:, -1] = 50   # Right edge = 50°C

print(T)
```

Output:
```
[[100. 100. 100. 100. 100.]
 [ 50.   0.   0.   0.  50.]
 [ 50.   0.   0.   0.  50.]
 [ 50.   0.   0.   0.  50.]
 [  0.   0.   0.   0.   0.]]
```

## Quick Reference

| Function | Purpose | Example |
|----------|---------|---------|
| `np.array([...])` | Create from list | `np.array([1, 2, 3])` |
| `np.zeros(n)` | n zeros | `np.zeros(10)` |
| `np.ones(n)` | n ones | `np.ones(5)` |
| `np.linspace(a, b, n)` | n points from a to b | `np.linspace(0, 1, 11)` |
| `np.arange(a, b, step)` | a to b with given step | `np.arange(0, 10, 0.5)` |
| `np.zeros((m, n))` | m×n matrix of zeros | `np.zeros((3, 4))` |
