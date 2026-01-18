---
title: Data Types
---

# Data Types in Python

## Why Should I Care About Types?

Imagine you're simulating a falling parachutist. You need to store:
- The parachutist's **mass**: `68.1` kg (a decimal number)
- The **drag coefficient**: `12.5` kg/s (another decimal)
- Whether the **parachute is open**: `True` or `False`
- The **jumper's name**: `"Alex"` (text)

Each of these is a different *type* of data. Python needs to know what type something is so it knows what operations make sense. You can multiply two numbers, but what does it mean to multiply two names?

Get the type wrong, and your code breaks. Understand types, and you'll write code that just works.

---

## Numbers: Integers and Floats

The most fundamental data in numerical methods is, of course, numbers. Python has two kinds.

### Integers (`int`)

When you type a number without a decimal point, Python treats it as an **integer**, a whole number:

```python
n_iterations = 100
temperature = -10
num_molecules = 602214085700000
```

Notice there are no quotes around these values. That's important: `25` is an integer, but `"25"` would be text (we'll get to that shortly).

### Floating-Point (`float`)

But most engineering calculations involve decimal numbers. When you include a decimal point, Python creates a **float**:

```python
pressure = 101.325
molar_mass = 18.015
```

For very large or very small numbers, you can use scientific notation with `e`:

```python
concentration = 2.5e-3  # Same as 0.0025
avogadro = 6.022e23     # 6.022 × 10²³
```

So now we know how to store numbers. But what about text?

---

## Text: Strings

Sometimes you need to store text: a compound name, a file path, a label for your plot. In Python, text is called a **string** (`str`), and it must be enclosed in quotes:

```python
element = "Carbon"
formula = 'H2O'
```

You can use single quotes `'...'` or double quotes `"..."`. Python treats them the same. Pick one style and be consistent.

For text that spans multiple lines, use triple quotes:

```python
description = """This reaction produces
carbon dioxide and water
as byproducts."""
```

### The Quotes Matter

Here's a common mistake. What happens if you forget the quotes?

```python
element = Carbon
```

Python sees `Carbon` without quotes and thinks: "That must be a variable name. Let me look up its value." But you never defined a variable called `Carbon`, so Python raises a `NameError`.

The fix is simple: always put quotes around text.

```python
element = "Carbon"  # Correct: this is the string "Carbon"
```

This brings us to an interesting question: if `25` is a number but `"25"` is text, how do you convert between them?

---

## Converting Between Types

User input always comes as text. If someone types `25.5` in response to a prompt, Python gives you the *string* `"25.5"`, not the *number* `25.5`. You can't do math with a string:

```python
temp_str = "25.5"
new_temp = temp_str + 10  # ERROR! Can't add string and integer
```

To convert a string to a number, use `int()` or `float()`:

```python
temp_str = "25.5"
temp = float(temp_str)  # Now it's the number 25.5
new_temp = temp + 10    # Works! new_temp is 35.5
```

This matters in numerical methods. When computing the Taylor series for $e^x$, you track both the term number (an `int` like 1, 2, 3...) and the running sum (a `float` like 2.718...).

You can also convert numbers to strings when you need to combine them with text:

```python
pressure = 101.325
message = "Pressure is " + str(pressure) + " kPa"
```

### A Trap: int() Truncates, It Doesn't Round

When you convert a float to an integer, Python chops off the decimal part. It does NOT round:

```python
print(int(3.9))   # Output: 3 (not 4!)
print(int(-3.9))  # Output: -3 (not -4!)
```

If you want rounding, use the `round()` function instead.

---

## True or False: Booleans

There's one more type you'll use constantly: **booleans**. A boolean can only be one of two values: `True` or `False`.

```python
is_exothermic = True
reaction_complete = False
```

You'll use booleans in conditionals and loops:

```python
parachute_open = False

if parachute_open:
    c = 68.0   # High drag
else:
    c = 12.5   # Low drag
```

### Watch the Capitalization

Python is picky about booleans:
- `True` and `False` (capital T and F) are booleans ✓
- `true` and `false` (lowercase) cause a `NameError` ✗
- `"True"` (in quotes) is a string, not a boolean ✗

```python
active = True      # ✓ Boolean
active = true      # ✗ NameError: name 'true' is not defined
active = "True"    # This "works" but it's a string, not a boolean!
```

---

## How Do I Check a Variable's Type?

If you're ever unsure what type a variable is, use the `type()` function:

```python
x = 3.14
print(type(x))
```

Output:
```
<class 'float'>
```

This is useful for debugging. If your code isn't working, check whether you have a string when you expected a number, or vice versa.

---

## Quick Reference

| Type | Example | Notes |
|------|---------|-------|
| `int` | `x = 42` | Whole numbers, no decimals |
| `float` | `x = 3.14` | Decimal numbers, use `e` for scientific notation |
| `str` | `x = "hello"` | Text in quotes (single or double) |
| `bool` | `x = True` | Only `True` or `False` (capital T/F, no quotes) |

**Type Conversion:**

| From → To | Function | Example |
|-----------|----------|--------|
| str → int | `int()` | `int("42")` → `42` |
| str → float | `float()` | `float("3.14")` → `3.14` |
| number → str | `str()` | `str(42)` → `"42"` |
| float → int | `int()` | `int(3.9)` → `3` (truncates!) |

## Next Steps

Now that you know the building blocks, continue to [Variables & Operators](variables.md) to learn how to store and manipulate these values.
