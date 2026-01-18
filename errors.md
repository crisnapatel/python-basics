---
title: Error Handling
---

# Common Python Errors

## Don't Panic When You See Red

Here's a secret: **professional programmers see errors constantly**. The difference between a beginner and an expert isn't that experts write perfect code. It's that experts can *read* the error message and fix the problem in 30 seconds.

When you see a wall of red text, don't panic. Python is trying to help you. It's saying: "Something went wrong, and here's exactly where and why."

This page shows you the most common errors you'll encounter. Learn to recognize them, and you'll debug code 10× faster.

---

## TypeError
```python
# Wrong: mixing types
result = "5" + 3  # TypeError: can only concatenate str to str

# Fix: convert types
result = int("5") + 3  # 8
```

## NameError
```python
# Wrong: variable not defined
print(temperatrue)  # NameError: name 'temperatrue' is not defined

# Fix: check spelling
temperature = 300
print(temperature)
```

## KeyError
```python
# Wrong: key doesn't exist
data = {"temp": 300}
print(data["pressure"])  # KeyError: 'pressure'

# Fix: use .get() with default
print(data.get("pressure", "Not found"))
```

## FileNotFoundError
```python
# Wrong: file doesn't exist
f = open("data.txt")  # FileNotFoundError

# Fix: check path or handle error
try:
    f = open("data.txt")
except FileNotFoundError:
    print("File not found!")
```

## How to Read Error Messages

```
Traceback (most recent call last):
  File "script.py", line 5, in <module>    ← WHERE (file, line)
    result = x / 0
             ~~^~~
ZeroDivisionError: division by zero         ← WHAT went wrong
```

**Always read from bottom up!**
