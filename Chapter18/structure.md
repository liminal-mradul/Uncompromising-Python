

# 📘 Chapter 18: Decorators and Closures

> *"Functions can wrap other functions, much like a gift — adding something extra without touching what’s inside."*

---

## 🎯 Chapter Goals

By the end of this chapter, readers will:

* Understand **closures** and how they capture variables.
* Write functions that return other functions.
* Build **custom decorators** to add extra behavior.
* Use `functools.wraps` to preserve metadata.
* Implement practical decorators (logging, timing, caching).
* Stack multiple decorators without confusion.
* Recognize common pitfalls and avoid decorator overuse.

---

## 📂 Chapter Structure

### 18.1 Functions Returning Functions — The First Step

* Functions can create and return other functions.
* Example:

```python
def outer():
    def inner():
        print("Hello")
    return inner
```

* Why this matters — **basis for closures & decorators**.

---

### 18.2 Closures — Capturing Outer Variables

* Functions that **remember the environment** in which they were created.
* Example:

```python
def multiplier(factor):
    def multiply_by(x):
        return x * factor
    return multiply_by

double = multiplier(2)
print(double(5))  # 10
```

* Rules:

  * Inner function references variables from outer scope.
  * Outer function has finished executing, but data is retained.

📦 **Philosophy Box:**
*"Closures are functions with memory — they keep their past alive."*

---

### 18.3 Introduction to Decorators

* A decorator is just **a function that takes a function and returns a function**.
* The `@decorator` syntax is just syntactic sugar.

Example without sugar:

```python
def my_decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

def say_hello():
    print("Hello")

say_hello = my_decorator(say_hello)
```

Example with sugar:

```python
@my_decorator
def say_hello():
    print("Hello")
```

---

### 18.4 Preserving Function Metadata — `functools.wraps`

* Without it, decorated functions lose their `__name__` and `__doc__`.
* Using `wraps`:

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

---

### 18.5 Practical Decorator Examples

1. **Logging**

```python
def log_calls(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with {args} {kwargs}")
        return func(*args, **kwargs)
    return wrapper
```

2. **Timing Execution**

```python
import time
def timing(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end-start:.4f}s")
        return result
    return wrapper
```

3. **Caching Results** (without `lru_cache`)

```python
def simple_cache(func):
    cache = {}
    @wraps(func)
    def wrapper(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]
    return wrapper
```

---

### 18.6 Stacking Multiple Decorators

* Decorators are applied **bottom to top**.

```python
@log_calls
@timing
def slow_add(a, b):
    time.sleep(1)
    return a + b
```

---

### 18.7 Decorators with Arguments

* Decorators can be parameterized by **creating a factory function**.

```python
def repeat(n):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet():
    print("Hello")
```

---

### 18.8 Class-Based Decorators

* When decorators need to maintain state across calls.

```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0
    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"Call {self.count}")
        return self.func(*args, **kwargs)
```

---

### 18.9 Built-in Decorators to Know

* `@staticmethod`, `@classmethod`, `@property`.
* `@functools.lru_cache` — built-in memoization.

---

### 18.10 Common Pitfalls with Decorators

* Making decorators too complex → unreadable code.
* Forgetting `wraps()` → loss of function identity.
* Using decorators where simple function calls would be clearer.

---

## 📦 Bonus Boxes

* 📌 *Under the Hood:* How `@decorator` syntax works in bytecode.
* 🧪 *Mini Lab:* Write a decorator that retries a function call 3 times if it raises an exception.
* ⚙️ *Tech Tip:* Use decorators in Flask/Django routes for authentication.

---

## 🧠 Concept Recall

* What’s the difference between a closure and a decorator?
* Why use `functools.wraps`?
* How are stacked decorators applied?

---

## ✅ Mastery Checklist

* [ ] I can create closures that remember variables.
* [ ] I can write decorators with and without arguments.
* [ ] I can preserve metadata using `wraps`.
* [ ] I know when to avoid decorators for clarity.

---

## 🧾 Cheatsheet (Chapter 18)

```python
# Basic decorator
def deco(func):
    def wrapper(*args, **kwargs):
        print("Before")
        result = func(*args, **kwargs)
        print("After")
        return result
    return wrapper

@deco
def hello(): print("Hello")

# Closure
def multiplier(factor):
    def inner(x): return x * factor
    return inner

# With wraps
from functools import wraps
def log_calls(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper
```

---

## 🔗 Transition to Chapter 19 — Working with Time, Date, and Schedulers

Decorators give you **power to wrap functionality**;
next, we’ll work with **time-related programming** to control when and how code executes.

---

If you want, I can make a **visual diagram showing closure variable binding** so readers really “see” how outer variables are captured.

Do you want me to add that?
