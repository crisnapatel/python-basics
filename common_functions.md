---
title: Common Built-in Functions
---

# Common Built-in Functions

## Tools You'll Use Constantly

Python comes with many built-in functions—no imports needed. These are the ones you'll reach for most often.

---

## Working with Numbers

### abs(): Absolute value
```python
error = -0.0023
print(abs(error))

difference = 5 - 8
print(abs(difference))
```

Output:
```
0.0023
3
```

### round(): Round to decimal places
```python
pi = 3.14159265359

print(round(pi))
print(round(pi, 2))
print(round(pi, 4))

concentration = 0.123456789
print(f"C = {round(concentration, 3)} mol/L")
```

Output:
```
3
3.14
3.1416
C = 0.123 mol/L
```

### min() and max(): Find extreme values
```python
temps = [300, 350, 280, 420, 390]

print(min(temps))
print(max(temps))
print(max(10, 20, 5))
```

Output:
```
280
420
20
```

They work with both lists and multiple arguments.

### sum(): Add up all values
```python
values = [1, 2, 3, 4, 5]
print(sum(values))

data = [2.3, 2.5, 2.4, 2.6, 2.5]
average = sum(data) / len(data)
print(f"Average: {average}")
```

Output:
```
15
Average: 2.46
```

### pow(): Raise to a power
```python
print(pow(2, 3))
print(pow(10, -2))
```

Output:
```
8
0.01
```

`pow(2, 3)` is equivalent to `2**3`.

---

## Working with Collections

### len(): Count items
```python
temps = [300, 350, 400, 450]
print(len(temps))

name = "methane"
print(len(name))

properties = {"MW": 18.0, "Tb": 373}
print(len(properties))
```

Output:
```
4
7
2
```

For strings, it counts characters. For dictionaries, it counts key-value pairs.

### sorted(): Return a sorted list
```python
values = [3, 1, 4, 1, 5, 9, 2]
print(sorted(values))
print(values)
print(sorted(values, reverse=True))
```

Output:
```
[1, 1, 2, 3, 4, 5, 9]
[3, 1, 4, 1, 5, 9, 2]
[9, 5, 4, 3, 2, 1, 1]
```

Notice the original list is unchanged. Use `reverse=True` for descending order.

### reversed(): Iterate in reverse
```python
temps = [300, 350, 400]
for T in reversed(temps):
    print(T)
```

Output:
```
400
350
300
```

---

## Type Checking and Conversion

### type(): Check the type
```python
x = 3.14
print(type(x))

temps = [300, 350, 400]
print(type(temps))
```

Output:
```
<class 'float'>
<class 'list'>
```

### Type conversion functions
```python
print(int(3.7))
print(int("42"))

print(float(5))
print(float("3.14"))

print(str(273.15))

print(list(range(5)))
print(list("abc"))

print(tuple([1, 2, 3]))

print(set([1, 2, 2, 3]))
```

Output:
```
3
42
5.0
3.14
273.15
[0, 1, 2, 3, 4]
['a', 'b', 'c']
(1, 2, 3)
{1, 2, 3}
```

Note that `int()` truncates (doesn't round), and `set()` removes duplicates.

---

## Useful for Iteration

### range(): Generate sequences
```python
print(list(range(5)))
print(list(range(2, 7)))
print(list(range(0, 10, 2)))
```

Output:
```
[0, 1, 2, 3, 4]
[2, 3, 4, 5, 6]
[0, 2, 4, 6, 8]
```

### enumerate(): Get index and value
```python
temps = [300, 350, 400]
for i, T in enumerate(temps):
    print(f"Index {i}: {T} K")
```

### zip(): Pair up lists
```python
x = [1, 2, 3]
y = [10, 20, 30]
for a, b in zip(x, y):
    print(a, b)
```

---

## Boolean Tests

### all(): Check if all are True
```python
values = [True, True, True]
print(all(values))

values = [True, False, True]
print(all(values))

temps = [300, 350, 400]
print(all(T > 0 for T in temps))
```

Output:
```
True
False
True
```

Useful for checking if all items in a collection meet some condition.

### any(): Check if at least one is True
```python
values = [False, False, True]
print(any(values))

temps = [300, 350, 500, 400]
print(any(T > 450 for T in temps))
```

Output:
```
True
True
```

Useful for checking if at least one item meets some condition.

---

## Input/Output

### print(): Display output
```python
print("Hello")
print("a", "b", "c")
print("a", "b", sep="-")
print("Line 1", end=" ")
print("Line 2")
```

Output:
```
Hello
a b c
a-b
Line 1 Line 2
```

Use `sep` to change the separator between items, and `end` to change what comes after (default is newline).

### input(): Get user input
```python
name = input("Enter name: ")
value = float(input("Enter number: "))
```

---

## Quick Reference Table

| Function | Purpose | Example |
|----------|---------|---------|
| `abs(x)` | Absolute value | `abs(-5)` → `5` |
| `round(x, n)` | Round to n decimals | `round(3.14159, 2)` → `3.14` |
| `min(...)` | Smallest value | `min([3, 1, 2])` → `1` |
| `max(...)` | Largest value | `max([3, 1, 2])` → `3` |
| `sum(list)` | Sum all values | `sum([1, 2, 3])` → `6` |
| `len(x)` | Number of items | `len([1, 2, 3])` → `3` |
| `sorted(x)` | Sorted copy | `sorted([3, 1, 2])` → `[1, 2, 3]` |
| `type(x)` | Check type | `type(3.14)` → `<class 'float'>` |
| `int(x)` | Convert to int | `int("42")` → `42` |
| `float(x)` | Convert to float | `float("3.14")` → `3.14` |
| `str(x)` | Convert to string | `str(42)` → `"42"` |
| `list(x)` | Convert to list | `list(range(3))` → `[0, 1, 2]` |
| `range(n)` | Sequence 0 to n-1 | `list(range(3))` → `[0, 1, 2]` |
| `all(x)` | All True? | `all([True, True])` → `True` |
| `any(x)` | Any True? | `any([False, True])` → `True` |

---

## Practical Example: Data Analysis

```python
# Experimental measurements
measurements = [2.31, 2.45, 2.38, 2.52, 2.41, 2.39]

# Basic statistics
n = len(measurements)
total = sum(measurements)
average = total / n
minimum = min(measurements)
maximum = max(measurements)
range_val = maximum - minimum

print(f"n = {n}")
print(f"Sum = {round(total, 2)}")
print(f"Average = {round(average, 3)}")
print(f"Min = {minimum}, Max = {maximum}")
print(f"Range = {round(range_val, 2)}")

# Check data quality
all_positive = all(x > 0 for x in measurements)
any_outliers = any(abs(x - average) > 0.2 for x in measurements)

print(f"All positive: {all_positive}")
print(f"Has outliers: {any_outliers}")
```

## What's Next?

You now have a solid foundation in Python basics! Next, you'll learn about NumPy for numerical computing in [NumPy Basics](numpy_basics/index.md).
