---
title: Functions
---

# Functions

## Write Once, Use Everywhere

Look at the Euler method code we wrote:

```python
v = v + (g - c/m * v) * dt
```

Now imagine you need to:
1. Run this for 5 different parachutists with different masses
2. Compare Euler's method with the analytical solution
3. Try different time steps to see which is more accurate

Are you going to copy-paste that code 15 times? What happens when you find a bug? Do you fix it in 15 places?

**Functions** solve this. You write the logic once, give it a name, and call it whenever you need it:

```python
def euler_velocity(v, g, c, m, dt):
    """One step of Euler's method for falling parachutist."""
    return v + (g - c/m * v) * dt
```

Now you can call `euler_velocity(...)` anywhere. Change the formula? Fix it in one place.

---

## Defining Functions

A function starts with `def`, followed by the function name and parameters in parentheses. The body is indented. Use `return` to send a value back.

```python
def add_numbers(a, b):
    """Add two numbers and return the result."""
    result = a + b
    return result

x = add_numbers(3, 5)
print(x)
```

Output:
```
8
```

Key things to notice:
- `def` starts the function definition
- Parameters (`a, b`) are like variables that get filled in when you call the function
- Everything indented belongs to the function
- `return` sends a value back (without it, the function returns `None`)

## Example: Ideal Gas Law

`R=8.314` is a **default value**. If you don't specify R when calling the function, it uses 8.314 automatically.

```python
def ideal_gas_volume(n, T, P, R=8.314):
    """Calculate volume using ideal gas law."""
    return (n * R * T) / P

V = ideal_gas_volume(1.0, 298.15, 101325)
print(f"Volume: {V:.6f} m^3")

for T in [273, 298, 373]:
    V = ideal_gas_volume(1.0, T, 101325)
    print(f"T = {T} K: V = {V:.4f} m^3")
```

---

## Numerical Methods: Encapsulating an Algorithm

In this course, you'll often wrap an entire numerical method in a function. Here's bisection:

```python
def bisection(f, a, b, tolerance=1e-6):
    """
    Find root of f(x) between a and b using bisection.
    
    Parameters:
        f: The function to find root of
        a, b: Initial bracket (f(a) and f(b) must have opposite signs)
        tolerance: Stop when interval is smaller than this
    
    Returns:
        Approximate root
    """
    while (b - a) > tolerance:
        mid = (a + b) / 2
        if f(a) * f(mid) < 0:
            b = mid
        else:
            a = mid
    return (a + b) / 2
```

Now you can find the root of *any* function:

```python
def my_equation(x):
    return x**3 - x - 2

root = bisection(my_equation, 1, 2)
print(f"Root: {root:.6f}")
```

Output:
```
Root: 1.521380
```

Notice how `bisection` takes a function `f` as a parameter. This is powerful: you write the algorithm once, and it works for any equation you pass to it.

---

## Returning Multiple Values

Sometimes a function needs to return more than one thing. For numerical methods, you often want both the answer and some information about how you got there (like how many iterations it took).

```python
def bisection_with_count(f, a, b, tolerance=1e-6):
    """Returns both the root AND the number of iterations."""
    iterations = 0
    
    while (b - a) > tolerance:
        mid = (a + b) / 2
        if f(a) * f(mid) < 0:
            b = mid
        else:
            a = mid
        iterations = iterations + 1
    
    return (a + b) / 2, iterations  # Return two values!

# Unpack the two returned values
root, count = bisection_with_count(my_equation, 1, 2)
print(f"Root = {root:.6f} found in {count} iterations")
```

Output:
```
Root = 1.521380 found in 20 iterations
```

---

## Example: Analytical vs Numerical

```python
import math

def analytical_velocity(t, g, c, m):
    """Exact solution for falling parachutist."""
    return (g * m / c) * (1 - math.exp(-c/m * t))

def numerical_velocity(t_end, g, c, m, dt):
    """Euler's method solution."""
    v = 0
    t = 0
    while t < t_end:
        v = v + (g - c/m * v) * dt
        t = t + dt
    return v

# Compare at t = 10s
t = 10
g, c, m = 9.8, 12.5, 68.1

v_exact = analytical_velocity(t, g, c, m)
v_euler = numerical_velocity(t, g, c, m, dt=2)

print(f"Analytical: {v_exact:.2f} m/s")
print(f"Euler (dt=2): {v_euler:.2f} m/s")
print(f"Error: {abs(v_exact - v_euler):.2f} m/s")
```

:::{tip}
For documenting your functions, see the docstrings section in [Comments](comments.md).
:::

---

## See Functions in Action

Now that you understand functions, try these interactive notebooks that use functions to implement numerical methods:

- <a href="lite/lab/index.html?path=newton_raphson.ipynb" target="_blank">Newton-Raphson Method</a>: Root finding with quadratic convergence
- <a href="lite/lab/index.html?path=bisection_method.ipynb" target="_blank">Bisection Method</a>: Guaranteed root finding
- <a href="lite/lab/index.html?path=trapezoidal_rule.ipynb" target="_blank">Trapezoidal Rule</a>: Numerical integration

---

## Next Steps

With functions, you can write modular, reusable code. Continue to [NumPy Basics](numpy_basics/index.md) to learn about efficient numerical computing with arrays.
