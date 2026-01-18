---
title: Variables & Operators
---

# Variables & Operators

## Stop Retyping Numbers

Let's say you're computing the velocity of a falling parachutist at different times. The formula from the textbook is:

$$v(t) = \frac{gm}{c} \left( 1 - e^{-\frac{c}{m}t} \right)$$

You could type `9.8 * 68.1 / 12.5 * (1 - 2.71828**(-12.5/68.1 * 2))` every time. But what if you want to try a different mass? Or compute velocity at 10 different times? You'd be retyping numbers everywhere, and making mistakes.

**Variables** let you store values once and reuse them. Change `mass = 68.1` to `mass = 80.0`, and every calculation updates automatically. That's the power of variables.

---

## Variables

Variables store values for later use. Think of them as labeled containers.

To create a variable, use `name = value`. To use it later, just write its name (no quotes). To update it, assign a new value to the same name.

```python
temperature = 298.15
pressure = 101.325
volume = 0.0224

print(temperature)              # Prints: 298.15

temperature = temperature + 10  # Updates to 308.15
print(temperature)              # Prints: 308.15
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
print(a // b)  # Integer division: 3 (drops the decimal)
print(a % b)   # Modulo: 1 (remainder of 10 / 3)
print(a ** b)  # Power: 1000 (10^3)
```

### Comparison Operators

These return `True` or `False` (boolean values). Used in if statements and loops.

```python
x = 5
y = 10

print(x == y)  # Equal? 5 == 10 is False
print(x != y)  # Not equal? 5 != 10 is True
print(x < y)   # Less than? 5 < 10 is True
print(x >= y)  # Greater or equal? 5 >= 10 is False

# Common mistake: = vs ==
# x = 5    means "assign 5 to x"
# x == 5   means "is x equal to 5?"
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

Continue to [The print() Function](print.md) to learn how to display output.
