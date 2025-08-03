

# 📘 Chapter 20: Regex and Data Validation

> *"Regular expressions are the scalpel of text processing — precise, sharp, and dangerous in untrained hands."*

---

## 🎯 Chapter Goals

By the end of this chapter, readers will:

* Understand **what regex is** and why it’s useful.
* Read and write **basic to advanced** regular expressions.
* Use `re` module functions effectively.
* Perform **searching, matching, and replacing** text.
* Extract specific patterns from large text files.
* Validate user inputs like emails, phone numbers, and passwords.
* Avoid common regex pitfalls (greedy matches, backtracking issues).
* Optimize regex for **performance and readability**.

---

## 📂 Chapter Structure

### 20.1 Introduction to Regular Expressions

* What is regex and why it exists.
* Regex vs normal string methods (`find()`, `split()`).
* When regex is overkill.

📦 **Philosophy Box:**
*"Regex is not magic — it’s math in disguise, using patterns instead of numbers."*

---

### 20.2 The `re` Module — Core Functions

* `re.search()` — find first match.
* `re.match()` — match at start only.
* `re.fullmatch()` — match the whole string.
* `re.findall()` — get all matches as a list.
* `re.finditer()` — match objects as an iterator.
* `re.sub()` — replace text.
* `re.split()` — split by pattern.

---

### 20.3 Basic Pattern Syntax

* Literal characters (`cat` matches “cat”).
* Metacharacters: `. ^ $ * + ? { } [ ] \ | ( )`.
* Escaping special characters: `\.` for a dot.

---

### 20.4 Character Classes & Shortcuts

* `[abc]` — match a, b, or c.
* `[^abc]` — not a, b, or c.
* Ranges: `[a-z]`, `[0-9]`.
* Shorthand:

  * `\d` → digits
  * `\w` → word characters
  * `\s` → whitespace
  * `\D`, `\W`, `\S` → opposites

---

### 20.5 Quantifiers

* `*` — 0 or more.
* `+` — 1 or more.
* `?` — 0 or 1.
* `{n}` — exactly n times.
* `{n,}` — at least n times.
* `{n,m}` — between n and m times.

📌 **Pro Tip:** Always clarify greedy (`+`) vs lazy (`+?`) matches.

---

### 20.6 Anchors & Boundaries

* `^` — start of string.
* `$` — end of string.
* `\b` — word boundary.
* `\B` — non-boundary.

---

### 20.7 Grouping & Capturing

* `(abc)` — capture group.
* `(?:abc)` — non-capturing group.
* `(?P<name>abc)` — named group.
* Accessing groups: `.group()`, `.groups()`, `.groupdict()`.

---

### 20.8 Alternation & Lookarounds

* `a|b` — match a or b.
* Lookahead: `(?=...)` (must be followed by).
* Negative lookahead: `(?!...)`.
* Lookbehind: `(?<=...)` (must be preceded by).
* Negative lookbehind: `(?<!...)`.

---

### 20.9 Flags & Modes

* `re.IGNORECASE` / `re.I`.
* `re.MULTILINE` / `re.M`.
* `re.DOTALL` / `re.S`.
* Combining flags: `re.I | re.M`.

---

### 20.10 Real-World Validation Patterns

1. **Email**:

```python
pattern = r"^[\w\.-]+@[\w\.-]+\.\w{2,}$"
```

2. **Phone Number**:

```python
pattern = r"^\+?[0-9]{7,15}$"
```

3. **Strong Password**:

```python
pattern = r"^(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&]).{8,}$"
```

4. **Date (YYYY-MM-DD)**:

```python
pattern = r"^\d{4}-\d{2}-\d{2}$"
```

---

### 20.11 Searching Large Files with Regex

* `re.finditer()` to avoid loading all matches into memory.
* Using compiled regex:

```python
pattern = re.compile(r"\berror\b", re.I)
for match in pattern.finditer(huge_text):
    print(match.group())
```

---

### 20.12 Common Pitfalls

* Overuse of `.*` → catastrophic backtracking.
* Forgetting raw strings → `r"..."`.
* Poor readability — always comment complex regex.

---

### 20.13 Performance & Readability Tips

* Pre-compile with `re.compile()`.
* Use explicit quantifiers instead of `.*`.
* Break long regex into multiple smaller ones.

---

## 📦 Bonus Boxes

* 📌 *Under the Hood:* How regex engines backtrack.
* 🧪 *Mini Lab:* Extract all hashtags from a text and count frequency.
* ⚙️ *Tech Tip:* Use `regex` module (pip install regex) for advanced Unicode handling.

---

## 🧠 Concept Recall

* What’s the difference between `re.match()` and `re.search()`?
* How do you make a regex case-insensitive?
* What’s the difference between a capturing and non-capturing group?

---

## ✅ Mastery Checklist

* [ ] I can match and extract specific patterns from text.
* [ ] I can validate inputs like email or phone numbers.
* [ ] I know how to use lookaheads/lookbehinds effectively.
* [ ] I can optimize regex for performance.

---

## 🧾 Cheatsheet (Chapter 20)

```python
import re

# Search
re.search(r"cat", "concatenate")

# Match full string
re.fullmatch(r"\d+", "12345")

# Find all
re.findall(r"\b\w+\b", "This is a test")

# Replace
re.sub(r"cat", "dog", "cat sat on mat")

# Compile
pattern = re.compile(r"\d{4}-\d{2}-\d{2}")
if pattern.match("2025-08-03"):
    print("Valid date")
```

---

## 🔗 Transition to Chapter 21 — Command-Line Apps and Argument Parsing

Regex is about **finding meaning in text**;
next, we’ll learn how to make your programs **accept, parse, and act on user input from the terminal**.

---
