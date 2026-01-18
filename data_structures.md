---
title: Data Structures
---

# Data Structures

## The Problem: Storing More Than One Value

So far, we've stored single values in variables: one temperature, one pressure, one mass. But what if you're running Euler's method and need to track the parachutist's velocity at every timestep?

You could create separate variables:

```python
v0 = 0.0
v1 = 19.6
v2 = 32.0
v3 = 39.85
# ... and so on for 1000 timesteps?
```

This is clearly impractical. What you need is a way to store multiple values in a single variable. That's exactly what **data structures** are for.

Python has four built-in data structures, each designed for different situations. Let's start with the most common one.

---

## Lists: Ordered Collections You Can Change

A **list** holds multiple items in order. You create one with square brackets:

```python
velocities = [0.0, 19.6, 32.0, 39.85, 44.82]
compounds = ["methane", "ethane", "propane"]
```

Now `velocities` is a single variable containing all five values. Much better than five separate variables!

### Accessing Items by Position

Items in a list are numbered starting from 0 (not 1—this trips up many beginners):

```python
temps = [300, 350, 400, 450, 500]

print(temps[0])   # First item
print(temps[2])   # Third item
print(temps[-1])  # Last item
print(temps[-2])  # Second to last
```

Output:
```
300
400
500
450
```

The negative indices are a nice Python feature: `-1` always means the last item, regardless of how long the list is.

### Getting Multiple Items: Slicing

What if you want items 1 through 3? Use a slice:

```python
temps = [300, 350, 400, 450, 500]

print(temps[1:3])   # Items at index 1 and 2
print(temps[:3])    # From start to index 2
print(temps[2:])    # From index 2 to end
print(temps[::2])   # Every 2nd item
```

Output:
```
[350, 400]
[300, 350, 400]
[400, 450, 500]
[300, 400, 500]
```

Notice that `[1:3]` gives you indices 1 and 2, but *not* 3. The end index is always excluded. This might seem odd, but it has a nice property: `temps[:3]` and `temps[3:]` together give you the whole list with no overlap.

### Modifying Lists

Unlike some other data structures we'll see, lists can be changed after creation:

```python
temps = [300, 350, 400]

temps[1] = 375           # Change the second item
temps.append(450)        # Add to the end
temps.insert(0, 250)     # Insert at the beginning
temps.remove(375)        # Remove a specific value
last = temps.pop()       # Remove and return the last item

print(temps)
```

Output:
```
[250, 300, 400]
```

Each of these operations modifies the list in place—you don't need to create a new list.

### Common List Operations

For data analysis, you'll often need the length, sum, minimum, or maximum:

```python
temps = [400, 300, 500, 350]

print(len(temps))      # 4 (number of items)
print(min(temps))      # 300 (smallest)
print(max(temps))      # 500 (largest)
print(sum(temps))      # 1550 (total)
print(sorted(temps))   # [300, 350, 400, 500] (new sorted list)
```

Note that `sorted()` returns a *new* sorted list—the original stays unchanged. If you want to sort in place, use `temps.sort()`.

:::{tip}
For more built-in functions that work with lists (like `sum()`, `min()`, `max()`), see [Common Functions](common_functions.md).
:::

---

## Tuples: When Data Shouldn't Change

Lists are great, but sometimes you want to guarantee that data can't be modified. That's what **tuples** are for.

A tuple looks like a list, but uses parentheses instead of brackets:

```python
point = (3.5, 2.1)
constants = (8.314, 6.022e23, 1.38e-23)  # R, Avogadro, Boltzmann
```

You can access items the same way as lists:

```python
print(point[0])  # 3.5
print(point[1])  # 2.1
```

But if you try to change an item, Python raises an error:

```python
point[0] = 4.0  # TypeError: 'tuple' object does not support item assignment
```

### Why Would I Want That?

You might wonder: why would I *want* something I can't change? A few reasons:

1. **Safety**: You can't accidentally modify data that shouldn't change (like physical constants)
2. **Dictionary keys**: Tuples can be used as dictionary keys, lists cannot
3. **Multiple return values**: Functions often return tuples

### Unpacking Tuples

A convenient feature: you can "unpack" a tuple into separate variables:

```python
point = (3.5, 2.1)
x, y = point

print(x)  # 3.5
print(y)  # 2.1
```

This is why functions can effectively return multiple values—they return a tuple, and you unpack it.

Now, lists and tuples are great for ordered data. But what if you want to look up values by name rather than by position?

---

## Dictionaries: Looking Up Values by Name

Imagine you want to store properties of water: formula, molar mass, boiling point. With a list, you'd have to remember that index 0 is formula, index 1 is molar mass, etc. That's error-prone.

A **dictionary** lets you use meaningful names (called "keys") instead of numbers:

```python
water = {
    "formula": "H2O",
    "molar_mass": 18.015,
    "boiling_point": 373.15,
    "density": 1000
}
```

Now you can access values by name:

```python
print(water["formula"])
print(water["molar_mass"])
print(water.get("viscosity", "not found"))
```

Output:
```
H2O
18.015
not found
```

Using `.get()` with a default value prevents errors when a key doesn't exist. Compare this to `water["viscosity"]`, which would crash with a `KeyError`.

### Modifying Dictionaries

Unlike tuples, dictionaries can be modified:

```python
water["viscosity"] = 0.001    # Add new key-value pair
water["density"] = 997        # Update existing value
del water["boiling_point"]    # Remove a key
```

### Looping Through Dictionaries

You'll often need to iterate through all the items in a dictionary:

```python
water = {"formula": "H2O", "molar_mass": 18.015, "density": 1000}

# Loop through keys and values together
for key, value in water.items():
    print(f"{key}: {value}")
```

Output:
```
formula: H2O
molar_mass: 18.015
density: 1000
```

### Nested Dictionaries: A Practical Example

Dictionaries can contain other dictionaries. This is perfect for storing properties of multiple compounds:

```python
compounds = {
    "methane": {"formula": "CH4", "MW": 16.04, "Tc": 190.6},
    "ethane": {"formula": "C2H6", "MW": 30.07, "Tc": 305.3},
    "propane": {"formula": "C3H8", "MW": 44.10, "Tc": 369.8}
}

# Access nested data
print(compounds["ethane"]["MW"])  # 30.07

# Loop through all compounds
for name, props in compounds.items():
    print(f"{name}: MW = {props['MW']} g/mol")
```

Output:
```
30.07
methane: MW = 16.04 g/mol
ethane: MW = 30.07 g/mol
propane: MW = 44.1 g/mol
```

There's one more data structure worth knowing about, especially when you need to find unique values or check membership quickly.

---

## Sets: Unique Items Only

A **set** is an unordered collection where duplicates are automatically removed:

```python
elements = {"C", "H", "O", "N"}

# Try adding duplicates
numbers = {1, 2, 2, 3, 3, 3}
print(numbers)
```

Output:
```
{1, 2, 3}
```

Python kept only one copy of each value.

### When Are Sets Useful?

Sets are perfect for finding unique values. Say you have a list of all species in a reaction mechanism and want to know how many unique species there are:

```python
all_species = ["H2", "O2", "H2O", "H2", "OH", "O2", "H2O"]
unique_species = set(all_species)
print(unique_species)
print(f"Found {len(unique_species)} unique species")
```

Output:
```
{'H2', 'O2', 'H2O', 'OH'}
Found 4 unique species
```

### Set Operations

Sets support mathematical set operations:

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a | b)   # Union: all items from both
print(a & b)   # Intersection: items in both
print(a - b)   # Difference: items in a but not in b
```

Output:
```
{1, 2, 3, 4, 5, 6}
{3, 4}
{1, 2}
```

The `in` operator checks membership very quickly:

```python
print("H2O" in unique_species)  # True
```

---

## So Which One Should I Use?

Now you know four data structures. Here's how to choose:

### Practical example: finding unique species

```python
reactions = ["A + B -> C", "C + D -> E", "A + E -> F"]

all_species = {"A", "B", "C", "D", "E", "F"}
products = {"C", "E", "F"}
reactants_only = all_species - products
print(reactants_only)
```

Output:
```
{'A', 'B', 'D'}
```

---

## When to Use What?

| Structure | Use When... | Example |
|-----------|-------------|---------|
| **List** | Order matters, items may change | Time series data, experiment results |
| **Tuple** | Data shouldn't change, returning multiple values | Coordinates, RGB colors, constants |
| **Dictionary** | You need to look up values by name | Compound properties, configuration settings |
| **Set** | You need unique items or set operations | Finding unique species, checking membership |

---

## Quick Reference

### Lists
| Operation | Syntax | Example |
|-----------|--------|--------|
| Create | `[item1, item2, ...]` | `temps = [300, 350, 400]` |
| Access | `list[i]` | `temps[0]` → `300` |
| Slice | `list[start:end]` | `temps[1:3]` → `[350, 400]` |
| Append | `list.append(item)` | `temps.append(450)` |
| Insert | `list.insert(i, item)` | `temps.insert(0, 250)` |
| Remove | `list.remove(item)` | `temps.remove(350)` |
| Pop | `list.pop()` | `last = temps.pop()` |
| Length | `len(list)` | `len(temps)` → `3` |
| Sort | `sorted(list)` or `list.sort()` | `sorted(temps)` |

### Tuples
| Operation | Syntax | Example |
|-----------|--------|--------|
| Create | `(item1, item2, ...)` | `point = (3.5, 2.1)` |
| Access | `tuple[i]` | `point[0]` → `3.5` |
| Unpack | `a, b = tuple` | `x, y = point` |

### Dictionaries
| Operation | Syntax | Example |
|-----------|--------|--------|
| Create | `{key: value, ...}` | `water = {"MW": 18.0}` |
| Access | `dict[key]` | `water["MW"]` → `18.0` |
| Safe access | `dict.get(key, default)` | `water.get("Tc", 0)` |
| Add/update | `dict[key] = value` | `water["Tb"] = 373` |
| Delete | `del dict[key]` | `del water["Tb"]` |
| Keys | `dict.keys()` | `water.keys()` |
| Values | `dict.values()` | `water.values()` |
| Items | `dict.items()` | `water.items()` |

### Sets
| Operation | Syntax | Example |
|-----------|--------|--------|
| Create | `{item1, item2, ...}` | `elements = {"C", "H", "O"}` |
| Add | `set.add(item)` | `elements.add("N")` |
| Union | `a \| b` | `{1,2} \| {2,3}` → `{1,2,3}` |
| Intersection | `a & b` | `{1,2} & {2,3}` → `{2}` |
| Difference | `a - b` | `{1,2} - {2,3}` → `{1}` |
| Membership | `item in set` | `"C" in elements` → `True` |

## Next Steps

Continue to [Iterators](iterators.md) to learn how to loop through data structures efficiently.
