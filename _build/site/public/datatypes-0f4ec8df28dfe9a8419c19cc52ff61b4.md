---
title: Data Types
---

# Data Types in Python

Python has several built-in data types. Understanding them is fundamental to writing correct code.

## Numbers

### Integers (`int`)

Whole numbers without decimal points.

```python
# Integer examples
age = 25
temperature = -10
num_molecules = 6022140857000000000000000  # Avogadro's number approximation
```

### Floating-Point (`float`)

Numbers with decimal points — essential for scientific calculations.

```python
# Float examples
pressure = 101.325  # kPa
molar_mass = 18.015  # g/mol for water
concentration = 2.5e-3  # 0.0025 mol/L (scientific notation)
```

## Strings (`str`)

Text data enclosed in quotes.

```python
# String examples
element = "Carbon"
formula = 'H2O'
description = """This is a 
multi-line string"""
```

## Booleans (`bool`)

True or False values — used for conditions.

```python
# Boolean examples
is_exothermic = True
reaction_complete = False
```

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
