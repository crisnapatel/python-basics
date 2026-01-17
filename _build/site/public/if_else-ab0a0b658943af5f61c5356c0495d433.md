---
title: If/Else Statements
---

# If/Else Statements

Make your code take different paths based on conditions.

## Basic Syntax

```python
temperature = 373.15  # K

if temperature > 373.15:
    print("Water is vapor")
elif temperature == 373.15:
    print("Water is at boiling point")
else:
    print("Water is liquid (or solid)")
```

## Comparison Operators

| Operator | Meaning |
|----------|---------|
| `==` | Equal to |
| `!=` | Not equal to |
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal |
| `>=` | Greater than or equal |

## Combining Conditions

Use `and`, `or`, `not`:

```python
T = 300  # K
P = 101  # kPa

# Both conditions must be true
if T > 273 and P > 100:
    print("Above STP")

# Either condition is true
if T < 273 or P < 100:
    print("Below normal conditions")

# Negation
if not (T > 373):
    print("Not boiling")
```

## Chemical Engineering Example

Reaction feasibility check:

```python
delta_G = -50.2  # kJ/mol

if delta_G < 0:
    print("Reaction is spontaneous (favorable)")
elif delta_G == 0:
    print("Reaction is at equilibrium")
else:
    print("Reaction is non-spontaneous")
```

## Common Mistake

:::{warning}
Use `==` for comparison, not `=` (assignment)!
```python
# WRONG - This assigns, doesn't compare
if x = 5:  # SyntaxError!

# CORRECT
if x == 5:
    print("x is five")
```
:::
