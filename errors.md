---
title: Error Handling
---

# Common Python Errors

## Don't Panic When You See Red

Here's a secret: **professional programmers see errors constantly**. The difference between a beginner and an expert isn't that experts write perfect code. It's that experts can *read* the error message and fix the problem in 30 seconds.

When you see a wall of red text, don't panic. Python is trying to help you. It's saying: "Something went wrong, and here's exactly where and why."

This page shows you the most common errors you'll encounter. Learn to recognize them, and you'll debug code 10× faster.

---

## TypeError
```python
# Wrong: mixing types
result = "5" + 3  # TypeError: can only concatenate str to str

# Fix: convert types
result = int("5") + 3  # 8
```

## IndentationError

This is the **most common beginner error**. Python uses indentation (spaces at the start of lines) to define code blocks. Mixing tabs and spaces, or inconsistent indentation, causes this error.

```python
# Wrong: inconsistent indentation
if x > 0:
print("positive")  # IndentationError: expected an indented block

# Wrong: mixed tabs and spaces
if x > 0:
    print("line 1")  # 4 spaces
	print("line 2")  # 1 tab - IndentationError!

# Correct: consistent 4-space indentation
if x > 0:
    print("positive")
    print("and non-zero")
```

:::{tip}
Configure your editor to insert 4 spaces when you press Tab. In VS Code: Settings → "Editor: Tab Size" = 4 and "Editor: Insert Spaces" = checked.
:::

## NameError
```python
# Wrong: variable not defined
print(temperatrue)  # NameError: name 'temperatrue' is not defined

# Fix: check spelling
temperature = 300
print(temperature)
```

## KeyError
```python
# Wrong: key doesn't exist
data = {"temp": 300}
print(data["pressure"])  # KeyError: 'pressure'

# Fix: use .get() with default
print(data.get("pressure", "Not found"))
```

## FileNotFoundError
```python
# Wrong: file doesn't exist
f = open("data.txt")  # FileNotFoundError

# Fix: check path or handle error
try:
    f = open("data.txt")
except FileNotFoundError:
    print("File not found!")
```

## How to Read Error Messages

```
Traceback (most recent call last):
  File "script.py", line 5, in <module>    ← WHERE (file, line)
    result = x / 0
             ~~^~~
ZeroDivisionError: division by zero         ← WHAT went wrong
```

**Always read from bottom up!**

---

## Debugging a Simulation: A Common Mistake

Here's an error that won't show a red message but will give wrong results. Can you spot the bug?

```python
# Euler's method for falling parachutist
g, c, m, dt = 9.8, 12.5, 68.1, 2.0
v = 0
t = 0

while t < 12:
    v = v + (g - c/m * v) * dt
    # Oops! Forgot to update t
    print(f"t = {t}, v = {v:.2f}")
```

This loop runs forever because `t` never changes! The fix:

```python
while t < 12:
    v = v + (g - c/m * v) * dt
    t = t + dt  # Don't forget this!
    print(f"t = {t}, v = {v:.2f}")
```

**Lesson**: Not all bugs cause error messages. If your loop runs forever or gives unexpected results, check that you're updating your loop variables.

---

## Quick Reference

| Error | Common Cause | Fix |
|-------|--------------|-----|
| `SyntaxError` | Typo, missing colon, unmatched quotes | Check the line Python points to |
| `NameError` | Variable not defined or misspelled | Check spelling, define before use |
| `TypeError` | Wrong type (e.g., `"5" + 3`) | Convert types: `int()`, `float()`, `str()` |
| `ValueError` | Right type, wrong value (e.g., `int("hello")`) | Validate input before converting |
| `KeyError` | Dictionary key doesn't exist | Use `.get(key, default)` |
| `IndexError` | List index out of range | Check `len(list)` before accessing |
| `FileNotFoundError` | File path is wrong | Check path, use `try/except` |
| `ZeroDivisionError` | Dividing by zero | Check denominator before dividing |

**Reading errors:** Start from the bottom line (the error type), then look at the line number above it.
