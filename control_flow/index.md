---
title: Control Flow
---

# Control Flow

## What If I Need to Repeat Something 1000 Times?

Here's the falling parachutist problem again. We want to compute velocity at *every second* from t = 0 to t = 12 using Euler's method:

$$v(t_{i+1}) = v(t_i) + \left( g - \frac{c}{m} v(t_i) \right) \Delta t$$

Without control flow, you'd write this:

```python
v0 = 0
v1 = v0 + (9.8 - 12.5/68.1 * v0) * 2
v2 = v1 + (9.8 - 12.5/68.1 * v1) * 2
v3 = v2 + (9.8 - 12.5/68.1 * v2) * 2
v4 = v3 + (9.8 - 12.5/68.1 * v3) * 2
v5 = v4 + (9.8 - 12.5/68.1 * v4) * 2
v6 = v5 + (9.8 - 12.5/68.1 * v5) * 2
```

That's painful. And what if you need 1000 time steps for accuracy? Or what if you want to stop when velocity reaches 99% of terminal velocity?

**Control flow** solves this:
- **Loops** let you repeat the same calculation as many times as needed
- **If/else** let your code make decisions (like: has the parachute opened?)

With control flow, the parachutist simulation becomes:

```python
v = 0

# range(0, 14, 2) generates: 0, 2, 4, 6, 8, 10, 12
#       ^   ^   ^
#       |   |   step size (increment by 2 each time)
#       |   stop before this value
#       start value

for t in range(0, 14, 2):
    print("t =", t, "s, v =", round(v, 2), "m/s")
    v = v + (9.8 - 12.5/68.1 * v) * 2
```

Six lines instead of twelve. And changing to 1000 steps? Just change the range.

---

## Topics

- [If/Else Statements](if_else.md): Make decisions based on conditions
- [Loops](loops.md): Repeat actions efficiently
