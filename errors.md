---
title: Error Handling
---
# Common Python Errors

Learn to read error messages — they tell you exactly what's wrong!

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
