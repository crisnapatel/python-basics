---
title: Computational Techniques — Python Basics
subtitle: A practical guide for CHL7002 students at IIT Delhi
---

# Welcome

This resource is designed to help you learn Python programming for the **CHL7002: Computational Techniques for Chemical Engineers** course.

## What You'll Learn

- **Comments**: Writing code others (and future you) can understand
- **Python Fundamentals**: Variables, data types, operators
- **Control Flow**: Conditionals and loops
- **Functions**: Writing reusable code
- **NumPy & Pandas**: Data manipulation essentials
- **Error Handling**: Reading and fixing common errors

## Why Learn Python?

Imagine you're in the lab and you've just finished a tracer experiment. You have a CSV file with 500 data points of concentration vs. time. Your task: calculate the mean residence time and variance of the RTD.

You could open Excel, manually set up columns, type formulas, drag them down, hope you didn't miss a row, and repeat this every time you run an experiment. Or you could write this:

```python
import pandas as pd
import numpy as np

data = pd.read_csv("tracer_data.csv")
t = data["time"]
C = data["concentration"]

E = C / np.trapz(C, t)                    # Normalize to get E(t)
t_mean = np.trapz(t * E, t)               # Mean residence time
variance = np.trapz((t - t_mean)**2 * E, t)  # Variance

print(f"Mean residence time: {t_mean:.2f} s")
print(f"Variance: {variance:.2f} s²")
```

Six lines. Run it once, and it works for any dataset, whether 500 points or 50,000. Change the experiment? Just point it to a new file. Want to plot E(t)? Add two more lines. Want to compare 10 experiments? Wrap it in a loop.

This is why you learn to code: **not because it's required, but because it makes you faster, less error-prone, and capable of tackling problems that would be impractical by hand.**

---

> "One student asked me: why code? What's the point?"

Here's the reality: many problems in chemical engineering **don't have analytical solutions**. You can't solve them by hand.

**Examples you'll encounter in this course:**

| Problem | What Python Does |
|---------|------------------|
| Compute $e^x$ using Taylor series | Add up terms in a loop, track the error |
| Find roots of equations (bisection, Newton-Raphson) | Repeat a formula until the answer is close enough |
| Molar volume from van der Waals equation | Solve a nonlinear equation iteratively |
| Calculate derivatives numerically | Compute $(f(x+h) - f(x))/h$ for different step sizes |
| Process experimental data from a file | Read CSV, calculate statistics, plot results |

These aren't abstract exercises. The first assignment asks you to compute $e^x$ from the series expansion and track the error at each step. That's a loop, some arithmetic, and print statements. By the end of this module, you'll be able to do it.

**What working engineers use Python for:**

Once you're comfortable with the basics, Python opens doors to real engineering work:
- **Automating calculations**: Run the same analysis on 50 datasets without copy-pasting
- **Plotting and visualization**: Generate publication-quality figures from your data
- **Reading sensor data**: Parse log files from lab equipment
- **Connecting to simulations**: Pre/post-process data for ANSYS, COMSOL, or LAMMPS
- **Building simple GUIs**: Create a tool your lab group can use without coding

Python is the tool that lets you solve these problems.

## Getting Started

Start with [Data Types](datatypes.md) to learn the building blocks of Python.
