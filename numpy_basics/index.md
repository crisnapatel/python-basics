---
title: NumPy Basics
---
# NumPy Basics

## Why Do I Need This?

You've been using Python lists, and they work fine for small things. But try running Euler's method with 10,000 timesteps:

```python
# With lists: slow and painful
velocities = [0.0] * 10000
for i in range(1, 10000):
    velocities[i] = velocities[i-1] + 0.1 * some_formula
```

Now imagine doing this for a 2D grid with 1 million points. Lists will take forever.

**NumPy arrays are built for this.** They're:
- 10-100x faster than lists for numerical operations
- Designed for mathematical formulas (no loops needed!)
- The foundation of all scientific Python

If you're solving differential equations, processing data, or doing any serious computation, you'll use NumPy. It's not optional.

---

## What You'll Learn

### [Creating Arrays](creating_arrays.md)
How to make arrays of zeros, evenly-spaced grids, and 2D matrices. These are the building blocks for every numerical method.

### [Array Operations](operations.md)
The superpower: doing math on entire arrays at once. Write formulas that apply to thousands of values without a single loop.

### [Useful Functions](useful_functions.md)
A reference for common tasks: checking array shape, reshaping, random numbers, sorting, searching, and more.
