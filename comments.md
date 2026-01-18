---
title: Comments
---

# Comments in Python

## You'll Thank Yourself Later

You write a script to process your lab data. It works perfectly. Three weeks later, you need to modify it for a different experiment. You open the file and see:

```python
x = data[:, 0]
y = data[:, 1] * 0.0821 * data[:, 2] / data[:, 3]
z = np.trapz(y, x) / np.trapz(np.ones_like(y), x)
```

What is `x`? Why `0.0821`? What is `z` calculating?

Now imagine you had written:

```python
# Extract time (column 0) and raw pressure data
time = data[:, 0]

# Convert pressure to moles using ideal gas law: n = PV/RT
# 0.0821 is R in L·atm/(mol·K)
moles = data[:, 1] * 0.0821 * data[:, 2] / data[:, 3]

# Calculate mean concentration using trapezoidal integration
mean_conc = np.trapz(moles, time) / np.trapz(np.ones_like(moles), time)
```

Comments allow us to understand what each block of code is doing without reading entire code block. It also makes it easy for us remember why we have implemented a certain logic etc. 
Imagine you write your assignments with no comments. Your TA has to read all the code to understand what's you have done exactly. Doing this for each student can be  time consuming and a frustrated TA or prof is less likely to reward you with good marks! Future you (and your lab partners, and your TA) will thank you.

---

## How to Write Comments

### Single-line comments with `#`

Everything after `#` on a line is ignored by Python.

```python
# This entire line is a comment. Python ignores it.

temperature = 298.15  # You can also put comments at the end of a line

# Comments are for HUMANS, not for Python
# Use them to explain WHY you're doing something, not just WHAT
```

### What's happening here?

```python
x = 10       # This line runs: x is now 10
# x = 20     # This line is IGNORED: x is still 10
print(x)     # Output: 10
```

Key insight: The `#` symbol tells Python "ignore everything after this on this line."

---

## Multi-line Comments

For longer explanations, you have two options:

### Option 1: Multiple `#` lines

```python
# This function calculates the Reynolds number
# for flow in a pipe. Reynolds number determines
# whether flow is laminar (Re < 2300) or 
# turbulent (Re > 4000).
def reynolds_number(velocity, diameter, viscosity, density):
    return (density * velocity * diameter) / viscosity
```

### Option 2: Triple quotes (docstrings)

```python
"""
This function calculates the Reynolds number
for flow in a pipe. Reynolds number determines
whether flow is laminar (Re < 2300) or 
turbulent (Re > 4000).
"""
def reynolds_number(velocity, diameter, viscosity, density):
    return (density * velocity * diameter) / viscosity
```

:::{note}
Triple-quoted strings at the start of a function are called **docstrings**. They're special because Python stores them and you can access them with `help(function_name)`.
:::

---

## When to Comment (and When Not To)

### Good comments explain WHY

```python
# Use 0.1s time step for stability (larger steps cause oscillation)
dt = 0.1

# Iterate until 99% of terminal velocity (not 100% because we'd never reach it)
while v < 0.99 * v_terminal:
    v = v + (g - c/m * v) * dt
```

### Bad comments repeat WHAT the code says

```python
# Set x to 5
x = 5  # This comment adds no information!

# Add 1 to counter
counter = counter + 1  # We can already see this from the code
```

### Good comments explain non-obvious details

```python
# R = 8.314 J/(mol·K), but we need L·atm/(mol·K), so R = 0.0821
R = 0.0821

# Data columns: [time, temp, pressure, volume, flow_rate]
# We only need time (0) and pressure (2)
time = data[:, 0]
pressure = data[:, 2]
```

---

## Commenting Out Code

You can "turn off" lines of code by commenting them out. This is useful for:
- Testing different approaches
- Temporarily disabling code without deleting it
- Debugging

```python
v = 0
g, c, m = 9.8, 12.5, 68.1

# Try different time steps to see which is more accurate
dt = 0.1
# dt = 0.5
# dt = 2.0

for i in range(100):
    v = v + (g - c/m * v) * dt
    # print(v)  # Uncomment this line to see each step (useful for debugging)

print(f"Final velocity: {v:.2f} m/s")
```

---

## Keyboard Shortcuts

Most code editors let you comment/uncomment multiple lines at once:

| Editor | Shortcut |
|--------|----------|
| VS Code | `Ctrl + /` (Windows/Linux) or `Cmd + /` (Mac) |
| Jupyter | `Ctrl + /` |
| Spyder | `Ctrl + 1` |

Select multiple lines, press the shortcut, and they all get commented or uncommented.

---

## Quick Reference

| Syntax | Use Case |
|--------|----------|
| `# comment` | Single-line comment |
| `code  # comment` | Inline comment (at end of line) |
| `# code` | Comment out (disable) a line |
| `"""..."""` or `'''...'''` | Multi-line string / docstring |

## Next Steps

Continue to [Data Types](datatypes.md) to learn about the different kinds of values Python can work with.
