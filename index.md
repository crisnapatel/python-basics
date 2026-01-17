---
title: Computational Techniques — Python Basics
subtitle: A practical guide for CHL7002 students at IIT Delhi
---

# Welcome

This resource is designed to help you learn Python programming for the **CHL7002: Computational Techniques for Chemical Engineers** course.

## What You'll Learn

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
t, C = data["time"], data["concentration"]

E = C / np.trapz(C, t)                    # Normalize to get E(t)
t_mean = np.trapz(t * E, t)               # Mean residence time
variance = np.trapz((t - t_mean)**2 * E, t)  # Variance

print(f"Mean residence time: {t_mean:.2f} s")
print(f"Variance: {variance:.2f} s²")
```

Six lines. Run it once, and it works for any dataset—500 points or 50,000. Change the experiment? Just point it to a new file. Want to plot E(t)? Add two more lines. Want to compare 10 experiments? Wrap it in a loop.

This is why you learn to code: **not because it's required, but because it makes you faster, less error-prone, and capable of tackling problems that would be impractical by hand.**

---

> "One student asked me: why code? What's the point?"

Here's the reality: many problems in chemical engineering **don't have analytical solutions**. You can't solve them by hand.

**Examples you'll encounter in this course:**

| Problem | Why You Need Code |
|---------|-------------------|
| PFR volume from a complex rate law | The integral $V = F_{A0} \int \frac{dX_A}{-r_A}$ often has no closed-form solution |
| Flash calculations with Peng-Robinson EOS | Solving $\sum \frac{z_i(K_i - 1)}{1 + V(K_i - 1)} = 0$ requires iterative numerical methods |
| Non-isothermal reactor design | Coupled energy and mass balances → systems of ODEs |
| Fitting rate constants to experimental data | Parameter estimation requires optimization algorithms |
| Mean residence time from RTD data | Your E(t) curve is experimental data points, not an equation |

**Beyond this course:**
- CFD simulations (Navier-Stokes + reactions)
- Molecular dynamics for property prediction
- Process optimization (yield, energy consumption)
- Machine learning for fault detection and control

Python is the tool that lets you solve these problems.

## Getting Started

Start with [Data Types](datatypes.md) to learn the building blocks of Python.
