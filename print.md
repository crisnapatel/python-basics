---
title: The print() Function
---

# The print() Function

## How Do I See What My Code Is Doing?

When you run code, Python does calculations silently. If you don't print anything, you have no idea what's happening. Did the velocity calculation work? Is the loop running? What value does `x` have right now?

`print()` is your window into what your code is doing. You'll use it constantly for:
- Checking if your calculations are correct
- Debugging when something goes wrong
- Displaying results to the user

---

## Basic Printing

### Print text (a string)

Text must be inside quotes (double `"` or single `'`).

```python
print("Hello, world!")    # Double quotes around text
print('Hello, world!')    # Single quotes work too (same result)
```
Output: `Hello, world!`

### Print a variable (no quotes!)

Variables go **outside** quotes. If you put quotes around a variable name, Python thinks it's just text.

```python
temperature = 298.15

print(temperature)        # Correct: prints the VALUE 298.15
print("temperature")      # Wrong: prints the WORD "temperature"
```
Output:
```
298.15
temperature
```

See the difference? `temperature` (no quotes) gives you the value. `"temperature"` (with quotes) gives you the literal word.

### Print multiple things

Separate items with commas. Python adds spaces between them automatically. Notice how text is quoted but the variable is not:

```python
temperature = 298.15
print("Temperature:", temperature, "K")
```
Output: `Temperature: 298.15 K`

---

## f-strings (Recommended)

f-strings are the modern way to format output. Two key things:
1. Put `f` **before** the opening quote
2. Put variables inside `{}` curly braces

### Basic usage

```python
T = 298.15
print(f"Temperature is {T} K")
```
Output: `Temperature is 298.15 K`

The `f` before the quote tells Python "look for curly braces and substitute variables." Without the `f`, it would print literally `{T}` instead of `298.15`.

Compare this to the comma approach:
```python
print("Temperature is", T, "K")   # Works, but harder to read
print(f"Temperature is {T} K")    # f-string: cleaner, all in one string
```

### Control decimal places with `:.Nf`

The `N` is the number of decimal places you want.

```python
P = 101.32567

print(f"Pressure: {P:.2f} kPa")   # 2 decimal places
print(f"Pressure: {P:.4f} kPa")   # 4 decimal places
print(f"Pressure: {P:.0f} kPa")   # 0 decimal places (integer)
```
Output:
```
Pressure: 101.33 kPa
Pressure: 101.3257 kPa
Pressure: 101 kPa
```

### Scientific notation with `:.Ne`

Useful for very large or very small numbers.

```python
avogadro = 6.022e23
conc = 0.00025

print(f"Avogadro's number: {avogadro:.2e}")
print(f"Concentration: {conc:.2e} mol/L")
```
Output:
```
Avogadro's number: 6.02e+23
Concentration: 2.50e-04 mol/L
```

### Calculations inside `{}`

You can put expressions, not just variables.

```python
T_kelvin = 298.15
print(f"Temperature in Celsius: {T_kelvin - 273.15:.1f} C")
```
Output: `Temperature in Celsius: 25.0 C`

### Padding and alignment

Useful for making tables look nice.

```python
# Right-align in 10 characters
x = 42
print(f"Value: {x:>10}")   # "Value:         42"

# Left-align in 10 characters
print(f"Value: {x:<10}!")  # "Value: 42        !"

# Pad numbers with zeros
print(f"Value: {x:05}")    # "Value: 00042"
```

---

## Combining Multiple Variables

```python
g = 9.8
m = 68.1
c = 12.5
t = 10

v = (g * m / c) * (1 - 2.71828**(-c/m * t))

# All on one line
print(f"At t = {t} s, velocity = {v:.2f} m/s")
```
Output: `At t = 10 s, velocity = 44.87 m/s`

---

## Printing in Loops

Very useful for seeing what happens at each step.

```python
v = 0
g, c, m, dt = 9.8, 12.5, 68.1, 2

for t in range(0, 14, 2):
    print(f"t = {t:2d} s, v = {v:5.2f} m/s")
    #        ^^^^         ^^^^^
    #        |            5 characters wide, 2 decimal places
    #        2 characters wide (pads with space)
    v = v + (g - c/m * v) * dt
```
Output:
```
t =  0 s, v =  0.00 m/s
t =  2 s, v = 19.60 m/s
t =  4 s, v = 32.00 m/s
t =  6 s, v = 39.85 m/s
t =  8 s, v = 44.82 m/s
t = 10 s, v = 47.97 m/s
t = 12 s, v = 49.96 m/s
```

---

## Older Styles (You'll See These)

You don't need to use these, but you'll encounter them in older code.

### %-formatting (C-style)

```python
V = 0.0245
print("Volume: %.4f m3" % V)
```
Output: `Volume: 0.0245 m3`

### .format() method

```python
V = 0.0245
print("Volume: {:.4f} m3".format(V))
```
Output: `Volume: 0.0245 m3`

:::{tip}
Use **f-strings** for new code. They're easier to read and less error-prone.
:::

---

## Common Mistakes

### Forgetting the `f`

```python
T = 300
print("Temperature is {T}")   # WRONG: prints literally "{T}"
print(f"Temperature is {T}")  # CORRECT: prints "Temperature is 300"
```

### Using wrong quotes

```python
# If your string contains quotes, use the other type
print(f"It's {T} Kelvin")     # Single quote inside double quotes: OK
print(f'Temperature: {T} K')  # No quotes inside: OK
```

## Next Steps

Continue to [Control Flow](control_flow/index.md) to learn about conditionals and loops.
