---
title: Data Structures
---

# Data Structures

## Storing More Than One Value

So far, we've stored single values in variables: one temperature, one pressure, one mass. But what if you have 100 temperature readings? Or a table of properties for 10 compounds?

You need **data structures**: containers that hold multiple values. Python has four built-in types, each with different strengths.

---

## Lists

A list is an ordered collection of items. You can add, remove, and change items. Use square brackets `[]`.

```python
temperatures = [300, 350, 400, 450, 500]
compounds = ["methane", "ethane", "propane"]
mixed = [1, "hello", 3.14, True]  # Can mix types (but usually don't)
```

### Accessing items

Items are numbered starting from 0 (not 1!).

```python
temps = [300, 350, 400, 450, 500]

print(temps[0])
print(temps[2])
print(temps[-1])
print(temps[-2])
```

Output:
```
300
400
500
450
```

Notice that negative indices count from the end: `-1` is the last item, `-2` is second to last.

### Slicing (getting multiple items)

```python
temps = [300, 350, 400, 450, 500]

print(temps[1:3])
print(temps[:3])
print(temps[2:])
print(temps[::2])
```

Output:
```
[350, 400]
[300, 350, 400]
[400, 450, 500]
[300, 400, 500]
```

The slice `[1:3]` gives items at index 1 and 2 (the end index is excluded). Using `[:3]` means "from the start", `[2:]` means "to the end", and `[::2]` takes every 2nd item.

### Modifying lists

```python
temps = [300, 350, 400]

temps[1] = 375
print(temps)

temps.append(450)
print(temps)

temps.insert(0, 250)
print(temps)

temps.remove(375)
print(temps)

last = temps.pop()
print(last, temps)
```

Output:
```
[300, 375, 400]
[300, 375, 400, 450]
[250, 300, 375, 400, 450]
[250, 300, 400, 450]
450 [250, 300, 400]
```

Each operation modifies the list in place. `pop()` removes AND returns the last item.

### Useful list operations

```python
temps = [400, 300, 500, 350]

print(len(temps))
print(min(temps))
print(max(temps))
print(sum(temps))
print(sorted(temps))
temps.sort()
print(temps)
print(350 in temps)
```

Output:
```
4
300
500
1550
[300, 350, 400, 500]
[300, 350, 400, 500]
True
```

Note that `sorted()` returns a new sorted list while `.sort()` modifies the original list in place.

---

## Tuples

A tuple is like a list, but **immutable** (you can't change it after creation). Use parentheses `()`.

```python
point = (3.5, 2.1)
rgb = (255, 128, 0)
constants = (8.314, 6.022e23, 1.38e-23)  # R, Avogadro, Boltzmann
```

### Why use tuples?

1. **Safety**: Can't accidentally modify data that shouldn't change
2. **Dictionary keys**: Tuples can be dictionary keys, lists cannot
3. **Multiple return values**: Functions often return tuples

Accessing works the same as lists:

```python
point = (3.5, 2.1)
print(point[0])
print(point[1])
```

Output:
```
3.5
2.1
```

Unpacking lets you assign multiple variables at once:

```python
point = (3.5, 2.1)
x, y = point
print(x)
print(y)
```

Output:
```
3.5
2.1
```

Trying to modify a tuple causes an error:

```python
point[0] = 4.0
```

```
TypeError: 'tuple' object does not support item assignment
```

---

## Dictionaries

A dictionary stores **key-value pairs**. Instead of accessing by position (index 0, 1, 2...), you access by a meaningful key. Use curly braces `{}`.

```python
water = {
    "formula": "H2O",
    "molar_mass": 18.015,
    "boiling_point": 373.15,
    "density": 1000
}
```

### Accessing values

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

Using `.get()` with a default value prevents errors when a key doesn't exist.

### Modifying dictionaries

```python
water["viscosity"] = 0.001    # Add new key-value pair
water["density"] = 997        # Update existing value
del water["boiling_point"]    # Remove a key
```

### Looping through dictionaries

```python
water = {"formula": "H2O", "molar_mass": 18.015, "density": 1000}   # dictionaries can be written in one line too!

# Loop through keys
for key in water:
    print(key)

# Loop through values
for value in water.values():
    print(value)

# Loop through both
for key, value in water.items():
    print(f"{key}: {value}")
```

### Practical example: compound properties

```python
compounds = {
    "methane": {"formula": "CH4", "MW": 16.04, "Tc": 190.6},
    "ethane": {"formula": "C2H6", "MW": 30.07, "Tc": 305.3},
    "propane": {"formula": "C3H8", "MW": 44.10, "Tc": 369.8}
}

print(compounds["ethane"]["MW"])

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

---

## Sets

A set is an **unordered** collection of **unique** items. Duplicates are automatically removed. Use curly braces `{}` but without key-value pairs.

```python
elements = {"C", "H", "O", "N"}
primes = {2, 3, 5, 7, 11}

numbers = {1, 2, 2, 3, 3, 3}
print(numbers)
```

Output:
```
{1, 2, 3}
```

Duplicates are automatically removed.

### Set operations

Sets are great for checking membership and finding unique values.

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a | b)
print(a & b)
print(a - b)
print(3 in a)
```

Output:
```
{1, 2, 3, 4, 5, 6}
{3, 4}
{1, 2}
True
```

`|` is union (all items), `&` is intersection (common items), `-` is difference (items in a but not b).

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
