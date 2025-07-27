

## 🔥 Chapter 5: Control Flow — If, Else, Elif Patterns (Expanded Edition)

---

### 🧠 FOUNDATIONAL THEORY

#### 1. **Decision-Making in Programs**

* Why conditional logic exists
* Mapping real-world decision trees to `if/else` structures
* Flowchart to code mapping

#### 2. **Boolean Evaluation (Deep Dive)**

* The `bool()` constructor and implicit casting rules
* Operator precedence in boolean logic
* Internals: how Python evaluates composite conditions like `not A or B and C`

---

### 🔍 COMPREHENSIVE CONTROL FLOW TOOLS

#### 3. **Python’s Control Constructs**

| Construct    | Purpose                            | Example           |
| ------------ | ---------------------------------- | ----------------- |
| `if`         | Test a single condition            | `if age > 18:`    |
| `elif`       | Test additional condition(s)       | `elif age == 18:` |
| `else`       | Catch-all fallback                 | `else:`           |
| `match-case` | Pattern-based conditional (>=3.10) | `match status:`   |

#### 4. **The Flow Pyramid**

A design principle:

1. Use `if` for binary decisions
2. Use `elif` for mutual exclusivity
3. Use early `return` or `continue` to flatten logic
4. Use `match-case` for structured pattern control
5. Use dictionaries for functional mapping

---

### 🧱 EXTENDED PATTERNS & PYTHONIC APPLICATIONS

#### 5. **Flattening vs Nesting Logic**

```python
# Bad
if user:
    if user["active"]:
        print("Welcome!")

# Better
if user and user["active"]:
    print("Welcome!")
```

#### 6. **EAFP vs LBYL**

* **EAFP**: "Easier to Ask Forgiveness than Permission"
* **LBYL**: "Look Before You Leap"

```python
# LBYL
if "key" in d:
    value = d["key"]

# EAFP
try:
    value = d["key"]
except KeyError:
    value = None
```

#### 7. **Chained Conditionals with `all()` / `any()`**

```python
if all([x > 0, y > 0, z > 0]):
    print("All positive")

if any([x == 0, y == 0]):
    print("At least one zero")
```

#### 8. **Early Exits & Guards**

```python
def process(data):
    if not data:
        return "Invalid input"  # Early exit (guard clause)
    # rest of the code
```

---

### 🧰 ADVANCED STRUCTURAL PATTERNS

#### 9. **`match-case` Deep Patterns (Python 3.10+)**

```python
match user:
    case {"role": "admin", "active": True}:
        print("Admin dashboard")
    case {"role": "guest"}:
        print("Guest mode")
    case _:
        print("Unknown user")
```

* Nested destructuring
* Combining with guards: `case x if x > 5:`
* Matching on class instances

#### 10. **Functional Mapping of Logic**

```python
def handle_admin(): ...
def handle_guest(): ...
def handle_default(): ...

handlers = {
    "admin": handle_admin,
    "guest": handle_guest
}

handlers.get(user.role, handle_default)()
```

---

### 🧨 GOTCHAS & EDGE CASES

#### 11. **Confusing Assignment vs Comparison**

```python
# Common beginner error (won’t compile in Python!)
if x = 5:  # ❌
```

#### 12. **Falsy Traps**

```python
# May behave unexpectedly if x = 0 or ""
if x:  # Fails even though x is a legit value
    ...
```

#### 13. **Identity (`is`) vs Equality (`==`)**

```python
# This fails!
if x is 5:  # ❌ identity test
```

---

### 🧪 APPLICATION DOMAINS

#### ✅ Data Validation

```python
if not email:
    return "Missing email"
if "@" not in email:
    return "Invalid email"
```

#### ✅ CLI Argument Routing

```python
if args.verbose:
    print("Running in verbose mode")
```

#### ✅ Web Request Routing (like Flask)

```python
if request.method == "POST":
    handle_post()
elif request.method == "GET":
    handle_get()
else:
    return "405 Method Not Allowed"
```

#### ✅ Game Logic (Match-case + functional)

```python
match action:
    case "move":
        player.move()
    case "attack":
        player.attack()
```

---

### 🧠 PHILOSOPHICAL ASPECTS

* **“Flat is better than nested.”**
* Avoid control flow abuse → prefer readability
* Compose decisions, don’t tangle them

---


1. `chapter5/practice.md` – Practice problems & applied logic.
2. `chapter5/concept-recall.md` – Targeted questions to reinforce.
3. `chapter5/checklist.md` – Mastery checklist of all patterns.
4. `chapter5/cheatsheet.md` – Summary + syntax snapshots.

