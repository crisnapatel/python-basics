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

## Creating Variables

To create a variable, write `name = value`. The `=` sign means "assign the value on the right to the name on the left":

```python
temperature = 298.15
pressure = 101.325
volume = 0.0224
```

Now `temperature` holds `298.15`. Whenever you write `temperature` in your code, Python substitutes `298.15`.

To see what's stored in a variable, print it:

```python
print(temperature)
```

Output:
```
298.15
```

### Updating Variables

You can change a variable's value by assigning to it again. The old value is replaced:

```python
temperature = 298.15
print(temperature)

temperature = 308.15
print(temperature)
```

Output:
```
298.15
308.15
```

A common pattern is updating a variable based on its current value. For example, adding 10 to the temperature:

```python
temperature = 298.15
temperature = temperature + 10
print(temperature)
```

Output:
```
308.15
```

This might look strange at first. How can `temperature` equal itself plus 10? Remember, `=` means "assign", not "equals". Python evaluates the right side first (`298.15 + 10 = 308.15`), then stores that result in `temperature`.

```{admonition} 🧩 Try It: Name → Value Visualizer
:class: tip

Practice the key idea behind variables: a *name* points to a *value*, and `=` can **rebind** the name.

<a href="_static/variables_bindings_visualizer.html" style="display: inline-block; background: #579aca; color: white; padding: 10px 20px; border-radius: 6px; text-decoration: none; font-weight: 500; margin-top: 8px;">
▶ Launch Variables Visualizer
</a>

Suggested mini-task (2 minutes):

1. Run the preset **Copy name, then rebind**.
2. Predict what `b` will be after `a = 7`.
3. Explain (in one sentence) why `b` didn’t change.
```

### Naming Rules

You can name variables almost anything, but there are a few rules:

| ✅ Valid | ❌ Invalid | Reason |
|---------|-----------|--------|
| `molar_mass` | `molar-mass` | No hyphens (looks like subtraction) |
| `temp1` | `1temp` | Can't start with a number |
| `_private` | `class` | `class` is a reserved keyword |
| `camelCase` | `my var` | No spaces |

A good practice: use descriptive names like `drag_coefficient` instead of cryptic ones like `c`. Your future self will thank you.

---

## Doing Math: Arithmetic Operators

Now that we can store values, let's do calculations. Python supports all the arithmetic operations you'd expect:

```python
m = 68.1   # mass (kg)
c = 12.5   # drag coefficient (kg/s)
g = 9.8    # gravity (m/s²)

print(g + c)    # Addition: 22.3
print(g - c)    # Subtraction: -2.7
print(g * m)    # Multiplication: 667.38
print(c / m)    # Division: 0.1835...
print(m ** 2)   # Power (exponent): 4637.61
```

These *parameters* define the physical system you're modeling. In numerical methods, you'll see this pattern constantly: define your parameters as variables, then write formulas using those variables.

### Integer Division and Remainder

Two operators might be less familiar:

```python
print(10 / 3)   # Regular division: 3.333...
print(10 // 3)  # Integer division: 3 (drops the decimal)
print(10 % 3)   # Modulo: 1 (remainder of 10 ÷ 3)
```

The modulo operator (`%`) is useful for checking if a number is even or odd:

```python
if iteration % 2 == 0:
    print("Even iteration")
```

---

## Comparing Values: Comparison Operators

So far we've stored and calculated values. But what if you need to check whether a value meets some condition? That's where comparison operators come in.

Comparisons return `True` or `False`:

```python
x = 5
y = 10

print(x == y)   # Equal? False
print(x != y)   # Not equal? True
print(x < y)    # Less than? True
print(x <= y)   # Less than or equal? True
print(x > y)    # Greater than? False
print(x >= y)   # Greater or equal? False
```

You'll use these constantly in conditionals and loops. For example, checking if the error is small enough to stop iterating.

### The Most Common Mistake: `=` vs `==`

This trips up everyone at first:

- `x = 5` means "assign 5 to x"
- `x == 5` means "is x equal to 5?"

```python
x = 5      # Assignment: x now holds 5
x == 5     # Comparison: returns True
x == 10    # Comparison: returns False
```

If you accidentally write `if x = 5:` instead of `if x == 5:`, Python will give you a syntax error. That's Python protecting you from a bug.

---

## Putting It Together: A Complete Example

Let's calculate the volume of an ideal gas using PV = nRT:

```python
# Define parameters
R = 8.314      # Gas constant, J/(mol·K)
T = 298.15     # Temperature, K
P = 101325     # Pressure, Pa
n = 1.0        # Amount, mol

# Calculate volume
V = (n * R * T) / P

# Display result
print(f"Volume: {V:.4f} m³")
```

Output:
```
Volume: 0.0245 m³
```

Notice how readable this is compared to `(1.0 * 8.314 * 298.15) / 101325`. And if you want to try a different temperature, you just change `T = 298.15` to `T = 373.15` and run again.

## Next Steps

You've stored values and done calculations. But how do you see the results? Continue to [The print() Function](print.md) to learn how to display output.
