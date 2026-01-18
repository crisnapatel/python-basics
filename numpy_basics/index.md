---
title: NumPy Basics
---
# NumPy Basics

## Why Lists Aren't Enough

You've been using Python lists to store data, and they work great for small collections. But imagine you're running Euler's method with 10,000 timesteps, or processing sensor data with 1 million readings.

Try this with lists:

```python
# Slow: looping through lists
velocities = [0.0] * 10000
for i in range(1, 10000):
    velocities[i] = velocities[i-1] + 0.1
```

This works, but it's slow. NumPy does the same thing *much* faster:

```python
import numpy as np

# Fast: NumPy array operations
velocities = np.zeros(10000)
# Vectorized operations work on entire arrays at once
```

NumPy arrays are designed for numerical computing. They're faster, use less memory, and support mathematical operations that work on entire arrays at once.

:::{note}
If you're solving ODEs, processing experimental data, or doing any serious numerical work, you'll use NumPy. It's the foundation of scientific Python.
:::

## Topics
- [Creating Arrays](creating_arrays.md) — Making arrays from lists, generating sequences
- [Array Operations](operations.md) — Math on entire arrays at once
