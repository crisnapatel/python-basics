---
title: The Parachutist Problem
---

# The Falling Parachutist: Our Running Example

Throughout this tutorial, we'll keep coming back to one problem: **a parachutist jumping from a hot air balloon**. This isn't just a random example. It's the central problem from your textbook (Chapters 1–5), and it demonstrates exactly why you need programming.

By the time you finish this course, you'll be able to simulate this problem yourself.

```{admonition} 🎮 Try the Interactive Simulation
:class: tip

Want to see Euler's method in action before diving into the math? 

<a href="_static/parachutist_simulation.html" style="display: inline-block; background: #579aca; color: white; padding: 10px 20px; border-radius: 6px; text-decoration: none; font-weight: 500; margin-top: 8px;">
▶ Launch Interactive Simulation
</a>

Adjust mass, drag, and time step to see how numerical solutions work!
```

---

## The Setup

A parachutist with mass $m = 68.1$ kg jumps from a stationary hot air balloon. As they fall, two forces act on them:

1. **Gravity pulls them down**: $F_{\text{gravity}} = mg$
2. **Air resistance pushes back up**: $F_{\text{drag}} = cv$

where:
- $g = 9.8$ m/s² (gravitational acceleration)
- $c$ = drag coefficient (depends on body position and parachute)
- $v$ = velocity (how fast they're falling)

The faster you fall, the more air resistance you feel. Eventually, these forces balance out and you stop accelerating. This is called **terminal velocity**.

---

## The Equation

Applying Newton's second law ($F = ma$), we get:

$$m\frac{dv}{dt} = mg - cv$$

Or, solving for the rate of change of velocity:

$$\frac{dv}{dt} = g - \frac{c}{m}v$$

This is a **differential equation**. It tells us how velocity *changes* over time, but not what the velocity *is* at any given time.

---

## The Analytical Solution

For this particular equation, calculus gives us an exact formula:

$$v(t) = \frac{gm}{c}\left(1 - e^{-\frac{c}{m}t}\right)$$

If you plug in $m = 68.1$ kg, $c = 12.5$ kg/s, and $g = 9.8$ m/s², you can calculate the velocity at any time. For example, at $t = 10$ seconds:

$$v(10) = \frac{9.8 \times 68.1}{12.5}\left(1 - e^{-\frac{12.5}{68.1} \times 10}\right) \approx 44.87 \text{ m/s}$$

Great! So why do we need programming?

---

## The Problem: Most Equations Don't Have Analytical Solutions

The parachutist equation is special. We *can* solve it with calculus. But most real engineering problems can't be solved this way:

- What if the drag coefficient changes with velocity ($c = c(v)$)?
- What if air density changes with altitude?
- What if the parachute opens at $t = 5$ seconds and $c$ suddenly jumps from 12.5 to 68?

For these cases, there's no formula. Instead, we use **numerical methods**: we approximate the solution step by step using a computer.

---

## The Numerical Approach: Euler's Method

Here's the key insight. That differential equation:

$$\frac{dv}{dt} = g - \frac{c}{m}v$$

tells us the *slope* of the velocity curve at any point. If we know the velocity now, we can estimate the velocity a short time later:

$$v_{\text{new}} = v_{\text{old}} + \text{slope} \times \Delta t$$

Or in math notation:

$$v(t_{i+1}) = v(t_i) + \left(g - \frac{c}{m}v(t_i)\right) \Delta t$$

This is called **Euler's method**. Start at $t = 0$ with $v = 0$, pick a time step (say, $\Delta t = 2$ seconds), and repeat the calculation over and over.

---

## Why This Matters for Python

Let's trace through the first few steps by hand:

| Step | Time (s) | Velocity (m/s) | Calculation |
|------|----------|----------------|-------------|
| 0 | 0 | 0.00 | Starting value |
| 1 | 2 | 19.60 | $0 + (9.8 - \frac{12.5}{68.1} \times 0) \times 2$ |
| 2 | 4 | 32.00 | $19.6 + (9.8 - \frac{12.5}{68.1} \times 19.6) \times 2$ |
| 3 | 6 | 39.85 | $32.0 + (9.8 - \frac{12.5}{68.1} \times 32.0) \times 2$ |
| ... | ... | ... | ... |

See the pattern? It's the same calculation repeated over and over with different numbers. This is exactly what computers are good at, and exactly what you'll learn to do with Python.

By the end of this tutorial, you'll write code that:
- **Stores** the parameters ($m$, $c$, $g$, $\Delta t$) in variables
- **Repeats** the Euler step calculation in a loop
- **Stores** all the velocity values in a list
- **Compares** the numerical result to the analytical solution

---

## The Parameters You'll See

Throughout the examples, we'll use these values from the textbook:

| Parameter | Symbol | Value | Units |
|-----------|--------|-------|-------|
| Mass | $m$ | 68.1 | kg |
| Drag coefficient (free fall) | $c$ | 12.5 | kg/s |
| Drag coefficient (parachute open) | $c$ | 68.0 | kg/s |
| Gravitational acceleration | $g$ | 9.8 | m/s² |
| Time step | $\Delta t$ | 2.0 | s |
| Terminal velocity | $v_{\text{terminal}}$ | 53.39 | m/s |

When you see `m = 68.1` or `c = 12.5` in code examples, now you know where those numbers come from.

---

## What You'll Learn Through This Problem

As you work through the Python basics, you'll build up the skills to simulate this problem:

| Python Concept | How It Applies |
|----------------|----------------|
| **Variables** | Store $m$, $c$, $g$, $\Delta t$, $v$, $t$ |
| **Arithmetic operators** | Calculate $g - \frac{c}{m}v$ |
| **Loops** | Repeat the Euler step many times |
| **Conditionals** | Change $c$ when parachute opens at $t = 5$ |
| **Lists** | Store velocity at every timestep |
| **Functions** | Package Euler step as reusable code |

By the end, you won't just understand Python. You'll understand how numerical methods actually work.

---

## Next Steps

Now that you know the problem we're solving, let's learn the Python tools you'll need. Start with [Data Types](datatypes.md) to learn about the building blocks of Python.
