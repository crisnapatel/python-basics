---
title: Array Operations
---
# Array Operations

## Math on Entire Arrays at Once

With Python lists, you'd need a loop to add two lists element by element. With NumPy, mathematical operations automatically apply to every element—this is called *vectorization*.

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(a + b)        # Element-wise addition
print(a * 2)        # Multiply every element by 2
print(np.dot(a, b)) # Dot product
```

Output:
```
[5 7 9]
[2 4 6]
32
```

This is why NumPy is essential for numerical methods: you can express mathematical formulas directly without writing loops.
