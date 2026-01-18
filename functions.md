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

## Next Steps

With functions, you can write modular, reusable code. Continue to [NumPy Basics](numpy_basics/index.md) to learn about efficient numerical computing with arrays.
