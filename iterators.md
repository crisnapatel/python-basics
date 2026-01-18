---
title: Iterators and Looping Patterns
---

# Iterators and Looping Patterns

## Beyond Basic Loops

You've seen `for i in range(n)` and `for item in list` in [Loops](control_flow/loops.md). But Python has more powerful patterns for iterating through data.

Here's a common situation: you're processing experimental data and need to know *which* measurement you're on. Maybe you want to print "Reading 1: 300 K" instead of just "300 K". Or you need to compare each value with the previous one. Manually tracking indices leads to bugs. These patterns make your code cleaner and less error-prone.

---

## enumerate(): Get Index and Value

Often you need both the item AND its position. Instead of manually tracking an index, use `enumerate()`.

Without enumerate (error-prone):
```python
temps = [300, 350, 400, 450]
i = 0
for temp in temps:
    print(f"Index {i}: {temp} K")
    i = i + 1
```

With enumerate (cleaner):
```python
temps = [300, 350, 400, 450]
for i, temp in enumerate(temps):
    print(f"Index {i}: {temp} K")
```

Output:
```
Index 0: 300 K
Index 1: 350 K
Index 2: 400 K
Index 3: 450 K
```

You can start from a different number:
```python
for i, temp in enumerate(temps, start=1):
    print(f"Reading {i}: {temp} K")
# Output: Reading 1: 300 K, Reading 2: 350 K, ...
```

---

## zip(): Loop Through Multiple Lists Together

When you have parallel data (same length lists that correspond to each other), use `zip()`.

```python
times = [0, 1, 2, 3, 4]
concentrations = [1.0, 0.82, 0.67, 0.55, 0.45]

for t, C in zip(times, concentrations):
    print(f"t = {t} s, C = {C:.2f} mol/L")
```

Output:
```
t = 0 s, C = 1.00 mol/L
t = 1 s, C = 0.82 mol/L
t = 2 s, C = 0.67 mol/L
...
```

You can zip more than two lists:
```python
temps = [300, 350, 400]
pressures = [101, 150, 200]
volumes = [0.024, 0.019, 0.016]

for T, P, V in zip(temps, pressures, volumes):
    print(f"T={T}K, P={P}kPa, V={V}m^3")
```

---

## List Comprehensions: Create Lists in One Line

A **list comprehension** is a compact way to create a new list by transforming each item of an existing list.

Traditional loop:
```python
temps_K = [300, 350, 400, 450]
temps_C = []
for T in temps_K:
    temps_C.append(T - 273.15)
```

List comprehension (same result):
```python
temps_K = [300, 350, 400, 450]
temps_C = [T - 273.15 for T in temps_K]
```

The pattern is: `[expression for item in iterable]`

More examples:
```python
# Square each number
numbers = [1, 2, 3, 4, 5]
squares = [x**2 for x in numbers]  # [1, 4, 9, 16, 25]

# Apply a formula
pressures_atm = [1, 2, 3]
pressures_kPa = [P * 101.325 for P in pressures_atm]  # [101.325, 202.65, 303.975]
```

### With a condition (filtering)

You can add `if` to filter which items are included:

```python
temps = [250, 300, 350, 400, 450, 500]

# Only temps above 300
hot = [T for T in temps if T > 300]  # [350, 400, 450, 500]

# Only even numbers
numbers = [1, 2, 3, 4, 5, 6]
evens = [x for x in numbers if x % 2 == 0]  # [2, 4, 6]
```

---

## Dictionary Comprehensions

Same idea, but creates a dictionary:

```python
compounds = ["methane", "ethane", "propane"]
carbon_count = [1, 2, 3]

# Create a dictionary
carbons = {name: n for name, n in zip(compounds, carbon_count)}
# {'methane': 1, 'ethane': 2, 'propane': 3}
```

---

## Iterating Through Dictionaries

```python
properties = {"MW": 18.015, "Tb": 373.15, "Tc": 647.1}

# Keys only (default)
for key in properties:
    print(key)

# Values only
for value in properties.values():
    print(value)

# Both keys and values
for key, value in properties.items():
    print(f"{key} = {value}")
```

---

## The range() Function

`range()` generates a sequence of numbers. You've seen it in loops, but here's the full picture.

```python
range(5)          # 0, 1, 2, 3, 4
range(2, 7)       # 2, 3, 4, 5, 6
range(0, 10, 2)   # 0, 2, 4, 6, 8 (step of 2)
range(10, 0, -1)  # 10, 9, 8, 7, 6, 5, 4, 3, 2, 1 (counting down)
```

To see the numbers as a list, convert it:
```python
print(list(range(5)))  # [0, 1, 2, 3, 4]
```

---

## Breaking Out of Loops

### break: Exit the loop immediately

```python
# Find first temperature above 400
temps = [300, 350, 420, 380, 450]
for T in temps:
    if T > 400:
        print(f"Found: {T} K")
        break  # Stop the loop
```
Output: `Found: 420 K`

### continue: Skip to next iteration

```python
# Print only positive values
values = [1, -2, 3, -4, 5]
for v in values:
    if v < 0:
        continue  # Skip negative values
    print(v)
```
Output: `1, 3, 5`

---

## Practical Example: Processing Experimental Data

```python
# Time and concentration data from an experiment
times = [0, 10, 20, 30, 40, 50, 60]
concentrations = [1.0, 0.82, 0.67, 0.55, 0.45, 0.37, 0.30]

# Calculate rate of change between each point
rates = []
for i in range(1, len(times)):
    dt = times[i] - times[i-1]
    dC = concentrations[i] - concentrations[i-1]
    rate = dC / dt
    rates.append(rate)

# Print with enumerate
print("Reaction rates:")
for i, rate in enumerate(rates, start=1):
    print(f"  Interval {i}: {rate:.4f} mol/(L*s)")
```

---

## Quick Reference

| Pattern | What It Does |
|---------|--------------|
| `for i, x in enumerate(list)` | Get index and value |
| `for a, b in zip(list1, list2)` | Loop through two lists together |
| `[expr for x in list]` | Create new list by transforming |
| `[x for x in list if cond]` | Filter items |
| `break` | Exit loop immediately |
| `continue` | Skip to next iteration |

## Next Steps

Continue to [User Input](user_input.md) to learn how to get data from the user.
