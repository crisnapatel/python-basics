---
title: Variables & Operators
---

# Variables & Operators

## Variables

Variables store values for later use. Think of them as labeled containers.

```python
# Assigning values to variables
temperature = 298.15  # Kelvin
pressure = 101.325    # kPa
volume = 0.0224       # m³

# Variables can be updated
temperature = temperature + 10  # Now 308.15
```

### Naming Rules

| ✅ Valid | ❌ Invalid | Reason |
|---------|-----------|--------|
| `molar_mass` | `molar-mass` | No hyphens |
| `temp1` | `1temp` | Can't start with number |
| `_private` | `class` | Reserved keyword |
| `camelCase` | `my var` | No spaces |

## Operators

### Arithmetic Operators

```python
a = 10
b = 3

print(a + b)   # Addition: 13
print(a - b)   # Subtraction: 7
print(a * b)   # Multiplication: 30
print(a / b)   # Division: 3.333...
print(a // b)  # Integer division: 3
print(a % b)   # Modulo (remainder): 1
print(a ** b)  # Power: 1000
```

### Comparison Operators

Return `True` or `False`:

```python
x = 5
y = 10

print(x == y)  # Equal: False
print(x != y)  # Not equal: True
print(x < y)   # Less than: True
print(x >= y)  # Greater or equal: False
```

### Chemical Engineering Example

Calculate ideal gas volume:

```python
# PV = nRT
R = 8.314      # J/(mol·K)
T = 298.15     # K
P = 101325     # Pa
n = 1.0        # mol

V = (n * R * T) / P
print(f"Volume: {V:.4f} m³")  # Volume: 0.0245 m³
```

## Next Steps

Continue to [Control Flow](control_flow/index.md) to learn about conditionals and loops.
