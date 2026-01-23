---
title: Useful NumPy Functions
---
# Useful NumPy Functions

You now know how to create arrays and do math on them. This page covers additional functions you'll reach for regularly: checking array properties, reshaping, generating random numbers, sorting, and more.

Think of this as a reference you'll come back to when you need something specific.

---

## Checking Array Properties

When debugging or setting up a problem, you often need to know what you're working with:

```python
import numpy as np

T = np.array([[100, 80, 60],
              [50, 40, 30]])

print(T.shape)    # (2, 3) - 2 rows, 3 columns
print(T.size)     # 6 - total number of elements
print(T.ndim)     # 2 - number of dimensions
print(len(T))     # 2 - length of first dimension (number of rows)
```

The `shape` is especially important. When your code crashes with a "shape mismatch" error, this is how you figure out what went wrong.

---

## Reshaping Arrays

Sometimes you need to change the shape of an array without changing its data. This comes up when:
- Converting a 1D solution back to a 2D grid
- Preparing data for matrix operations
- Flattening a 2D array to 1D for easier processing

```python
import numpy as np

# Start with a 1D array
a = np.array([1, 2, 3, 4, 5, 6])

# Reshape to 2x3
b = a.reshape((2, 3))
print(b)
```

Output:
```
[[1 2 3]
 [4 5 6]]
```

You can also go the other way, flattening a 2D array to 1D:

```python
c = b.flatten()
print(c)  # [1 2 3 4 5 6]
```

:::{warning}
The total number of elements must stay the same. You can't reshape 6 elements into a 2×4 array.
:::

---

## Random Numbers

Random numbers are essential for:
- Testing your code with different inputs
- Monte Carlo simulations
- Adding noise to signals
- Initializing iterative methods with random guesses

### Uniform Random Numbers (0 to 1)

```python
import numpy as np

# 5 random numbers between 0 and 1
r = np.random.rand(5)
print(r)
```

Output (yours will differ):
```
[0.417 0.720 0.000 0.302 0.147]
```

### Random Integers

```python
# 10 random integers from 0 to 99
r = np.random.randint(0, 100, size=10)
print(r)
```

### Normal (Gaussian) Distribution

For simulating measurement noise or natural variation:

```python
# Mean = 0, Standard deviation = 1, 5 samples
r = np.random.randn(5)
print(r)

# Mean = 50, Standard deviation = 10, 100 samples
measurements = 50 + 10 * np.random.randn(100)
```

### Reproducible Random Numbers

For debugging, you want the same "random" numbers each time:

```python
np.random.seed(42)  # Any integer works
r = np.random.rand(5)
# Now r will be the same every time you run this
```

---

## Sorting

Sorting is useful for finding medians, percentiles, or organizing results:

```python
import numpy as np

data = np.array([3.2, 1.5, 4.8, 2.1, 3.9])

sorted_data = np.sort(data)
print(sorted_data)  # [1.5 2.1 3.2 3.9 4.8]
```

If you need the indices that would sort the array (useful for sorting one array based on another):

```python
indices = np.argsort(data)
print(indices)  # [1 3 0 4 2] - element 1 is smallest, then 3, etc.
```

---

## Finding Values

### Where Is a Condition True?

Find indices where a condition is met:

```python
import numpy as np

T = np.array([100, 80, 60, 40, 20])

# Where is T less than 50?
indices = np.where(T < 50)
print(indices)  # (array([3, 4]),) - indices 3 and 4

# Get the actual values
print(T[T < 50])  # [40 20]
```

This is useful for finding points where a solution exceeds a threshold or changes sign.

### Maximum and Minimum Locations

```python
data = np.array([3.2, 1.5, 4.8, 2.1])

print(np.argmax(data))  # 2 - index of maximum (4.8)
print(np.argmin(data))  # 1 - index of minimum (1.5)
```

---

## Combining Arrays

### Stacking Vertically or Horizontally

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Stack vertically (as rows)
v = np.vstack([a, b])
print(v)
```

Output:
```
[[1 2 3]
 [4 5 6]]
```

```python
# Stack horizontally (side by side)
h = np.hstack([a, b])
print(h)  # [1 2 3 4 5 6]
```

### Concatenating Along an Axis

For more control:

```python
c = np.concatenate([a, b])  # Same as hstack for 1D
print(c)  # [1 2 3 4 5 6]
```

---

## Copying Arrays

This is a common source of bugs. Watch carefully:

```python
import numpy as np

a = np.array([1, 2, 3])
b = a        # b is NOT a copy! It's the same array.
b[0] = 99
print(a)     # [99 2 3] - a changed too!
```

To make an independent copy:

```python
a = np.array([1, 2, 3])
b = a.copy()  # Now b is independent
b[0] = 99
print(a)      # [1 2 3] - a is unchanged
```

Always use `.copy()` when you want to modify an array without affecting the original.

---

## Iterating Over Arrays

Usually you should avoid loops with NumPy (use vectorization instead). But sometimes you need to iterate:

```python
import numpy as np

x = np.array([10, 20, 30])

# Simple iteration
for val in x:
    print(val)

# With index
for i, val in enumerate(x):
    print(f"x[{i}] = {val}")
```

For 2D arrays:

```python
T = np.array([[1, 2], [3, 4]])

# Iterate over rows
for row in T:
    print(row)

# Iterate over all elements
for val in T.flat:
    print(val)
```

But remember: if you can express it without a loop, do that instead. It's faster and cleaner.

---

## Quick Reference

| What you need | Code |
|---------------|------|
| Shape of array | `a.shape` |
| Number of elements | `a.size` |
| Number of dimensions | `a.ndim` |
| Reshape | `a.reshape((m, n))` |
| Flatten to 1D | `a.flatten()` |
| Random 0-1 | `np.random.rand(n)` |
| Random integers | `np.random.randint(low, high, size=n)` |
| Normal distribution | `np.random.randn(n)` |
| Set random seed | `np.random.seed(42)` |
| Sort | `np.sort(a)` |
| Indices that sort | `np.argsort(a)` |
| Where condition is true | `np.where(a > 0)` |
| Index of max/min | `np.argmax(a)`, `np.argmin(a)` |
| Stack vertically | `np.vstack([a, b])` |
| Stack horizontally | `np.hstack([a, b])` |
| Make a copy | `a.copy()` |

---

## What's Next?

You now have a solid foundation in NumPy. As you work through the course, you'll use these tools constantly:
- `shape` to debug dimension mismatches
- `reshape` to convert between 1D and 2D representations
- Random numbers for testing and Monte Carlo methods
- `where` to find points meeting specific conditions

When you encounter a new NumPy function in lecture code, you can look it up in the [NumPy documentation](https://numpy.org/doc/stable/reference/).
