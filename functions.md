---
title: Functions
---
# Functions

Reusable blocks of code.

```python
def ideal_gas_volume(n, T, P, R=8.314):
    """Calculate volume using ideal gas law."""
    return (n * R * T) / P

# Use the function
V = ideal_gas_volume(1.0, 298.15, 101325)
print(f"Volume: {V:.4f} m³")
```
