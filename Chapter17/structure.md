

# 📘 Chapter 17: Advanced Functions — Lambda, Map, Filter, Reduce

> *"Functions are not just tools; they’re building blocks that can be passed, shaped, and chained like data."*

---

## 🎯 Chapter Goals

By the end of this chapter, readers will:

* Understand **functions as first-class citizens** in Python.
* Write and use **lambda functions** effectively.
* Apply **map()**, **filter()**, and **reduce()** for transformation and aggregation.
* Use **functools** for partial functions, caching, and functional utilities.
* Recognize when functional patterns improve clarity — and when they harm it.
* Combine functional techniques with Pythonic readability.

---

## 📂 Chapter Structure

### 17.1 Functions as First-Class Citizens

* Assigning functions to variables.
* Passing functions as arguments.
* Returning functions from functions.

📦 **Philosophy Box:**
*"In Python, functions are objects — treat them like any other value."*

---

### 17.2 Lambda Functions — Anonymous Power

* Syntax:

```python
lambda args: expression
```

* When to use: small, throwaway functions.
* When **not** to use: multi-line or complex logic.
* Example:

```python
square = lambda x: x ** 2
```

* Common use cases: sorting, quick transformations.

⚠ **Warning Box:**
*"Don’t hide complexity in lambdas — readability wins over brevity."*

---

### 17.3 The `map()` Function — Transformation Pipeline

* Syntax: `map(function, iterable)`.
* Works lazily, returns an iterator.
* Example:

```python
numbers = [1, 2, 3]
squares = list(map(lambda x: x**2, numbers))
```

* Real-world: data normalization, formatting output.

---

### 17.4 The `filter()` Function — Selective Processing

* Syntax: `filter(function, iterable)`.
* Keeps elements where function returns `True`.
* Example:

```python
evens = list(filter(lambda x: x % 2 == 0, numbers))
```

* Real-world: filtering logs, cleaning datasets.

---

### 17.5 The `reduce()` Function — Aggregating Data

* From `functools`:

```python
from functools import reduce
```

* Syntax: `reduce(function, iterable[, initializer])`.
* Example:

```python
from functools import reduce
product = reduce(lambda x, y: x * y, [1, 2, 3, 4])
```

* When to prefer `sum()`, `min()`, `max()` over `reduce()`.

---

### 17.6 Combining map(), filter(), and reduce()

* Chaining transformations:

```python
result = reduce(
    lambda x, y: x + y,
    filter(lambda n: n > 0, map(lambda x: x-1, numbers))
)
```

* Potential readability issues & refactoring to comprehensions.

---

### 17.7 `functools` — Functional Utilities

* `partial()` — pre-filling function arguments.
* `lru_cache()` — memoization for performance.
* `cmp_to_key()` — custom sort order with comparison functions.

Example:

```python
from functools import partial
power_of_two = partial(pow, 2)
```

---

### 17.8 Pythonic Alternatives to Functional Tools

* List comprehensions vs `map()` + `filter()`.
* Generator expressions for lazy evaluation.
* Example transformation with both approaches for clarity comparison.

---

### 17.9 Functional Thinking in Real Applications

* Processing API results.
* Log file analysis.
* Quick data reshaping in ETL pipelines.

---

### 17.10 Common Pitfalls & Anti-Patterns

* Overusing lambdas where `def` is better.
* Chaining too many functional calls (readability loss).
* Forgetting that `map()` and `filter()` return iterators in Python 3.

---

## 📦 Bonus Boxes

* 📌 *Under the Hood:* Why `map()` and `filter()` are faster than equivalent for-loops in some cases.
* 🧪 *Mini Lab:* Transform a CSV column of prices into a list of discounted prices using `map()` and `filter()`.
* ⚙️ *Tech Tip:* Combine `lru_cache()` with recursive functions for massive speed boosts.

---

## 🧠 Concept Recall

* When is it better to use a named function instead of a lambda?
* What’s the difference between `map()` and a list comprehension?
* How does `reduce()` differ from `sum()` or `min()`?

---

## ✅ Mastery Checklist

* [ ] I can write clean, single-expression lambdas.
* [ ] I know how to transform and filter data with functional tools.
* [ ] I understand when to replace functional code with comprehensions.
* [ ] I can optimize functions with `functools` utilities.

---

## 🧾 Cheatsheet (Chapter 17)

```python
# Lambda
square = lambda x: x**2

# Map
list(map(lambda x: x*2, [1, 2, 3]))

# Filter
list(filter(lambda x: x % 2 == 0, range(10)))

# Reduce
from functools import reduce
reduce(lambda x, y: x + y, [1, 2, 3, 4])

# Partial
from functools import partial
pow2 = partial(pow, 2)
pow2(5)  # 32

# Cache
from functools import lru_cache
@lru_cache(maxsize=None)
def fib(n):
    return n if n < 2 else fib(n-1) + fib(n-2)
```

---

## 🔗 Transition to Chapter 18 — Decorators and Closures

We’ve seen how functions can be **passed around and chained** —
next, we’ll explore **how to wrap them** to add behavior without changing their code.

---

