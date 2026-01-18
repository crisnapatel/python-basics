---
title: Loops
---

# Loops

## Every Numerical Method Needs This

Numerical methods are fundamentally about **repetition**. Whether it's:
- Euler's method: repeat "compute next value" 1000 times
- Newton-Raphson: repeat "improve guess" until error is small enough  
- Simulations: repeat "update state" for each time step

You can't do computational engineering without loops. They're the engine that drives every numerical algorithm.

---

## For Loop

Use `for` when you know how many times you want to repeat something.

### Euler's method for falling parachutist

The loop repeats the indented code for each value of `t`. Here, `range(0, 14, 2)` gives us: 0, 2, 4, 6, 8, 10, 12.

```python
g = 9.8
c = 12.5
m = 68.1
dt = 2
v = 0

for t in range(0, 14, 2):
    print(f"t = {t:2d} s, v = {v:5.2f} m/s")
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

### How `range()` works

```python
range(5)         # 0, 1, 2, 3, 4        (start defaults to 0, stop at 5)
range(2, 7)      # 2, 3, 4, 5, 6        (start at 2, stop before 7)
range(0, 10, 2)  # 0, 2, 4, 6, 8        (start at 0, stop before 10, step by 2)
range(10, 0, -1) # 10, 9, 8, ..., 1     (count backwards)
```

### Looping over a list

Read `for compound in compounds` as "for each compound in the list compounds, do..."

The loop variable (`compound`) is a new variable created by the loop. It takes on each value from the list, one at a time. You can name it anything you want.

```python
compounds = ["methane", "ethane", "propane"]

for compound in compounds:
    print(compound)
```

Output:
```
methane
ethane
propane
```

---

## While Loop

Use `while` when you don't know how many iterations you need. The loop keeps running as long as the condition is `True`.

### How while works

```python
count = 0
while count < 3:
    print(count)
    count = count + 1
```
Output: `0, 1, 2` (stops when count becomes 3)

:::{warning}
Always update the variable in your condition! Otherwise the loop runs forever.
:::

### Example: iterate until convergence

How long until the parachutist reaches 99% of terminal velocity? We don't know in advance, so we use `while`.

```python
g, c, m, dt = 9.8, 12.5, 68.1, 0.1
v_terminal = g * m / c

v = 0
t = 0

while v < 0.99 * v_terminal:
    v = v + (g - c/m * v) * dt
    t = t + dt

print(f"Reached 99% terminal velocity at t = {t:.1f} s")
```
Output: `Reached 99% terminal velocity at t = 25.1 s`

### Decaying concentration

```python
concentration = 1.0
while concentration > 0.1:
    concentration = concentration * 0.5
    print(f"C = {concentration}")
```
