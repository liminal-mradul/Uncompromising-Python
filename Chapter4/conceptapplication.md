
## **Operator Mastery: A Full-Proof Exercise Set**

**Instructions:** For each question, try to determine the exact output or value without running the code. Then, compare your answer with the provided solution and explanation. Pay close attention to the "Why" section, especially for the harder questions.

-----

### **Level 1: Easy (Fundamental Concepts)**

**Q1. Arithmetic Basics:**
What is the value of `result`?

```python
result = 15 // 4 + 7 % 3
```

**Q2. Comparison:**
What is the value of `is_equal`?

```python
is_equal = (5 * 2 == 10) and (12 - 3 != 8)
```

**Q3. Logical OR:**
What is the value of `status`?

```python
is_logged_in = False
has_items_in_cart = True
status = is_logged_in or has_items_in_cart
```

**Q4. String Concatenation:**
What is the value of `full_message`?

```python
part1 = "Hello"
part2 = "World"
full_message = part1 + " " + part2 + "!"
```

**Q5. Bitwise AND:**
What is the value of `mask_check`? (Think in binary or use `bin()` conceptually)

```python
permissions = 0b1011  # Read, Write, Execute (on, off, on, on)
READ_MASK = 0b0001
mask_check = permissions & READ_MASK
```

-----

### **Level 2: Moderate (Combining Concepts, Basic Nuances)**

**Q6. Precedence with Arithmetic:**
What is the value of `final_value`?

```python
final_value = 2 * 3 ** 2 - 10 / 5
```

**Q7. Truthiness and Logical `and`:**
What is the value of `outcome`?

```python
name = ""
age = 25
outcome = name and age
```

**Q8. Identity vs. Equality (Small Integers):**
What are the values of `check1` and `check2`?

```python
x = 200
y = 200
check1 = (x == y)
check2 = (x is y)
```

**Q9. Membership and Strings:**
What is the value of `found_substring`?

```python
sentence = "Python programming is fun."
found_substring = "gram" in sentence and "java" not in sentence
```

**Q10. Bitwise OR for Setting Flags:**
What is the decimal value of `combined_flags`?

```python
FLAG_A = 0b001
FLAG_B = 0b010
FLAG_C = 0b100
current_flags = FLAG_A | FLAG_C
new_flag = FLAG_B
combined_flags = current_flags | new_flag
```

-----

### **Level 3: Hard (Deep Understanding, Common Pitfalls)**

**Q11. Bitwise NOT and Two's Complement:**
What is the value of `result`?

```python
val = 7
result = ~val
```

**Q12. Augmented Assignment and Mutability:**
What are the final values of `list1` and `list_ref`?

```python
list1 = [1, 2]
list_ref = list1
list1 = list1 + [3]
```

**Q13. Logical Operator Precedence:**
What is the value of `can_access`?

```python
is_admin = False
has_license = True
is_guest = False
can_access = is_admin and has_license or is_guest
```

**Q14. Right Shift with Negative Numbers:**
What is the value of `shifted_neg`?

```python
shifted_neg = -100 >> 2
```

**Q15. Ternary Operator and Function Calls:**
What will be printed?

```python
def check_status(value):
    print(f"Checking {value}")
    return value % 2 == 0

message = "Even" if check_status(4) else "Odd"
print(message)
```

-----

### **Level 4: Uncompromising (Internal Mechanisms, Edge Cases, Design)**

**Q16. `is` vs `==` with Custom Objects (Operator Overloading):**
What are the values of `comp1` and `comp2`?

```python
class MyValue:
    def __init__(self, val):
        self.val = val
    def __eq__(self, other):
        if isinstance(other, MyValue):
            return self.val == other.val
        return NotImplemented

v1 = MyValue(10)
v2 = MyValue(10)
v3 = v1

comp1 = (v1 == v2)
comp2 = (v1 is v3)
```

**Q17. Assignment Expression (`:=`) in a Loop:**
What are the final contents of `processed_lines`?

```python
def get_input_stream():
    yield "line 1"
    yield "line 2"
    yield "END"
    yield "line 3 (should not be processed)"

lines_stream = get_input_stream()
processed_lines = []
while (line := next(lines_stream)) != "END":
    processed_lines.append(line.upper())
```

**Q18. Operator Overloading Design Choice:**
Given a `ComplexNumber` class, discuss whether `*` (multiplication) should be overloaded for both complex-complex multiplication and complex-scalar multiplication. If so, how would you handle the types?

**Q19. Expression Evaluation Order with Side Effects:**
What will be the exact print output and the final value of `result`?

```python
def func1():
    print("Func1 called")
    return True

def func2():
    print("Func2 called")
    return False

def func3():
    print("Func3 called")
    return 10

result = func1() and func2() or func3()
```

**Q20. Bitwise Masking for Toggling a Specific Bit:**
You have a `settings` integer. How would you write a single expression (using bitwise operators) to **toggle** the 3rd bit (0-indexed, so 2^3) without affecting any other bits? Provide the expression and its binary explanation for `settings = 0b10110101`.

-----

-----

### **Answers and Detailed Explanations**

-----

### **Level 1: Easy - Answers**

**A1. Arithmetic Basics:**
`result = 15 // 4 + 7 % 3`

  * `15 // 4` (floor division): `3` (15 divided by 4 is 3 with remainder 3, floor division rounds down)
  * `7 % 3` (modulus): `1` (7 divided by 3 is 2 with remainder 1)
  * `3 + 1` = `4`
    **Answer:** `result = 4`

**A2. Comparison:**
`is_equal = (5 * 2 == 10) and (12 - 3 != 8)`

  * `5 * 2 == 10`: `10 == 10` is `True`
  * `12 - 3 != 8`: `9 != 8` is `True`
  * `True and True` is `True`
    **Answer:** `is_equal = True`

**A3. Logical OR:**
`is_logged_in = False`
`has_items_in_cart = True`
`status = is_logged_in or has_items_in_cart`

  * `False or True`: The `or` operator returns the first truthy value.
    **Answer:** `status = True`

**A4. String Concatenation:**
`part1 = "Hello"`
`part2 = "World"`
`full_message = part1 + " " + part2 + "!"`

  * `"Hello" + " "`: `"Hello "`
  * `"Hello " + "World"`: `"Hello World"`
  * `"Hello World" + "!"`: `"Hello World!"`
    **Answer:** `full_message = "Hello World!"`

**A5. Bitwise AND:**
`permissions = 0b1011`
`READ_MASK = 0b0001`
`mask_check = permissions & READ_MASK`

  * Binary:
    ```
      1011 (permissions)
    & 0001 (READ_MASK)
    ------
      0001 (mask_check)
    ```
  * `0b0001` in decimal is `1`.
    **Answer:** `mask_check = 1`

-----

### **Level 2: Moderate - Answers**

**A6. Precedence with Arithmetic:**
`final_value = 2 * 3 ** 2 - 10 / 5`

  * **1. `**` (Exponentiation):** `3 ** 2` is `9`.
  * **2. `*` (Multiplication) and `/` (Division):** These have equal precedence and are left-associative.
      * `2 * 9` is `18`.
      * `10 / 5` is `2.0` (float division).
  * **3. `-` (Subtraction):**
      * `18 - 2.0` is `16.0`.
        **Answer:** `final_value = 16.0`

**A7. Truthiness and Logical `and`:**
`name = ""` (empty string is falsy)
`age = 25` (non-zero number is truthy)
`outcome = name and age`

  * `name` is falsy. The `and` operator short-circuits and returns the first falsy operand.
    **Answer:** `outcome = ""`

**A8. Identity vs. Equality (Small Integers):**
`x = 200`
`y = 200`
`check1 = (x == y)`
`check2 = (x is y)`

  * `x == y`: `200 == 200` is `True` (values are equal).
  * `x is y`: Python *does not* guarantee that integers outside the range of -5 to 256 will be interned (i.e., refer to the same object). For `200`, it's highly likely Python creates two distinct objects.
    **Answer:** `check1 = True`, `check2 = False` (This can vary based on Python interpreter version and runtime conditions, but `False` is the standard expectation for numbers outside the small int range).

**A9. Membership and Strings:**
`sentence = "Python programming is fun."`
`found_substring = "gram" in sentence and "java" not in sentence`

  * `"gram" in sentence`: `True` (because "programming" contains "gram").
  * `"java" not in sentence`: `True` (because "java" is indeed not in the sentence).
  * `True and True` is `True`.
    **Answer:** `found_substring = True`

**A10. Bitwise OR for Setting Flags:**
`FLAG_A = 0b001` (1)
`FLAG_B = 0b010` (2)
`FLAG_C = 0b100` (4)
`current_flags = FLAG_A | FLAG_C`
`new_flag = FLAG_B`
`combined_flags = current_flags | new_flag`

  * `current_flags`:
    ```
      001 (FLAG_A)
    | 100 (FLAG_C)
    ------
      101 (current_flags)
    ```
  * `combined_flags`:
    ```
      101 (current_flags)
    | 010 (FLAG_B)
    ------
      111 (combined_flags)
    ```
  * `0b111` in decimal is `7`.
    **Answer:** `combined_flags = 7`

-----

### **Level 3: Hard - Answers**

**A11. Bitwise NOT and Two's Complement:**
`val = 7`
`result = ~val`

  * Recall the rule: `~x` is equivalent to `-(x + 1)`.
  * So, `~7` is `-(7 + 1)` which is `-8`.
  * Binary explanation (conceptual 8-bit, Python is arbitrary precision):
      * `7` in binary is `0000 0111`.
      * Applying bitwise NOT (`~`) flips all bits: `1111 1000`.
      * In two's complement, `1111 1000` represents `-8`. (To verify: invert `1111 1000` -\> `0000 0111`. Add 1 -\> `0000 1000`, which is 8. So the original was `-8`).
        **Answer:** `result = -8`

**A12. Augmented Assignment and Mutability:**
`list1 = [1, 2]`
`list_ref = list1` (Both `list1` and `list_ref` point to the same list object in memory)
`list1 = list1 + [3]`

  * `list1 = list1 + [3]`: This operation `list1 + [3]` creates a **new list object** `[1, 2, 3]`. The variable `list1` is then **reassigned** to point to this *new* list.
  * `list_ref` still points to the *original* list object `[1, 2]`.
    **Answer:**
    `list1 = [1, 2, 3]`
    `list_ref = [1, 2]`

**A13. Logical Operator Precedence:**
`is_admin = False`
`has_license = True`
`is_guest = False`
`can_access = is_admin and has_license or is_guest`

  * **1. `and` has higher precedence:** `is_admin and has_license`
      * `False and True` evaluates to `False` (due to short-circuiting, returns `False`).
  * **2. `or` has lower precedence:** The expression becomes `False or is_guest`
      * `False or False` evaluates to `False` (due to short-circuiting, returns `False`).
        **Answer:** `can_access = False`

**A14. Right Shift with Negative Numbers:**
`shifted_neg = -100 >> 2`

  * Python uses **arithmetic right shift** for signed integers, meaning the sign bit is extended. This preserves the sign and is equivalent to floor division `x // (2**n)`.
  * `-100 // (2**2)` is `-100 // 4`.
  * Floor division rounds down towards negative infinity.
  * `-100 / 4 = -25`.
    **Answer:** `shifted_neg = -25`

**A15. Ternary Operator and Function Calls:**

```python
def check_status(value):
    print(f"Checking {value}")
    return value % 2 == 0

message = "Even" if check_status(4) else "Odd"
print(message)
```

  * The `condition` part of the ternary operator (`check_status(4)`) is evaluated first.
  * `check_status(4)` will execute: `print("Checking 4")`.
  * `4 % 2 == 0` is `True`.
  * Since the condition is `True`, `"Even"` is chosen and assigned to `message`.
  * Finally, `print(message)` prints "Even".
    **Answer (Exact Output):**

<!-- end list -->

```
Checking 4
Even
```

-----

### **Level 4: Uncompromising - Answers**

**A16. `is` vs `==` with Custom Objects (Operator Overloading):**

```python
class MyValue:
    def __init__(self, val):
        self.val = val
    def __eq__(self, other):
        if isinstance(other, MyValue):
            return self.val == other.val
        return NotImplemented

v1 = MyValue(10)
v2 = MyValue(10)
v3 = v1

comp1 = (v1 == v2)
comp2 = (v1 is v3)
```

  * `comp1 = (v1 == v2)`:
      * This calls `v1.__eq__(v2)`.
      * `isinstance(v2, MyValue)` is `True`.
      * `self.val == other.val` becomes `10 == 10`, which is `True`.
  * `comp2 = (v1 is v3)`:
      * `v3 = v1` makes `v3` a reference to the *exact same object* in memory that `v1` points to.
      * `is` checks for object identity.
        **Answer:** `comp1 = True`, `comp2 = True`

**A17. Assignment Expression (`:=`) in a Loop:**

```python
def get_input_stream():
    yield "line 1"
    yield "line 2"
    yield "END"
    yield "line 3 (should not be processed)"

lines_stream = get_input_stream()
processed_lines = []
while (line := next(lines_stream)) != "END":
    processed_lines.append(line.upper())
```

  * The `while` loop condition uses `:=` to assign the result of `next(lines_stream)` to `line` *and* then uses that `line` for comparison.
  * **Iteration 1:** `line` gets `"line 1"`. `"line 1"` is not `"END"`. `processed_lines.append("LINE 1")`.
  * **Iteration 2:** `line` gets `"line 2"`. `"line 2"` is not `"END"`. `processed_lines.append("LINE 2")`.
  * **Iteration 3:** `line` gets `"END"`. `"END"` *is* `"END"`. The loop condition `("END" != "END")` evaluates to `False`.
  * The loop terminates *before* the body executes again. `"line 3"` is yielded but never processed because the loop exits.
    **Answer:** `processed_lines = ['LINE 1', 'LINE 2']`

**A18. Operator Overloading Design Choice:**
Given a `ComplexNumber` class, discuss whether `*` (multiplication) should be overloaded for both complex-complex multiplication and complex-scalar multiplication. If so, how would you handle the types?

**Discussion:**
Yes, it is generally **highly recommended and intuitive** to overload the `*` operator for both complex-complex and complex-scalar multiplication for a `ComplexNumber` class.

**Why?**

1.  **Intuitive Analogy:** In mathematics, both complex number multiplication (complex \* complex) and scalar multiplication (complex \* real) are standard operations using the `*` symbol. Python's built-in `complex` type already supports this.
2.  **Readability:** `c1 * c2` and `c1 * 5` are far more readable than `c1.multiply(c2)` or `c1.scalar_multiply(5)`.
3.  **Consistency:** It allows `ComplexNumber` objects to behave more like native numeric types.

**How to handle the types (`__mul__` and `__rmul__`):**

```python
class ComplexNumber:
    def __init__(self, real, imag):
        self.real = real
        self.imag = imag

    def __repr__(self):
        return f"({self.real}{'+' if self.imag >= 0 else ''}{self.imag}j)"

    def __add__(self, other):
        if isinstance(other, ComplexNumber):
            return ComplexNumber(self.real + other.real, self.imag + other.imag)
        if isinstance(other, (int, float)): # Scalar addition
            return ComplexNumber(self.real + other, self.imag)
        return NotImplemented

    # Overloading Multiplication `c1 * c2` or `c1 * scalar`
    def __mul__(self, other):
        # Case 1: ComplexNumber * ComplexNumber
        if isinstance(other, ComplexNumber):
            new_real = self.real * other.real - self.imag * other.imag
            new_imag = self.real * other.imag + self.imag * other.real
            return ComplexNumber(new_real, new_imag)
        # Case 2: ComplexNumber * Scalar (int or float)
        elif isinstance(other, (int, float)):
            return ComplexNumber(self.real * other, self.imag * other)
        
        # If unsupported type, return NotImplemented to allow __rmul__ to be tried
        return NotImplemented

    # Overloading Reverse Multiplication `scalar * c1`
    # This is called if `scalar.__mul__(c1)` returns NotImplemented or is not defined.
    def __rmul__(self, other):
        # Scalar * ComplexNumber
        if isinstance(other, (int, float)):
            return ComplexNumber(self.real * other, self.imag * other)
        # If still unsupported, return NotImplemented
        return NotImplemented

# Demonstration:
c1 = ComplexNumber(2, 3) # 2 + 3j
c2 = ComplexNumber(1, 4) # 1 + 4j

print(f"c1 * c2: {c1 * c2}") # Expected: (2*1 - 3*4) + (2*4 + 3*1)j = (2-12) + (8+3)j = -10 + 11j
print(f"c1 * 5: {c1 * 5}")   # Expected: 10 + 15j
print(f"5 * c1: {5 * c1}")   # Expected: 10 + 15j (thanks to __rmul__)

try:
    c1 * "text"
except TypeError as e:
    print(f"Error: {e}") # Should raise TypeError: unsupported operand type(s) for *: 'ComplexNumber' and 'str'
```

**Conclusion:** It's a good design choice. The `__mul__` method handles the `ComplexNumber * X` case (where X can be `ComplexNumber` or scalar), and `__rmul__` handles `X * ComplexNumber` where X is a scalar. Using `isinstance()` for type checking and returning `NotImplemented` for unhandled types ensures proper behavior and error handling.

**A19. Expression Evaluation Order with Side Effects:**

```python
def func1():
    print("Func1 called")
    return True

def func2():
    print("Func2 called")
    return False

def func3():
    print("Func3 called")
    return 10

result = func1() and func2() or func3()
```

  * **1. `func1() and func2()`:**
      * `func1()` is called first: prints "Func1 called", returns `True`.
      * Since `func1()` returned `True` (truthy), `func2()` is then called (because `and` needs to evaluate the second operand if the first is truthy).
      * `func2()` executes: prints "Func2 called", returns `False`.
      * The result of `True and False` is `False`.
  * **2. `False or func3()`:**
      * The first operand `False` is falsy, so `func3()` is called (due to `or` needing to evaluate the second operand if the first is falsy).
      * `func3()` executes: prints "Func3 called", returns `10`.
      * The result of `False or 10` is `10` (as `or` returns the first truthy value it encounters).

**Answer (Exact Output):**

```
Func1 called
Func2 called
Func3 called
```

**Answer (Value of `result`):** `result = 10`

**A20. Bitwise Masking for Toggling a Specific Bit:**
You have a `settings` integer. How would you write a single expression (using bitwise operators) to **toggle** the 3rd bit (0-indexed, so 2^3) without affecting any other bits? Provide the expression and its binary explanation for `settings = 0b10110101`.

**Understanding the Goal:**

  * To toggle a bit, we use the XOR operator (`^`).
  * A bit `X` XORed with `1` flips `X` (`0^1=1`, `1^1=0`).
  * A bit `X` XORed with `0` leaves `X` unchanged (`0^0=0`, `1^0=1`).
  * So, we need a mask that has `1` at the 3rd bit position and `0` everywhere else.

**Creating the Mask:**

  * The 3rd bit (0-indexed) corresponds to $2^3 = 8$.
  * In binary, this mask is `0b00001000`.

**The Expression:**
`settings ^ (1 << 3)`
Or more simply, `settings ^ 8` (if you already know the decimal value of the bit mask).

**Binary Explanation for `settings = 0b10110101`:**

  * `settings`: `1011 0101`
  * Mask `(1 << 3)` or `8`: `0000 1000`

Performing XOR:

```
  1011 0101 (settings)
^ 0000 1000 (mask)
------------
  1011 1101 (result)
```

  * The original 3rd bit in `settings` was `0`. After XORing with `1` from the mask, it becomes `1`.
  * All other bits were XORed with `0` from the mask, so they remain unchanged.

**Answer:**
**Expression:** `settings ^ (1 << 3)` (or `settings ^ 8`)

**Binary Explanation:**
`settings = 0b10110101` (decimal 181)
The 3rd bit (0-indexed) is the 4th bit from the right: `...X_3_X_2_X_1_X_0`
In `0b10110101`, the 3rd bit is `0`.

The mask for the 3rd bit is `0b00001000` (which is `1 << 3` or `8` in decimal).

Performing the XOR operation:

```
  1011 0101 (Original settings)
^ 0000 1000 (Toggle mask)
------------
  1011 1101 (Resulting settings)
```

The 3rd bit (from the right) has successfully been toggled from `0` to `1`. All other bits remain `10110` and `101` as they were.
The new decimal value is `0b10111101` which is `128 + 32 + 16 + 8 + 4 + 1 = 189`.

-----
