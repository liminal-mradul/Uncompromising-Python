
# 📘 Chapter 16: Inheritance, Polymorphism, and Composition

> *"Code is not built in isolation — it grows by standing on the shoulders of existing structures."*

---

## 🎯 Chapter Goals

By the end of this chapter, readers will:

* Understand **inheritance** and when to use it.
* Create **base classes** and extend them.
* Override methods and use `super()` effectively.
* Implement **polymorphism** for flexible code.
* Use **multiple inheritance** safely.
* Understand **mixins** and when to apply them.
* Use `isinstance()` and `issubclass()` for type checking.
* Prefer **composition over inheritance** when appropriate.

---

## 📂 Chapter Structure

### 16.1 Why Inheritance Exists

* Reusability — avoiding code duplication.
* Hierarchies in the real world (Animal → Mammal → Dog).
* When inheritance is overkill or harmful.

📦 **Philosophy Box:**
*"Inheritance is like DNA — it passes traits forward, but can also carry baggage."*

---

### 16.2 Basic Inheritance

```python
class Animal:
    def speak(self):
        print("Some sound")

class Dog(Animal):
    pass

d = Dog()
d.speak()
```

* Parent-child relationship.
* Implicit method/attribute inheritance.

---

### 16.3 Method Overriding

* Redefining a method in a subclass.
* Preserving parent behavior with `super()`.

```python
class Dog(Animal):
    def speak(self):
        super().speak()
        print("Woof!")
```

---

### 16.4 The `super()` Function Deep Dive

* How `super()` resolves the method chain (MRO — Method Resolution Order).
* When `super()` is **necessary** vs optional.

---

### 16.5 Polymorphism — One Interface, Many Forms

* Same method name, different class behavior.
* Example: `draw()` for different shapes.
* Duck typing:

```python
def make_it_speak(animal):
    animal.speak()  # Works as long as object has speak()
```

---

### 16.6 Abstract Base Classes (ABC)

* Enforcing a method contract without implementation.
* Using `abc` module:

```python
from abc import ABC, abstractmethod
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```

---

### 16.7 Multiple Inheritance

* Combining traits from multiple parents.
* MRO in multiple inheritance.
* Dangers: diamond problem & ambiguity.

---

### 16.8 Mixins — Behavior Injection

* Small, reusable classes providing extra methods.
* Example: `LoggingMixin`, `SerializationMixin`.
* Naming convention: always end in `Mixin`.

---

### 16.9 Type Checking — `isinstance()` and `issubclass()`

```python
isinstance(obj, Class)
issubclass(SubClass, ParentClass)
```

* When to use them vs duck typing.

---

### 16.10 Composition — An Alternative to Inheritance

* "Has-a" relationship vs "Is-a".
* Example:

```python
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()
```

📦 **Pro Insight Box:**
*"If you only need a feature, compose it; if you need a full identity, inherit it."*

---

### 16.11 OOP Design Choices — Inheritance vs Composition

* Favor composition when features are independent.
* Favor inheritance when entities truly share identity and core behavior.

---

### 16.12 Common Pitfalls with Inheritance

* Deep inheritance trees → hard to maintain.
* Misusing inheritance for code reuse instead of proper design.
* Overriding methods without calling `super()` when needed.

---

## 📦 Bonus Boxes

* 📌 *Under the Hood:* How Python’s MRO is computed.
* 🧪 *Mini Lab:* Create a `FlyingCar` using multiple inheritance from `Car` and `Airplane`.
* ⚙️ *Design Tip:* Keep inheritance hierarchies shallow — most classes shouldn’t have more than 1–2 parent levels.

---

## 🧠 Concept Recall

* What’s the difference between inheritance and composition?
* Why might deep inheritance trees be bad?
* How does `super()` decide what to call?

---

## ✅ Mastery Checklist

* [ ] I can create base and derived classes.
* [ ] I can override methods correctly with `super()`.
* [ ] I understand multiple inheritance and MRO.
* [ ] I know when to use composition instead of inheritance.

---

## 🧾 Cheatsheet (Chapter 16)

```python
# Basic inheritance
class Parent:
    def greet(self):
        print("Hello")

class Child(Parent):
    pass

# Overriding + super
class Dog(Animal):
    def speak(self):
        super().speak()
        print("Woof!")

# Multiple inheritance
class A: pass
class B: pass
class C(A, B): pass

# Composition
class Engine:
    def start(self): print("Engine on")
class Car:
    def __init__(self):
        self.engine = Engine()
```

---

## 🔗 Transition to Chapter 17 — Advanced Functions: Lambda, Map, Filter, Reduce

Inheritance and composition give you structure.
Now, we’ll explore **functional techniques** to make your methods and data processing more elegant and efficient.

---

