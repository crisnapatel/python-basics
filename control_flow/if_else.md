---
title: If/Else Statements
---

# If/Else Statements

## What If My Code Needs to Make Decisions?

Back to our parachutist. In the real problem, the drag coefficient **changes** when the parachute opens:
- Free-fall: c = 12.5 kg/s
- Parachute open: c = 68 kg/s (much more air resistance!)

The parachute opens after 5 seconds. How do you handle this in code?

```python
t = 7  # current time

if t < 5:
    c = 12.5   # free-fall
else:
    c = 68.0   # parachute deployed

print(f"At t={t}s, drag coefficient = {c} kg/s")
```

Without `if/else`, you'd need two completely separate programs: one for before the parachute opens, one for after. With `if/else`, your code adapts automatically.

---

## Basic Syntax

The structure is: `if CONDITION:` followed by indented code. Use `elif` (else if) for additional conditions, and `else` for the default case. Indentation matters!

```python
temperature = 373.15

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

Use `and`, `or`, `not` to combine multiple conditions.

- `and`: both conditions must be true
- `or`: at least one condition must be true  
- `not`: flips true to false (and vice versa)

```python
T = 300
P = 101

if T > 273 and P > 100:
    print("Above STP")

if T < 273 or P < 100:
    print("Below normal conditions")

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

## Numerical Methods Example: Quadratic Formula

When implementing the quadratic formula algorithm, you need to check for special cases:

```python
import math

a, b, c = 1, -5, 6  # coefficients of ax² + bx + c = 0

if a == 0:
    print("Not a quadratic equation (a cannot be 0)")
else:
    discriminant = b**2 - 4*a*c
    
    if discriminant > 0:
        x1 = (-b + math.sqrt(discriminant)) / (2*a)
        x2 = (-b - math.sqrt(discriminant)) / (2*a)
        print(f"Two real roots: {x1}, {x2}")
    elif discriminant == 0:
        x = -b / (2*a)
        print(f"One repeated root: {x}")
    else:
        print("Complex roots (discriminant < 0)")
```

Output:
```
Two real roots: 3.0, 2.0
```

This is exactly the kind of error checking you'll implement in numerical algorithms. You handle edge cases before they cause crashes.

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

## Next Steps

Now that your code can make decisions, it's time to learn repetition. Continue to [Loops](loops.md) to see how numerical methods use iteration to solve problems step by step.
