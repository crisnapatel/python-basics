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

## Numerical Methods: Convergence Checking

Here's the pattern you'll use constantly in this course. Almost every iterative method—bisection, Newton-Raphson, Gauss-Seidel—needs to know when to stop. The answer? Check if the error is small enough:

```python
tolerance = 1e-6  # Stop when error is below this threshold

if abs(error) < tolerance:
    print("Converged! Solution found.")
else:
    print("Not yet. Keep iterating...")
```

This tiny snippet is the heart of numerical methods. You'll see it in nearly every algorithm we study. The tolerance (`1e-6` means $10^{-6}$, or 0.000001) controls how accurate your answer needs to be.

### Real Example: Stopping a Root-Finding Loop

In practice, you'll use this inside a loop. Here's the pattern:

```python
tolerance = 1e-6
max_iterations = 100

for iteration in range(max_iterations):
    # ... do some computation to get x_new ...
    
    error = abs(x_new - x_old)
    
    if error < tolerance:
        print(f"Converged after {iteration + 1} iterations!")
        break  # Exit the loop early
    
    x_old = x_new  # Prepare for next iteration
```

The `break` statement exits the loop immediately when convergence is achieved. Without it, you'd waste time on unnecessary iterations.

---

## Numerical Methods: Bracket Checking for Root Finding

Before starting the bisection method, you need to verify that your interval actually contains a root. The key insight: if a function changes sign between two points, there must be a root somewhere between them.

```python
f_a = f(a)  # Function value at left endpoint
f_b = f(b)  # Function value at right endpoint

if f_a * f_b < 0:
    print("Good bracket! A root exists between a and b.")
elif f_a * f_b > 0:
    print("Bad bracket. No sign change detected.")
else:
    print("Lucky! One endpoint is exactly a root.")
```

Why does `f_a * f_b < 0` work? If one value is positive and the other is negative, their product is negative. This is a classic trick you'll use in bisection and false-position methods.

---

## Chemical Engineering Example: Reaction Feasibility

```python
delta_G = -50.2  # Gibbs free energy, kJ/mol

if delta_G < 0:
    print("Reaction is spontaneous (favorable)")
elif delta_G == 0:
    print("Reaction is at equilibrium")
else:
    print("Reaction is non-spontaneous")
```

---

## Numerical Methods Example: Quadratic Formula

When implementing the quadratic formula, you need to check the discriminant ($b^2 - 4ac$) to determine what type of roots you'll get. This is a great example of nested if/else:

```python
import math

a, b, c = 1, -5, 6  # coefficients of ax² + bx + c = 0

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

You'll encounter this exact pattern when solving the van der Waals equation of state for molar volume—it's a cubic equation, and checking for root types helps you understand the physical behavior of the gas.

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
