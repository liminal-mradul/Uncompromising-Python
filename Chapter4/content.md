
# 📘 **Chapter 4: Operators and Expressions in Depth**

*Power in Every Symbol — Every Operator, Understood and Tamed*

-----

Welcome to Chapter 4, where we delve into the fundamental building blocks of all Python programs: **operators** and **expressions**. In Chapter 3, we explored data types and how variables reference objects in memory. Now, we'll learn how to actually *do* things with those objects—how to combine them, transform them, and make decisions based on them.

An uncompromising programmer doesn't just know what an operator does; they understand *how* it works, its subtleties, and how it fits into Python's expression-oriented design. Mastering operators is key to writing concise, efficient, and truly Pythonic code.

-----

### **1. Expressions vs. Statements: The Foundational Difference**

Before we dissect individual operators, it's crucial to understand the two core types of constructs in any programming language: **expressions** and **statements**. For the uncompromising programmer, this distinction isn't mere academic jargon; it dictates how code behaves and what you can do with it.

#### **What is an Expression? What Does It Return?**

At its heart, an **expression** in Python is a piece of code that, when evaluated by the interpreter, **produces (or returns) a value**. Think of it as a calculation or a question that yields an answer.

  * **Key Characteristic:** Every expression evaluates to a single, specific object (a value).
  * **Examples:**
      * `10` (evaluates to the integer object `10`)
      * `"hello"` (evaluates to the string object `"hello"`)
      * `5 + 3` (evaluates to the integer object `8`)
      * `len("Python")` (evaluates to the integer object `6`)
      * `x > 0` (evaluates to a boolean object `True` or `False`)
      * `my_list[0]` (evaluates to the object at index 0 of `my_list`)

You can use an expression wherever a value is expected. For example, the argument to a function call, the right-hand side of an assignment, or within a conditional check.

```python
# Simple expressions and their returned values
result_int = 10 * 2         # Expression `10 * 2` returns 20
print(result_int)           # 20

result_str = "Python" + "ic" # Expression `"Python" + "ic"` returns "Pythonic"
print(result_str)           # Pythonic

is_positive = -5 < 0        # Expression `-5 < 0` returns True
print(is_positive)          # True

# An expression as an argument to a function
print(max(10, 20, 5))       # The expression `max(10, 20, 5)` returns 20

# An expression as part of a larger expression
final_score = (80 + 90) / 2 # `(80 + 90)` is an expression, `/ 2` is an expression
print(final_score)          # 85.0
```

#### **What is a Statement?**

A **statement**, in contrast to an expression, is a unit of code that performs an **action** or executes a **command**. It does *not* necessarily evaluate to a value that can be assigned or used in another expression. Statements represent a complete instruction.

  * **Key Characteristic:** Executes an action; often doesn't "return" a value in the same sense an expression does (though some statements, like assignment, *do* have side effects and can sometimes be part of an expression as we'll see with the Walrus operator).
  * **Examples:**
      * `x = 10` (an assignment statement)
      * `print("Hello")` (a print statement, though `print` is a function call which *is* an expression, the whole line as an instruction is a statement)
      * `if condition: ...` (a conditional statement)
      * `for item in my_list: ...` (a loop statement)
      * `def my_function(): ...` (a function definition statement)
      * `import os` (an import statement)

<!-- end list -->

```python
# Examples of statements
x = 10                  # Assignment statement
print("Hello, world!")  # Function call (expression) wrapped in a statement
if x > 5:               # If statement
    print("x is greater than 5")
```

*The uncompromising programmer distinguishes expressions from statements. Expressions are about **producing values**; statements are about **performing actions**.* You cannot assign a statement to a variable (e.g., `y = if x > 0:` would be a syntax error).

#### **Python’s Expression-Oriented Design**

Python leans heavily towards an **expression-oriented design**. This means that many constructs that might be statements in other languages are expressions in Python, making the language more flexible and often leading to more concise code.

Key aspects of this design include:

  * Most operations (arithmetic, comparison, logical) result in a value.
  * Function calls are always expressions.
  * Even conditional logic can be an expression (the ternary operator `x if condition else y`).
  * List comprehensions, dictionary comprehensions, and generator expressions are powerful examples of combining expressions.

This design philosophy encourages functional programming patterns and allows for compact, readable code where results from one operation can seamlessly feed into the next.

#### **`eval()` and Its Dangers**

The `eval()` function in Python takes a string as an argument and attempts to **evaluate that string as a Python expression**. It then returns the result of that evaluation.

```python
code_string_1 = "2 * (10 + 5)"
result_1 = eval(code_string_1)
print(f"eval('{code_string_1}') = {result_1}") # Output: 30

code_string_2 = "len('Uncompromising')"
result_2 = eval(code_string_2)
print(f"eval('{code_string_2}') = {result_2}") # Output: 14
```

**The Uncompromising Warning: Dangers of `eval()`**

While `eval()` seems powerful, it is an incredibly dangerous function in most real-world applications.

  * **Security Risk:** `eval()` can execute *any* valid Python expression. If you use `eval()` on input received from an untrusted source (like user input on a web form, data from an external file, or a network request), you are essentially allowing that external source to execute arbitrary Python code on your system. This is a massive security vulnerability.
    ```python
    # NEVER do this with untrusted input!
    malicious_input = "__import__('os').system('rm -rf /')" # Example: delete all files
    # eval(malicious_input) # This line could cause severe damage if run!
    print("Pretending to run malicious code via eval()... (NOT ACTUALLY RUNNING)")
    ```
  * **Readability & Maintainability:** Code that relies heavily on `eval()` is typically harder to read, debug, and maintain because the logic is hidden within strings and only determined at runtime.

*The uncompromising programmer understands that `eval()` is almost always a sign of a design flaw when used with untrusted input. There are almost always safer, more explicit ways to achieve desired functionality (e.g., using configuration files, parsing specific commands, or dedicated libraries). Reserve `eval()` for very specific, controlled scenarios where the input source is guaranteed to be trusted and the expressions are well-defined.*

#### **Nesting Expressions**

A key aspect of writing powerful and concise Python code is the ability to **nest expressions**. This means using the result of one expression as an input or component of another, larger expression.

```python
# Simple nesting
total_cost = (item_price * quantity) + shipping_fee
# (item_price * quantity) is an expression
# Its result is used in the `+ shipping_fee` expression

# Nesting function calls
greeting = "Hello, " + input("Enter your name: ").strip().capitalize() + "!"
# `input()` is an expression that returns a string.
# `.strip()` is a method call (expression) on that string, returning a new string.
# `.capitalize()` is another method call (expression) on the result of .strip().
# The result of .capitalize() is then used in string concatenation.
print(greeting)

# Nesting comparisons within a larger expression
is_valid_range = (user_age >= 18) and (user_age <= 65)
# `user_age >= 18` is an expression returning a boolean.
# `user_age <= 65` is an expression returning a boolean.
# These boolean results are then combined by the `and` logical operator (another expression).
```

Nesting allows you to build complex logic from simpler parts, following Python's philosophy of readable and composable code. However, over-nesting can reduce readability, so use parentheses to clarify intent where needed.

### **2. Arithmetic Operators: The Foundation of Computation**

Arithmetic operators are the symbols used to perform mathematical calculations. While seemingly straightforward, an uncompromising programmer understands their nuances in Python, especially how they interact with different numerical types and handle edge cases.

#### **Basic Usage: The Core Operations**

Python provides standard arithmetic operators for common mathematical tasks:

| Operator | Operation       | Example          | Result |
| :------- | :-------------- | :--------------- | :----- |
| `+`      | Addition        | `10 + 3`         | `13`   |
| `-`      | Subtraction     | `10 - 3`         | `7`    |
| `*`      | Multiplication  | `10 * 3`         | `30`   |
| `/`      | Division        | `10 / 3`         | `3.333...` |
| `//`     | Floor Division  | `10 // 3`        | `3`    |
| `%`      | Modulus (Remainder) | `10 % 3`       | `1`    |
| `**`     | Exponentiation  | `2 ** 3`         | `8`    |

```python
# Basic Arithmetic Examples
print(f"10 + 3 = {10 + 3}")
print(f"10 - 3 = {10 - 3}")
print(f"10 * 3 = {10 * 3}")
print(f"2 ** 3 = {2 ** 3}") # 2 to the power of 3 (2*2*2)
print(f"9 ** 0.5 = {9 ** 0.5}") # Square root (3.0)

# Operations with floats
print(f"5.0 + 2.5 = {5.0 + 2.5}") # Result is float
print(f"7 * 1.5 = {7 * 1.5}")   # Result is float
```

#### **Differences Between `/` (True Division), `//` (Floor Division), and `%` (Modulus)**

These three operators are often confused but are distinct and powerful for integer arithmetic.

1.  **`/` (True Division):**

      * Always returns a `float` result, even if the numbers divide evenly.
      * This is a significant difference from many other languages (like C++ or Java) where integer division (`/`) truncates. Python's `/` provides "true" mathematical division.

    <!-- end list -->

    ```python
    print(f"10 / 3 = {10 / 3}")    # Output: 3.3333333333333335
    print(f"9 / 3 = {9 / 3}")      # Output: 3.0 (still a float!)
    print(f"-10 / 3 = {-10 / 3}")  # Output: -3.3333333333333335
    ```

2.  **`//` (Floor Division):**

      * Performs division and then "floors" the result, meaning it rounds down to the nearest whole number (integer).
      * The result type will be `int` if both operands are integers, and `float` if either operand is a float.
      * **Crucial for negative numbers:** Floor division always rounds *down* towards negative infinity.

    <!-- end list -->

    ```python
    print(f"10 // 3 = {10 // 3}")   # Output: 3 (3.33... rounded down)
    print(f"9 // 3 = {9 // 3}")     # Output: 3
    print(f"10 // 3.0 = {10 // 3.0}") # Output: 3.0 (result is float because of 3.0)
    print(f"-10 // 3 = {-10 // 3}") # Output: -4 (important! -3.33... rounded down to -4, not -3)
    print(f"-7 // 2 = {-7 // 2}")   # Output: -4 (-3.5 rounded down to -4)
    ```

3.  **`%` (Modulus - Remainder):**

      * Returns the remainder of the division.
      * The sign of the result matches the sign of the *divisor*.
      * The relationship `a = (a // b) * b + (a % b)` always holds true.

    <!-- end list -->

    ```python
    print(f"10 % 3 = {10 % 3}")    # Output: 1 (10 = 3*3 + 1)
    print(f"9 % 3 = {9 % 3}")      # Output: 0
    print(f"10 % -3 = {10 % -3}")  # Output: -2 (10 = -4 * -3 + (-2)) -> Sign of divisor (-3)
    print(f"-10 % 3 = {-10 % 3}")  # Output: 2 (-10 = -4 * 3 + 2) -> Sign of divisor (3)
    print(f"-7 % 2 = {-7 % 2}")    # Output: 1 (-7 = -4 * 2 + 1)
    ```

    *The uncompromising programmer understands the precise behavior of floor division and modulus with negative numbers, as this is a common source of bugs for those coming from other languages.*

#### **Float Quirks and the `decimal` Module Intro**

Floating-point numbers (`float` type) are represented in computers using a binary (base-2) system. This can lead to small, seemingly "quirky" inaccuracies when representing decimal (base-10) numbers that don't have an exact binary equivalent (similar to how $1/3$ cannot be perfectly represented in decimal).

```python
print(f"0.1 + 0.2 = {0.1 + 0.2}") # Output: 0.30000000000000004 (not exactly 0.3)
print(f"1.1 - 0.2 = {1.1 - 0.2}") # Output: 0.9000000000000001
```

These small errors are typically negligible for most scientific or graphical applications. However, for **financial calculations, exact decimal arithmetic, or critical precision requirements**, these quirks are unacceptable.

**The Uncompromising Solution: The `decimal` Module**

For scenarios demanding absolute decimal precision, Python provides the built-in `decimal` module. This module implements decimal floating-point arithmetic using base 10, avoiding the binary representation issues.

```python
from decimal import Decimal, getcontext

# Set precision for decimal calculations (default is usually 28)
getcontext().prec = 6 # Example: set to 6 decimal places

d1 = Decimal('0.1') # Always create Decimal objects from strings for exact representation
d2 = Decimal('0.2')
d3 = Decimal('0.3')

print(f"Decimal 0.1 + 0.2 = {d1 + d2}") # Output: 0.3
print(f"Decimal 1.1 - 0.2 = {Decimal('1.1') - Decimal('0.2')}") # Output: 0.9

# Comparison with Decimal is also exact
print(f"Decimal 0.1 + 0.2 == 0.3: {d1 + d2 == d3}") # Output: True (Exact!)

# Be aware of context precision
d4 = Decimal('1') / Decimal('3')
print(f"Decimal 1/3 (prec=6) = {d4}") # Output: 0.333333 (truncated to 6 places)

getcontext().prec = 28 # Reset to default or higher for more precision
d4 = Decimal('1') / Decimal('3')
print(f"Decimal 1/3 (prec=28) = {d4}") # Output: 0.3333333333333333333333333333
```

*The uncompromising programmer never uses standard `float` for financial calculations or any domain where exact decimal representation is paramount. They reach for the `decimal` module.*

#### **Edge Case Demos**

  * **Division by Zero:** All division operators (`/`, `//`, `%`) will raise a `ZeroDivisionError` if the divisor is zero. This is a crucial runtime error that must be handled.

    ```python
    try:
        result = 10 / 0
    except ZeroDivisionError as e:
        print(f"Error: {e}") # Output: Error: division by zero

    try:
        result = 10 // 0
    except ZeroDivisionError as e:
        print(f"Error: {e}") # Output: Error: integer division or modulo by zero
    ```

  * **Zero to the Power of Zero (`0**0`):** In mathematics, this is often undefined or context-dependent (sometimes 1). In Python, `0 ** 0` evaluates to `1`.

    ```python
    print(f"0 ** 0 = {0 ** 0}") # Output: 1
    ```

#### **`divmod()` and `round()` Functions**

Python provides built-in functions that often offer more convenient or precise ways to handle common arithmetic needs.

1.  **`divmod(a, b)`:**

      * Returns a tuple containing the quotient (`a // b`) and the remainder (`a % b`).
      * This is more efficient than calculating `//` and `%` separately if you need both.

    <!-- end list -->

    ```python
    quotient, remainder = divmod(17, 5)
    print(f"divmod(17, 5) -> Quotient: {quotient}, Remainder: {remainder}") # Output: Quotient: 3, Remainder: 2

    # Works with negative numbers respecting floor division rules
    q_neg, r_neg = divmod(-17, 5)
    print(f"divmod(-17, 5) -> Quotient: {q_neg}, Remainder: {r_neg}") # Output: Quotient: -4, Remainder: 3
    # Check: (-4 * 5) + 3 = -20 + 3 = -17 (correct)
    ```

2.  **`round(number, ndigits=None)`:**

      * Rounds `number` to `ndigits` decimal places.
      * If `ndigits` is omitted or `None`, it rounds to the nearest integer.
      * **Important Rounding Rule (Tie-breaking):** When a number is exactly halfway between two integers (e.g., `2.5`, `3.5`), Python's `round()` uses "round half to even" (also known as "banker's rounding"). This means it rounds to the nearest even integer. This helps mitigate bias when summing rounded numbers.

    <!-- end list -->

    ```python
    print(f"round(3.14159, 2) = {round(3.14159, 2)}") # Output: 3.14
    print(f"round(7.8) = {round(7.8)}")             # Output: 8
    print(f"round(7.3) = {round(7.3)}")             # Output: 7

    # Banker's Rounding examples:
    print(f"round(2.5) = {round(2.5)}")             # Output: 2 (rounds to the nearest even integer)
    print(f"round(3.5) = {round(3.5)}")             # Output: 4 (rounds to the nearest even integer)
    print(f"round(2.6) = {round(2.6)}")             # Output: 3
    print(f"round(2.4) = {round(2.4)}")             # Output: 2
    ```

    *The uncompromising programmer is aware of the "round half to even" rule for `round()` and will use the `decimal` module's `quantize` method with specific rounding modes (e.g., `ROUND_HALF_UP`) if different rounding behavior is strictly required.*


-----

### **3. Assignment Operators: Binding Names to Values**

Assignment is the most fundamental operation in Python: it's how you bind a name (a variable) to an object (a value) in memory. While the simple `=` operator is used for direct assignment, Python also provides a rich set of **compound assignment operators** and powerful shorthand for simultaneous assignments. An uncompromising programmer understands not just how to assign, but the profound implications of assignment on object references and mutability.

#### **Basic Assignment (`=`)**

The single equal sign is the basic assignment operator. It takes the object on its right-hand side and binds it to the variable name on its left-hand side.

```python
# Basic assignment
my_score = 100
player_name = "Alice"
is_game_over = False

print(f"my_score: {my_score}")
print(f"player_name: {player_name}")
print(f"is_game_over: {is_game_over}")
```

#### **Compound Assignment Operators (`+=`, `-=`, `*=`, etc.)**

Compound assignment operators combine an arithmetic (or bitwise) operation with assignment. They provide a concise shorthand for modifying a variable's value based on its current value.

| Operator | Equivalent to        | Example (Initial `x = 10`) | Result of `x` |
| :------- | :------------------- | :-------------------------- | :------------ |
| `+=`     | `x = x + value`      | `x += 5`                    | `15`          |
| `-=`     | `x = x - value`      | `x -= 3`                    | `7`           |
| `*=`     | `x = x * value`      | `x *= 2`                    | `20`          |
| `/=`     | `x = x / value`      | `x /= 4`                    | `2.5`         |
| `//=`    | `x = x // value`     | `x //= 3`                   | `3`           |
| `%=`     | `x = x % value`      | `x %= 3`                    | `1`           |
| `**=`    | `x = x ** value`     | `x **= 2`                   | `100`         |
| `&=`     | `x = x & value`      | `x &= 0b11` (for bitwise)   | `2` (if x=10) |
| `|=`     | `x = x | value`      | `x |= 0b1` (for bitwise)    | `11` (if x=10)|
| `^=`     | `x = x ^ value`      | `x ^= 0b10` (for bitwise)   | `8` (if x=10) |
| `<<=`    | `x = x << value`     | `x <<= 1` (for bitwise)     | `20` (if x=10)|
| `>>=`    | `x = x >> value`     | `x >>= 1` (for bitwise)     | `5` (if x=10) |

```python
score = 50
score += 10 # score = score + 10 -> 60
print(f"score after += 10: {score}")

price = 20.0
price *= 1.05 # price = price * 1.05 -> 21.0
print(f"price after *= 1.05: {price}")

progress = 17
progress %= 5 # progress = progress % 5 -> 2
print(f"progress after %= 5: {progress}")

# Example with string (concatenation)
message = "Hello"
message += " World!" # message = message + " World!" -> "Hello World!"
print(f"message after += ' World!': {message}")

# Example with list (extension)
my_numbers = [1, 2]
my_numbers += [3, 4] # my_numbers = my_numbers + [3, 4] -> [1, 2, 3, 4]
print(f"my_numbers after += [3, 4]: {my_numbers}")
```

#### **Difference Between Reassignment and In-Place Mutation with Compound Assignments**

This is a critical distinction for the uncompromising programmer, directly tied to the concepts of **mutability** and **object identity** from Chapter 3.

  * **Reassignment:** For **immutable** types (like `int`, `float`, `str`, `tuple`), compound assignment operators behave exactly like `x = x op value`. A *new object* is created for the result of the operation, and the variable name is then **rebound** to this new object. The original object, if no longer referenced, becomes eligible for garbage collection.

    ```python
    x = 10
    id_x_initial = id(x)
    print(f"x: {x}, id(x): {id_x_initial}")

    x += 5 # Equivalent to x = x + 5. A new int object 15 is created.
           # The name 'x' is rebound to this new object.
    id_x_after = id(x)
    print(f"x: {x}, id(x): {id_x_after}")
    print(f"Did x's ID change? {id_x_initial != id_x_after}") # Output: True (usually)
    ```

    (Note: For small integers, Python often "interns" them, meaning `id()` might unexpectedly stay the same for `x += 1`. This is an optimization. The conceptual model of a new object being created still holds, and for larger numbers or floats, the `id` *will* change.)

  * **In-Place Mutation:** For **mutable** types (like `list`, `dict`, `set`), compound assignment operators often (but not always\!) attempt to perform an **in-place modification** of the original object, if the type supports it. This means the object's `id()` typically remains the same, as its content is updated directly.

    ```python
    my_list = [1, 2, 3]
    id_list_initial = id(my_list)
    print(f"my_list: {my_list}, id(my_list): {id_list_initial}")

    my_list += [4, 5] # This typically calls my_list.extend([4, 5]), which modifies the list in-place.
    id_list_after = id(my_list)
    print(f"my_list: {my_list}, id(my_list): {id_list_after}")
    print(f"Did my_list's ID change? {id_list_initial != id_list_after}") # Output: False (most common case for lists)

    # Contrast with explicit reassignment for lists:
    another_list = [10, 20]
    id_another_initial = id(another_list)
    print(f"another_list: {another_list}, id(another_list): {id_another_initial}")
    another_list = another_list + [30, 40] # This explicitly creates a *new* list object.
    id_another_after = id(another_list)
    print(f"another_list: {another_list}, id(another_list): {id_another_after}")
    print(f"Did another_list's ID change? {id_another_initial != id_another_after}") # Output: True
    ```

    *The uncompromising programmer leverages compound assignments for mutable types when in-place modification is desired, as it's often more efficient (avoids creating a new object) and semantically clear.* Always be aware of whether the operation will rebind the name or mutate the object.

#### **Chaining Assignments: `a = b = c = 0`**

Python allows you to assign the same value to multiple variables in a single line using chained assignment. This is evaluated from right to left.

```python
x = y = z = 0
print(f"x: {x}, y: {y}, z: {z}") # Output: x: 0, y: 0, z: 0

# All three variables now reference the *same* integer object (0)
print(f"id(x): {id(x)}, id(y): {id(y)}, id(z): {id(z)}")
print(f"x is y: {x is y}, y is z: {y is z}") # Output: True, True
```

**Crucial Caveat for Chained Assignment with Mutable Objects:**

While chaining is fine for immutable objects, be extremely cautious when chaining assignments of **mutable objects**. All variables will point to the *exact same mutable object*. Modifying one through any of the variables will affect all of them.

```python
list1 = list2 = list3 = [1, 2, 3] # ALL refer to the same list object!

print(f"list1: {list1}, id(list1): {id(list1)}")
print(f"list2: {list2}, id(list2): {id(list2)}")

list1.append(4) # Modify the list via list1

print(f"list1 after append: {list1}") # Output: [1, 2, 3, 4]
print(f"list2 after append: {list2}") # Output: [1, 2, 3, 4] (SURPRISE! It changed too!)

print(f"list1 is list2: {list1 is list2}") # Output: True
```

*The uncompromising programmer avoids chaining assignment for mutable objects unless the explicit intention is to create aliases that share and modify the same underlying object.* If you need independent mutable objects, create them separately: `list1 = [1,2,3]; list2 = [1,2,3]`.

#### **Variable Value Swap: `a, b = b, a`**

Python offers an incredibly elegant and Pythonic way to swap the values of two variables without needing a temporary variable. This is achieved through **tuple packing and unpacking** in a single assignment statement.

```python
a = 10
b = 20

print(f"Before swap: a = {a}, b = {b}")

a, b = b, a # The magic swap!
            # 1. Right side: (b, a) creates a temporary tuple (20, 10).
            # 2. Left side: This tuple is unpacked into 'a' and 'b'.
            #    'a' gets 20, 'b' gets 10.

print(f"After swap: a = {a}, b = {b}") # Output: After swap: a = 20, b = 10
```

This pattern is widely used and highly readable. It relies on the right-hand side creating a tuple (implicitly or explicitly), which is then unpacked into the variables on the left-hand side.

*The uncompromising programmer leverages Python's expressive assignment features, like compound assignments for concise modifications and tuple unpacking for elegant swaps, always mindful of the underlying object model and mutability implications.*


-----

### **4. Comparison Operators: Making Decisions with Data**

Comparison operators, also known as relational operators, are fundamental for controlling program flow and making decisions. They allow you to compare two values and determine their relationship, always returning a Boolean result (`True` or `False`). For the uncompromising programmer, understanding their precise behavior, especially across different data types and in advanced scenarios like chaining, is non-negotiable.

#### **Basic Comparison Operators**

Python provides a standard set of comparison operators:

| Operator | Meaning                  | Example          | Result   |
| :------- | :----------------------- | :--------------- | :------- |
| `==`     | Equal to                 | `5 == 5`         | `True`   |
| `!=`     | Not equal to             | `5 != 10`        | `True`   |
| `>`      | Greater than             | `10 > 5`         | `True`   |
| `<`      | Less than                | `5 < 10`         | `True`   |
| `>=`     | Greater than or equal to | `10 >= 10`       | `True`   |
| `<=`     | Less than or equal to    | `5 <= 10`        | `True`   |

```python
# Numerical comparisons
print(f"5 == 5: {5 == 5}")       # True
print(f"5 != 10: {5 != 10}")     # True
print(f"10 > 5: {10 > 5}")       # True
print(f"5 < 10: {5 < 10}")       # True
print(f"10 >= 10: {10 >= 10}")   # True
print(f"5 <= 10: {5 <= 10}")     # True

# String comparisons (lexicographical/dictionary order)
# Case matters ('A' < 'a')
print(f"'apple' == 'apple': {'apple' == 'apple'}") # True
print(f"'apple' != 'orange': {'apple' != 'orange'}") # True
print(f"'apple' < 'orange': {'apple' < 'orange'}") # True (a comes before o)
print(f"'Banana' < 'apple': {'Banana' < 'apple'}") # True (B comes before a due to ASCII values)

# Mixed type comparisons (generally discouraged for ==/!= unless types have defined conversions)
# Python 3 generally prevents direct comparison of totally unrelated types with <, >, etc.
# print(5 < "hello") # TypeError: '<' not supported between instances of 'int' and 'str'
print(f"5 == 5.0: {5 == 5.0}") # True (Python performs implicit type promotion for comparison)
```

*The uncompromising programmer is precise with numerical comparisons and understands that string comparisons are based on lexicographical (dictionary) order, influenced by character encoding (e.g., ASCII or Unicode) values, meaning 'A' comes before 'a'. They also know that Python's strong typing prevents direct order comparisons between fundamentally unrelated types (like `int` and `str`), raising a `TypeError`.*

#### **Use with Custom Classes (`__eq__`, `__lt__`, etc.)**

By default, for custom objects (objects you create from your own `class` definitions, as briefly introduced in Chapter 3.6), the `==` operator checks for **identity** (like `is`) unless you explicitly define how your objects should be compared. Other comparison operators (`<`, `>`, etc.) will raise a `TypeError` by default.

To enable meaningful comparisons for your custom objects, you implement special "dunder" (double underscore) methods within your class definition. This process is called **operator overloading**, which we'll cover in more detail in Section 4.12.

Here's a preview for comparison operators:

  * `__eq__(self, other)`: Implements the `==` operator.
  * `__ne__(self, other)`: Implements the `!=` operator.
  * `__lt__(self, other)`: Implements the `<` operator.
  * `__le__(self, other)`: Implements the `<=` operator.
  * `__gt__(self, other)`: Implements the `>` operator.
  * `__ge__(self, other)`: Implements the `>=` operator.

<!-- end list -->

```python
# Let's use a simple class to demonstrate (will be fully explained in 4.12)
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    # Define how Point objects are compared for equality (==)
    def __eq__(self, other):
        if not isinstance(other, Point): # Ensure 'other' is also a Point object
            return NotImplemented # Or raise TypeError
        return self.x == other.x and self.y == other.y

    # Define how Point objects are compared for less than (<)
    def __lt__(self, other):
        if not isinstance(other, Point):
            return NotImplemented
        # Example: compare based on x-coordinate, then y if x's are equal
        return (self.x, self.y) < (other.x, other.y)

    def __repr__(self): # For better printing of the object
        return f"Point({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(1, 2)
p3 = Point(3, 4)
p4 = Point(1, 3)

print(f"p1 == p2: {p1 == p2}") # True (because __eq__ is implemented)
print(f"p1 == p3: {p1 == p3}") # False
print(f"p1 != p3: {p1 != p3}") # True

print(f"p1 < p3: {p1 < p3}")   # True (because __lt__ is implemented, (1,2) < (3,4))
print(f"p1 < p4: {p1 < p4}")   # True (because __lt__ is implemented, (1,2) < (1,3))
print(f"p4 < p1: {p4 < p1}")   # False

# Default behavior without __eq__ or __lt__
class SimpleObject:
    def __init__(self, value):
        self.value = value

s1 = SimpleObject(10)
s2 = SimpleObject(10)
print(f"s1 == s2 (without __eq__): {s1 == s2}") # False (default checks identity)
# print(f"s1 < s2 (without __lt__): {s1 < s2}") # TypeError (no __lt__ defined)
```

*The uncompromising programmer defines appropriate comparison methods for custom classes to ensure logical and predictable behavior for equality and ordering, reflecting the domain's rules.*

#### **Chaining Comparisons (`1 < x <= 10`)**

One of Python's most elegant features is the ability to **chain comparison operators**. This allows you to express multiple comparisons concisely, much like in mathematics.

The expression `a < b < c` is not evaluated as `(a < b) < c`. Instead, it is logically equivalent to `(a < b) and (b < c)`, but it's more efficient as `b` is evaluated only once.

```python
age = 25

# Chained comparison: (age > 18) and (age < 65)
is_working_age = 18 < age < 65
print(f"Is {age} working age (18 < age < 65)? {is_working_age}") # True

temperature = 0

# Chained comparison: (temperature >= -5) and (temperature <= 5)
is_freezing_ish = -5 <= temperature <= 5
print(f"Is {temperature} around freezing (-5 <= temp <= 5)? {is_freezing_ish}") # True

# An example where chaining might not be what you expect if misunderstood
x = 10
y = 5
z = 10

# Is x equal to y AND y equal to z? No, because y is 5, not 10.
# This evaluates as (x == y) and (y == z)
print(f"x == y == z: {x == y == z}") # False

# Example of a common pitfall:
a = False
b = 0
c = ""
# If you expect this to check if 'a' is equal to 'b' AND 'b' is equal to 'c'
# This works for these Falsy values
print(f"False == 0 == '': {False == 0 == ''}") # True (False==0 is True, 0=='' is False, True and False is False) - Wait!

# Let's break down False == 0 == ''
# 1. False == 0 --> True
# 2. 0 == '' --> False
# 3. True and False --> False
# So, the output will be False. My previous comment about "True" for this specific chain was incorrect for the last comparison.
# This actually highlights a good point of potential confusion in chaining == with different types that can implicitly convert for ==

# Let's clarify that specific example:
# False == 0 evaluates to True
# 0 == '' evaluates to False
# The chain False == 0 == '' is effectively (False == 0) and (0 == '')
# Which is (True) and (False) --> False.
# This correctly demonstrates that while Python allows chaining, you still need to understand the individual comparisons.
# In this specific case, 0 == '' is False because an integer 0 and an empty string "" are not considered equal by Python's ==.
# My prior comment was implicitly thinking of 'truthiness' which is for `bool()` or `if` conditions, not `==`.

# Re-demonstrating:
print(f"False == 0: {False == 0}") # True
print(f"0 == '': {0 == ''}")     # False
print(f"False == 0 == '': {False == 0 == ''}") # Effectively (False == 0) and (0 == '') which is (True and False) = False.
```

*The uncompromising programmer harnesses chained comparisons for concise, mathematical expressions, but always validates their understanding of how individual comparisons resolve, especially when different types are involved, to avoid subtle bugs.*

-----
