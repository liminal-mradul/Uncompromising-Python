
# 📘 Chapter 14: Modular Programming and `import` Mastery

> *"Good code is like good architecture — built in modules, not monoliths."*

---

## 🎯 Chapter Goals

By the end of this chapter, readers will:

* Organize Python code into **modules and packages** like professional developers.
* Understand how **`import` works internally** (module search, caching).
* Use **every `import` syntax** effectively (`from`, `as`, `*`, relative imports).
* Write scripts that **run standalone or as imports** without side effects.
* Control what’s **exposed** from a module using `__all__`.
* Avoid common **import pitfalls** like circular imports.
* Structure **multi-file projects** for readability and maintainability.

---

## 📂 Chapter Structure

### 14.1 Why Modular Programming?

* Breaking large programs into smaller, reusable files.
* Benefits: maintainability, reusability, collaboration.

📦 **Philosophy Box:**
*"If your program is a novel, each module is a chapter — complete, self-contained, yet part of the bigger story."*

---

### 14.2 What is a Module?

* Any `.py` file is a module.
* Difference between running and importing a module.

🧪 Example:

```python
# greetings.py
def hello(name):
    print(f"Hello, {name}!")

# main.py
import greetings
greetings.hello("Alice")
```

---

### 14.3 Packages — Organizing Modules

* A folder with `__init__.py` becomes a package.
* Purpose of `__init__.py` (initialization code, controlling public API).

---

### 14.4 The `import` Statement — All Styles

#### 1. Basic Import

```python
import math
print(math.sqrt(16))
```

*Good for importing the whole module when you’ll use multiple functions.*

---

#### 2. Import with Alias (`as`)

```python
import numpy as np
print(np.array([1, 2, 3]))
```

*Best for shortening long module names or following community conventions.*

---

#### 3. Selective Import (`from`)

```python
from math import sqrt
print(sqrt(25))
```

*Good for importing only what you need.*

---

#### 4. Selective Import with Alias (`from ... import ... as`)

```python
from datetime import datetime as dt
print(dt.now())
```

*Helps avoid name clashes or make names more readable.*

---

#### 5. Wildcard Import (`from ... import *`) — **Avoid This**

```python
from math import *
print(sin(0))
```

⚠ **Danger:** Pollutes namespace, hides where functions come from, can overwrite variables.
*Only acceptable in REPL or for generated code.*

---

#### 6. Multiple Imports in One Line

```python
import os, sys
```

⚠ Not PEP 8–recommended; prefer one import per line for clarity.

---

#### 7. Import Inside a Function

```python
def process_data():
    import json
    ...
```

*Use when a dependency is rarely needed or to avoid circular imports.*

---

#### 8. Conditional Imports

```python
try:
    import ujson as json
except ImportError:
    import json
```

*Great for optional performance boosts.*

---

### 14.5 Relative Imports (Inside Packages)

```python
from . import utils        # Same package
from ..common import config  # Parent package
```

*Best for keeping package imports consistent when moving files around.*

---

### 14.6 How `import` Works Internally

* Search order: built-in modules → `sys.path` entries.
* Once imported, module is cached in `sys.modules`.
* Reloading with `importlib.reload()` when needed.

📦 **Under the Hood Box:**
*"`import` compiles a `.py` to `.pyc`, caches it in `__pycache__`, and loads it from memory next time."*

---

### 14.7 Controlling Public API with `__all__`

```python
__all__ = ["main_function", "helper"]
```

*Restricts what `from module import *` brings in.*

---

### 14.8 `if __name__ == "__main__"` Idiom

```python
def main():
    print("Script running")

if __name__ == "__main__":
    main()
```

*Ensures code runs only when executed directly, not on import.*

---

### 14.9 Organizing a Multi-File Project (Best Practice)

```
project/
    package/
        __init__.py
        module1.py
        module2.py
    main.py
```

*Follow PEP 8: group imports — stdlib, third-party, local.*

---

### 14.10 Common Import Pitfalls

* Circular imports — fix by restructuring code or local imports.
* Modifying `sys.path` excessively.
* Using wildcard imports in production code.

---

## 📦 Bonus Boxes

* 📌 *Tech Tip:* Speeding up imports with lazy loading (`importlib.util`).
* 🧪 *Mini Lab:* Break a single 200-line script into 3 modules and import them cleanly.
* ⚙️ *Under the Hood:* Difference between `import` and `__import__()` function.

---

## 🧠 Concept Recall

* When should you use an alias in imports?
* What is `__all__` used for?
* Why should wildcard imports be avoided?
* How does Python avoid re-importing modules?

---

## ✅ Mastery Checklist

* [ ] I can use every `import` syntax fluently.
* [ ] I can write code that’s import-safe.
* [ ] I can structure packages with relative and absolute imports.
* [ ] I know how to avoid circular imports.

---

## 🧾 Cheatsheet (Chapter 14)

```python
# Basic import
import math

# Alias
import numpy as np

# Selective
from math import sqrt

# Selective with alias
from datetime import datetime as dt

# Wildcard (avoid in production)
from math import *

# Relative
from . import helper
from ..common import config

# Conditional import
try:
    import ujson as json
except ImportError:
    import json

# Inside function
def run():
    import random
    print(random.randint(1, 10))
```

---

## 🔗 Transition to Chapter 15 — Object-Oriented Programming

With modular thinking in place,
we now move to **designing blueprints for reusable objects** in Python —
a step toward **engineering programs like real-world systems**.

---

