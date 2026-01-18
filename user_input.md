---
title: User Input
---

# User Input

## Getting Data from the User

Sometimes your program needs information from the person running it: a temperature, a number of iterations, or a filename. Python's `input()` function lets you ask for this.

In numerical methods, interactive input is useful for:
- Testing your code with different parameter values (mass, drag coefficient, step size)
- Running "what-if" scenarios without editing the code
- Building simple tools for lab partners who don't want to modify Python files

---

## The input() Function

```python
name = input("Enter your name: ")
print(f"Hello, {name}!")
```

When this runs, the program pauses and waits for you to type something. After you press Enter, whatever you typed is stored in the variable.

```
Enter your name: Sumit
Hello, Sumit!
```

---

## Important: input() Always Returns a String

Even if the user types a number, Python treats it as text:

```python
value = input("Enter a number: ")
print(type(value))
```

```
Enter a number: 42
<class 'str'>
```

This matters because you can't do math with strings:

```python
value = input("Enter a temperature: ")
new_value = value + 10  # ERROR! Can't add str and int
```

---

## Converting Input to Numbers

Use `int()` or `float()` to convert the text to a number:

```python
temp_str = input("Enter temperature (K): ")
temp = float(temp_str)  # Convert to a decimal number

# Now you can do math
temp_celsius = temp - 273.15
print(f"That's {temp_celsius:.2f} °C")
```

You can do this in one line:
```python
temp = float(input("Enter temperature (K): "))
```

### int() vs float()

- Use `int()` for whole numbers (iterations, counts, indices)
- Use `float()` for decimal numbers (temperatures, concentrations, pressures)

```python
n_iterations = int(input("How many iterations? "))
pressure = float(input("Enter pressure (kPa): "))
```

---

## Handling Bad Input

What if the user types "hello" when you asked for a number?

```python
value = float(input("Enter a number: "))
```

```
Enter a number: hello
ValueError: could not convert string to float: 'hello'
```

Your program crashes! To handle this gracefully, use try/except:

```python
user_input = input("Enter a number: ")

try:
    value = float(user_input)
    print(f"You entered: {value}")
except ValueError:
    print("That's not a valid number!")
```

### Asking Again Until Valid Input

```python
while True:
    user_input = input("Enter a positive number: ")
    try:
        value = float(user_input)
        if value > 0:
            break  # Valid input, exit the loop
        else:
            print("Number must be positive!")
    except ValueError:
        print("That's not a valid number!")

print(f"Using value: {value}")
```

---

## Practical Example: Simple Calculator

```python
print("Temperature Converter")
print("---------------------")

temp_str = input("Enter temperature: ")
unit = input("Is this (C)elsius or (K)elvin? ")

temp = float(temp_str)

if unit.upper() == "C":
    kelvin = temp + 273.15
    print(f"{temp} °C = {kelvin:.2f} K")
elif unit.upper() == "K":
    celsius = temp - 273.15
    print(f"{temp} K = {celsius:.2f} °C")
else:
    print("Unknown unit. Please enter C or K.")
```

The `.upper()` method converts the input to uppercase, so both "c" and "C" work.

---

## Getting Multiple Values

### One at a time:
```python
x1 = float(input("Enter x1: "))
x2 = float(input("Enter x2: "))
```

### On one line (space-separated):
```python
line = input("Enter two numbers (space-separated): ")
parts = line.split()  # Split by whitespace
x1 = float(parts[0])
x2 = float(parts[1])
```

Or more compactly:
```python
x1, x2 = map(float, input("Enter two numbers: ").split())
```

This uses `split()` to break the string into parts and `map()` to convert each part to a float.

---

## Quick Reference

| Task | Code |
|------|------|
| Get text input | `name = input("Prompt: ")` |
| Get integer | `n = int(input("Prompt: "))` |
| Get decimal | `x = float(input("Prompt: "))` |
| Handle errors | `try: ... except ValueError: ...` |
| Convert to uppercase | `text.upper()` |
| Split by spaces | `text.split()` |

---

## When to Use input()

`input()` is great for:
- Quick scripts you run from the terminal
- Interactive tools
- Testing your functions with different values

For more complex programs, you'll often use:
- Command-line arguments
- Reading from files
- Configuration files

But `input()` is a good starting point!

## Next Steps

Continue to [Common Functions](common_functions.md) to learn about built-in functions you'll use frequently.
