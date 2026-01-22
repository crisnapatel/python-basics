---
title: Loops
---

# Loops

## Every Numerical Method Needs This

Numerical methods are fundamentally about **repetition**. Whether it's:
- Euler's method: repeat "compute next value" 1000 times
- Newton-Raphson: repeat "improve guess" until error is small enough  
- Simulations: repeat "update state" for each time step

You can't do computational engineering without loops. They're the engine that drives every numerical algorithm.

---

## For Loop

Use `for` when you know how many times you want to repeat something.

### A Simple Counting Example

Let's start with something basic. Say you want to print "Hello" five times:

```python
for i in range(5):
    print(f"Hello! This is repetition number {i + 1}")
```

Output:
```
Hello! This is repetition number 1
Hello! This is repetition number 2
Hello! This is repetition number 3
Hello! This is repetition number 4
Hello! This is repetition number 5
```

The `range(5)` generates the numbers 0, 1, 2, 3, 4 (five numbers, starting from 0). For each number, Python runs the indented code.

### Summing Up Numbers

What if you want to add up all numbers from 1 to 10? Instead of typing `1 + 2 + 3 + ... + 10`, use a loop:

```python
total = 0

for number in range(1, 11):
    total = total + number
    print(f"Added {number}, total is now {total}")

print(f"\nFinal sum: {total}")
```

Output:
```
Added 1, total is now 1
Added 2, total is now 3
Added 3, total is now 6
...
Added 10, total is now 55

Final sum: 55
```

This pattern (start with zero, then add things in a loop) appears everywhere in numerical methods. You'll use it for summing series, computing integrals, and more.

:::{tip}
**Want to see a more advanced example?** Check out [this notebook](../notebooks/taylor_series_loop.ipynb) where we use a for loop to compute the Taylor series for $e^x$ term by term.
:::

### Euler's method for falling parachutist

The loop repeats the indented code for each value of `t`. Here, `range(0, 14, 2)` gives us: 0, 2, 4, 6, 8, 10, 12.

```python
g = 9.8
c = 12.5
m = 68.1
dt = 2
v = 0

for t in range(0, 14, 2):
    print(f"t = {t:2d} s, v = {v:5.2f} m/s")
    v = v + (g - c/m * v) * dt
```

Output:
```
t =  0 s, v =  0.00 m/s
t =  2 s, v = 19.60 m/s
t =  4 s, v = 32.00 m/s
t =  6 s, v = 39.85 m/s
t =  8 s, v = 44.82 m/s
t = 10 s, v = 47.97 m/s
t = 12 s, v = 49.96 m/s
```

### How `range()` works

```python
range(5)         # 0, 1, 2, 3, 4        (start defaults to 0, stop at 5)
range(2, 7)      # 2, 3, 4, 5, 6        (start at 2, stop before 7)
range(0, 10, 2)  # 0, 2, 4, 6, 8        (start at 0, stop before 10, step by 2)
range(10, 0, -1) # 10, 9, 8, ..., 1     (count backwards)
```

### Looping over a list

Read `for compound in compounds` as "for each compound in the list compounds, do..."

The loop variable (`compound`) is a new variable created by the loop. It takes on each value from the list, one at a time. You can name it anything you want.

```python
compounds = ["methane", "ethane", "propane"]

for compound in compounds:
    print(compound)
```

Output:
```
methane
ethane
propane
```

### Numerical Integration: Composite Trapezoidal Rule

When you need to compute a definite integral numerically, you divide it into segments and sum up the areas. Here's how to integrate $\int_0^2 x^2 \, dx$:

```python
def f(x):
    return x**2

a, b = 0, 2       # Integration limits
n = 4             # Number of segments
h = (b - a) / n   # Width of each segment

# Trapezoidal rule: sum up trapezoid areas
integral = f(a) + f(b)  # First and last terms

for i in range(1, n):
    x_i = a + i * h
    integral = integral + 2 * f(x_i)  # Middle terms are weighted by 2

integral = integral * h / 2

print(f"Computed integral: {integral:.4f}")
print(f"Exact answer: {2**3 / 3:.4f}")  # ∫x² = x³/3
```

Output:
```
Computed integral: 2.7500
Exact answer: 2.6667
```

The formula adds up the function values at each point, with middle points counted twice (that's the "2 *" in the loop). You'll learn why in the numerical integration lectures.

---

## While Loop

Use `while` when you don't know how many iterations you need. The loop keeps running as long as the condition is `True`.

This is exactly what you need for iterative numerical methods: you keep improving your answer until it's "good enough." But how many iterations will that take? You don't know in advance, and that's why you need `while`.

### How while works

```python
count = 0
while count < 3:
    print(count)
    count = count + 1
```
Output: `0, 1, 2` (stops when count becomes 3)

:::{warning}
Always update the variable in your condition! Otherwise the loop runs forever.
:::

### Numerical Methods: Newton-Raphson Until Convergence

This is the most important while loop pattern in the course. Newton-Raphson finds roots by repeatedly improving a guess until the error is small enough:

```python
import math

# Find x where e^(-x) = x (i.e., solve e^(-x) - x = 0)
def f(x):
    return math.exp(-x) - x

def df(x):
    return -math.exp(-x) - 1  # derivative of f

x = 0.0        # Initial guess
tolerance = 1e-6
iteration = 0

while True:
    x_new = x - f(x) / df(x)  # Newton-Raphson formula
    error = abs(x_new - x)
    iteration = iteration + 1
    
    print(f"Iteration {iteration}: x = {x_new:.8f}, error = {error:.2e}")
    
    if error < tolerance:
        print(f"\nConverged! Root = {x_new:.6f}")
        break
    
    x = x_new
```

Output:
```
Iteration 1: x = 0.50000000, error = 5.00e-01
Iteration 2: x = 0.56631100, error = 6.63e-02
Iteration 3: x = 0.56714317, error = 8.32e-04
Iteration 4: x = 0.56714329, error = 1.24e-07

Converged! Root = 0.567143
```

Notice how the error drops rapidly. That's the quadratic convergence of Newton-Raphson. In just 4 iterations, we went from a rough guess to a highly accurate answer.

### The Bisection Method

Bisection is slower but guaranteed to work. You keep halving an interval until it's small enough:

```python
def f(x):
    return x**3 - x - 2  # Find root of this function

x_lower, x_upper = 1.0, 2.0  # Initial bracket
tolerance = 1e-6

while (x_upper - x_lower) > tolerance:
    x_mid = (x_lower + x_upper) / 2
    
    if f(x_lower) * f(x_mid) < 0:
        x_upper = x_mid  # Root is in lower half
    else:
        x_lower = x_mid  # Root is in upper half
    
    print(f"Bracket: [{x_lower:.6f}, {x_upper:.6f}], width = {x_upper - x_lower:.2e}")

print(f"\nRoot ≈ {(x_lower + x_upper) / 2:.6f}")
```

The key insight: `if f(x_lower) * f(x_mid) < 0` checks if there's a sign change. If yes, the root must be in that half. This is the bracket-checking pattern you learned in the if/else section!

### Example: iterate until convergence

How long until the parachutist reaches 99% of terminal velocity? We don't know in advance, so we use `while`.

```python
g, c, m, dt = 9.8, 12.5, 68.1, 0.1
v_terminal = g * m / c

v = 0
t = 0

while v < 0.99 * v_terminal:
    v = v + (g - c/m * v) * dt
    t = t + dt

print(f"Reached 99% terminal velocity at t = {t:.1f} s")
```
Output: `Reached 99% terminal velocity at t = 25.1 s`

### Decaying concentration

```python
concentration = 1.0
while concentration > 0.1:
    concentration = concentration * 0.5
    print(f"C = {concentration}")
```

---

## Quick Reference

| Pattern | Syntax | Use When |
|---------|--------|----------|
| For loop (count) | `for i in range(n):` | You know how many iterations |
| For loop (items) | `for x in list:` | Loop through each item |
| While loop | `while condition:` | Loop until condition is false |
| range(n) | `range(5)` → 0,1,2,3,4 | Sequence starting from 0 |
| range(start, stop) | `range(2, 7)` → 2,3,4,5,6 | Sequence from start to stop-1 |
| range(start, stop, step) | `range(0, 10, 2)` → 0,2,4,6,8 | Sequence with custom step |

## Next Steps

Continue to [Data Structures](../data_structures.md) to learn about lists, dictionaries, and more.

:::{tip}
For advanced loop patterns like `enumerate()`, `zip()`, and list comprehensions, see [Iterators and Looping Patterns](../iterators.md) after you've learned about data structures.
:::
