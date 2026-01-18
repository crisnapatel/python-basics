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

## Numbers

### Integers (`int`)

Whole numbers without decimal points. Just type the number directly. Remember: no quotes around numbers! `25` is an integer, but `"25"` would be text.

```python
age = 25
temperature = -10
num_molecules = 602214085700000
```

### Floating-Point (`float`)

Numbers with decimal points. Essential for scientific calculations. You can use `e` for scientific notation (powers of 10).

```python
pressure = 101.325
molar_mass = 18.015
concentration = 2.5e-3  # Same as 0.0025
avogadro = 6.022e23     # 6.022 times 10^23
```

## Strings (`str`)

Text data. **Must be enclosed in quotes** (single `'` or double `"`). Without quotes, Python thinks you're referring to a variable name.

```python
element = "Carbon"
formula = 'H2O'
description = """This is a 
multi-line string"""
```

:::{warning}
`Carbon` without quotes causes an error (Python looks for a variable named Carbon). `"Carbon"` with quotes is correct.
:::

## Booleans (`bool`)

Only two possible values: `True` or `False`. Used for conditions. Note the capital letters and no quotes.

```python
is_exothermic = True
reaction_complete = False
```

:::{warning}
`true` (lowercase) causes an error. `"True"` (with quotes) is a string, not a boolean. Always use `True` or `False` with capital letters and no quotes.
:::

## Checking Types

Use `type()` to check any variable's type:

```python
x = 3.14
print(type(x))  # <class 'float'>

name = "Reactor"
print(type(name))  # <class 'str'>
```

## Type Conversion

Convert between types when needed:

```python
# String to number
user_input = "25.5"
temperature = float(user_input)  # 25.5

# Number to string
pressure = 101.325
text = str(pressure)  # "101.325"

# Float to integer (truncates!)
value = int(3.99)  # 3 (not 4!)
```

:::{warning}
`int()` truncates toward zero, it does NOT round!
```python
int(3.9)   # → 3
int(-3.9)  # → -3
```
:::

## Next Steps

Continue to [Variables & Operators](variables.md) to learn how to work with these data types.
