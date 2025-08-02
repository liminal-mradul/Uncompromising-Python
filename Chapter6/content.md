# Chapter 6: Loops and Iteration Mastery
> *"Repetition with intention. Iterate like an artisan, not a robot."*
------
### 6.1 What is Iteration?

At its core, **iteration** is the process of repeating a sequence of instructions for a specified number of times or until a certain condition is met. It is one of the most fundamental concepts in computer programming, enabling programs to perform tasks efficiently that would be tedious or impossible to do manually. Iteration is the engine of automation, allowing code to process large datasets, handle user input, and simulate complex systems with a simple, repeatable set of commands.

#### Real-World Analogies of Loops

To understand iteration, consider its presence in everyday life:

* **A Wheel:** The spokes of a wheel are a perfect analogy for a loop. As the wheel turns, each spoke follows the same path, one after another, completing a full rotation. This repetition of a single action (moving along a circular path) is a continuous process until the wheel stops.
* **A Daily Routine:** Your morning routine is a form of iteration. You might repeat the same sequence of actions—wake up, brush teeth, make coffee, get dressed—every day. Each day is one cycle, or one iteration, of the routine. The routine repeats until a condition is met, such as the weekend arriving.
* **A Recipe:** Baking a dozen cookies involves a looping pattern. The recipe might contain a step that says, "Repeat for each cookie dough ball." This single instruction encapsulates the repetition of forming a cookie, placing it on a tray, and so on, for a definite number of times (12 iterations).

#### Types of Iteration: Definite vs. Indefinite

In programming, iteration is broadly categorized into two types, which directly correspond to the two primary types of loops in Python:

* **Definite Iteration:** This occurs when the number of repetitions is known in advance. The loop is set to execute a specific number of times. This is analogous to the cookie recipe: you know you need to make exactly 12 cookies. In Python, the **`for` loop** is the primary tool for definite iteration. It is used to iterate over a finite sequence of elements, such as a list of names or the characters in a string.

* **Indefinite Iteration:** This occurs when the number of repetitions is not known ahead of time. The loop continues to run as long as a certain condition remains true. This is like waiting for a bus: you don't know exactly how many minutes it will take, so you continue waiting until the condition "the bus has arrived" is met. In Python, the **`while` loop** is used for indefinite iteration. It is ideal for scenarios like reading user input, where the program waits for a specific command, or for retrying a network connection until it succeeds.

#### Looping as a Form of Automation

The true power of iteration lies in its ability to automate repetitive tasks. Without loops, processing a list of one million items would require writing one million separate lines of code. Loops abstract this repetition, allowing a single block of code to handle an entire dataset, regardless of its size. This not only makes programs more concise and manageable but also unlocks the ability to perform complex operations on a massive scale, from generating reports to simulating weather patterns.

### 6.2 The `for` Loop

The `for` loop is the workhorse of definite iteration in Python. It is designed to iterate over the elements of a sequence or any other iterable object, executing a block of code once for each item. Its clear, concise syntax makes it the most common and idiomatic choice for repetition where the number of iterations is known or can be determined from the data itself.

#### Syntax and Flowchart

The basic syntax of a `for` loop is straightforward:

```python
for variable in iterable:
    # Code block to be executed
    # This block runs once for each item in 'iterable'
```

  - `for` and `in` are Python keywords.
  - `variable` is a temporary variable that holds the current item from the iterable in each pass of the loop.
  - `iterable` is any object that can be iterated over (e.g., lists, strings, tuples, dictionaries, sets).

The conceptual flowchart for a `for` loop is as follows:

1.  Check if there are more items in the `iterable`.
2.  If **yes**, assign the next item to the `variable`.
3.  Execute the code block inside the loop.
4.  Return to step 1.
5.  If **no**, exit the loop and continue with the rest of the program.

#### Iterating Over Sequences

The `for` loop can iterate over a wide variety of iterable objects:

  * **List:**
    ```python
    fruits = ["apple", "banana", "cherry"]
    for fruit in fruits:
        print(fruit)
    ```
  * **String:** Iterates over each character.
    ```python
    for char in "Python":
        print(char)
    ```
  * **Tuple:**
    ```python
    coordinates = (10, 20)
    for coord in coordinates:
        print(coord)
    ```
  * **Set:** Iterates over each unique element in an arbitrary order.
    ```python
    unique_ids = {101, 102, 103}
    for uid in unique_ids:
        print(uid)
    ```

#### Practical Examples

  * **Email Parsing:** A common task is to process a list of email addresses. A `for` loop allows you to apply the same logic (e.g., printing the domain) to each one.

    ```python
    emails = ["alice@example.com", "bob@example.org", "charlie@example.com"]
    for email in emails:
        username, domain = email.split('@')
        print(f"Domain: {domain}")
    ```

  * **File Line-by-Line Reading:** A `for` loop is the most direct and efficient way to read and process a file line by line. Python's file objects are themselves iterables.

    ```python
    # Assuming a file named 'data.txt' exists
    # file_object is an iterable that yields one line at a time
    with open('data.txt', 'r') as file_object:
        for line in file_object:
            print(line.strip()) # .strip() removes leading/trailing whitespace and newlines
    ```

#### Iterating Over Dictionaries

Dictionaries can be iterated over in several ways, each providing access to a different part of the key-value structure.

  * **Iterating over keys (default behavior):**

    ```python
    person = {"name": "Alice", "age": 30, "city": "New York"}
    for key in person:
        print(key) # Prints: name, age, city
    ```

  * **Iterating over values:**

    ```python
    for value in person.values():
        print(value) # Prints: Alice, 30, New York
    ```

  * **Iterating over key-value pairs (items):** This is the most common pattern for dictionaries.

    ```python
    for key, value in person.items():
        print(f"{key}: {value}")
    ```

-----



### 📦 **Bonus Box: "Behind the `for` loop: How Python uses iterators under the hood."**

The magic of the `for` loop lies in Python's **iterator protocol**. When a `for` loop starts, it doesn't simply grab all the data at once. Instead, it follows a specific, two-step process to fetch items one by one. This mechanism makes `for` loops both versatile and memory-efficient.

### The Iterator Protocol in Action: `iter()`, `next()`, and `StopIteration`

Here are explicit code examples demonstrating how Python's iterator protocol works, which is the underlying mechanism for all `for` loops.

#### 1\. The `iter()` Function

The `iter()` function takes an iterable object (like a list, tuple, or string) and returns a corresponding **iterator object**. The iterator is what keeps track of your position in the sequence.

```python
# A simple list, which is an iterable
my_list = ['apple', 'banana', 'cherry']

# iter() returns an iterator object for the list
list_iterator = iter(my_list)

print("The original list is:", my_list)
print("The type of the iterator is:", type(list_iterator))

# Output:
# The original list is: ['apple', 'banana', 'cherry']
# The type of the iterator is: <class 'list_iterator'>
```

Notice that `list_iterator` is a different type of object from `my_list`.

#### 2\. The `next()` Function

The `next()` function takes an iterator object and returns the next item in the sequence. Each call to `next()` advances the iterator's position.

```python
my_tuple = ('red', 'green', 'blue')
tuple_iterator = iter(my_tuple)

# First call to next() gets the first item
item_1 = next(tuple_iterator)
print("First item:", item_1)  # Output: First item: red

# Second call to next() gets the second item
item_2 = next(tuple_iterator)
print("Second item:", item_2) # Output: Second item: green

# Third call to next() gets the last item
item_3 = next(tuple_iterator)
print("Third item:", item_3)  # Output: Third item: blue
```

At this point, the `tuple_iterator` has been exhausted. It has no more items to give.

#### 3\. The `StopIteration` Exception

When `next()` is called on an iterator that has no more items, it raises a `StopIteration` exception. A `for` loop handles this exception silently to know when to stop. You can handle it explicitly with a `try...except` block.

```python
my_string = "Hello"
string_iterator = iter(my_string)

# We can loop through the items with next()
print(next(string_iterator)) # Output: H
print(next(string_iterator)) # Output: e
# ... and so on

# After the last item is returned, the next call to next() will raise an exception.
try:
    # This will work for the remaining items in the string
    for _ in range(3):
        print(next(string_iterator))
    
    # This call will raise the StopIteration exception
    print(next(string_iterator)) 
except StopIteration:
    print("The iterator is now empty. The loop has ended.")
# Output:
# l
# l
# o
# The iterator is now empty. The loop has ended.
```

### All Together: Simulating a `for` Loop

Here is a complete example that manually simulates exactly what Python's `for` loop does automatically, combining `iter()`, `next()`, and `StopIteration`.

```python
my_list = ['A', 'B', 'C']

# Step 1: Get an iterator
manual_iterator = iter(my_list)

# Step 2: Set up a loop to repeatedly call next()
while True:
    try:
        # Step 3: Call next() and process the item
        current_item = next(manual_iterator)
        print("Processing item:", current_item)
    except StopIteration:
        # Step 4: Catch the StopIteration exception and break the loop
        print("Done processing all items.")
        break

# This manual loop produces the same result as:
# for current_item in my_list:
#     print("Processing item:", current_item)
```
### 6.3 The `while` Loop

The `while` loop is Python's primary tool for **indefinite iteration**. It is a powerful but demanding tool, as its execution depends entirely on a condition that must eventually become `False`. This makes it the ideal choice for scenarios where the number of repetitions is not known ahead of time.

#### Syntax and When to Prefer It

The syntax for a `while` loop is declarative:

```python
while condition:
    # Code block to be executed repeatedly
    # This block continues as long as 'condition' is True
```

  - The `condition` is a Boolean expression evaluated at the start of each iteration.
  - The loop's body **must** contain code that eventually changes the state of the `condition` to `False`.

You should prefer a `while` loop over a `for` loop when:

  * The number of iterations is not known in advance (e.g., waiting for user input, retrying a connection).
  * The termination condition is based on a complex state change, not a simple traversal of a sequence.
  * The loop is designed to run forever, waiting for events (often using `while True`).

#### Sentinel-Controlled Iteration

A classic application of the `while` loop is **sentinel-controlled iteration**. A *sentinel* is a special value that serves as a signal to terminate the loop.

**Example: Processing Data from a File with a Sentinel**
Imagine a data file where a blank line or a specific keyword like `"END"` marks the end of the records.

```python
data_stream = ["item1", "item2", "END", "item3"] # Simulate a data source
index = 0
current_item = data_stream[index]

# The loop continues as long as the current item is not the sentinel
while current_item != "END":
    print(f"Processing: {current_item}")
    index += 1
    current_item = data_stream[index]

print("End of data reached.")
```

The string `"END"` is the sentinel value that controls the loop's termination. This pattern is robust even if the number of items before the sentinel changes.

#### The `while True` Idiom for Event Loops

A very common and powerful pattern is to create an infinite loop using `while True` and use a `break` statement to exit cleanly based on a condition within the loop's body. This is often called an **event loop** or a **main loop**.

**Example: A Simple Command-Line Interface**

```python
while True:
    command = input("Enter a command (or 'exit'): ")
    if command == "exit":
        print("Exiting application.")
        break  # Exit the infinite loop
    elif command == "help":
        print("Available commands: help, exit")
    else:
        print(f"Command '{command}' not recognized.")
```

This pattern is fundamental to applications that constantly wait for user input, network packets, or other events.

#### Simulating Conditions: "Retry Until Success" with Exponential Backoff

This advanced pattern uses a `while` loop to repeatedly attempt a task that might fail, but it introduces a delay that grows with each failure. This is known as **exponential backoff** and is a best practice for network operations.

```python
import time

max_retries = 5
retries = 0
delay = 1  # Initial delay in seconds
connection_successful = False

while not connection_successful and retries < max_retries:
    print(f"Attempting to connect... (Retry {retries + 1}/{max_retries})")
    
    # --- Simulate a task that might fail ---
    if retries < 3: # Simulate failure for the first 3 attempts
        print("Connection failed. Retrying...")
        retries += 1
        time.sleep(delay)
        delay *= 2  # Double the delay for the next retry
    else:
        connection_successful = True
        print("Connection successful!")
```

This demonstrates the `while` loop's ability to manage dynamic variables (`retries`, `delay`) to create sophisticated, real-world logic.

-----

🛑 **Common Pitfall: Accidentally Infinite Loops**

An **infinite loop** is a `while` loop whose condition never becomes `False`. This can happen if the termination logic is flawed or missing.

**Example of an Infinite Loop:**

```python
count = 1
while count <= 5:
    print(f"Count is {count}")
    # The increment (count += 1) is missing!
```

Without the `count += 1` statement, the condition `count <= 5` will always be true, and the loop will never terminate.

**Debugging Infinite Loops:**

1.  **Trace with `print()`:** Add `print()` statements inside the loop to observe the values of the variables in the condition. This helps you identify which variable isn't changing as expected.
2.  **Add a Counter:** If you suspect a loop might run too long, add a simple counter and a `break` to stop it after a fixed number of iterations.
3.  **Use a Debugger:** Tools like the built-in `pdb` module allow you to step through code line by line, inspect variable values, and precisely locate the cause of the non-terminating loop.
4.  **Force Exit:** If a program is stuck, you can usually terminate it from the terminal by pressing **`Ctrl + C`**.

### 6.4 `break` and `continue`

The `break` and `continue` statements are powerful tools for fine-grained control over the flow of a loop. While they should be used judiciously to maintain code clarity, they are indispensable for handling specific conditions that arise during iteration.

#### Immediate Exit (`break`) vs. Skip Step (`continue`)

  * **`break`**: The `break` statement provides an immediate exit from the innermost loop in which it is located. When the program encounters a `break`, it completely terminates the loop and resumes execution at the first line of code after the loop's body. It's typically used when a desired condition is met, and there's no need to continue iterating.

  * **`continue`**: The `continue` statement skips the rest of the current loop iteration and immediately jumps to the next one. It is used when a specific condition is met, but you still want the loop to proceed with the remaining items. The program simply ignores the rest of the code block for that single pass and goes back to the top of the loop.

#### Clean Loop Exits: How and When to Apply

The `break` statement is crucial for making loops more efficient and concise. A common pattern is to use it for **early exit** when searching for an item.

**Example: Searching for an Element**
Without `break`, you might use a flag to track if an item was found.

```python
# Inefficient approach without `break`
numbers = [1, 5, 9, 13, 17]
found = False
for num in numbers:
    if num == 9:
        found = True
print(f"Item found: {found}")
# The loop continues to iterate even after finding the number 9.
```

With `break`, the loop exits as soon as the target is found, saving unnecessary iterations.

```python
# Efficient approach with `break`
numbers = [1, 5, 9, 13, 17]
found = False
for num in numbers:
    if num == 9:
        found = True
        break  # Exit immediately
print(f"Item found: {found}")
# The loop stops after checking the number 9.
```

#### Conditional Skips: Skipping Comments or Whitespace

The `continue` statement is perfect for filtering or skipping unwanted items during an iteration without terminating the entire loop. This keeps your main processing logic clean and unpolluted by conditional checks.

**Example: Processing a Data Stream**
Imagine you are processing a stream of data but need to ignore any lines that are empty or contain only a specific marker.

```python
data_lines = [
    "---start---",
    "item A",
    "",  # An empty line
    "item B",
    "# This is a comment",
    "item C"
]

for line in data_lines:
    # Skip empty lines
    if not line:
        continue
    # Skip lines that are comments
    if line.startswith("#"):
        continue

    # Main processing logic
    print(f"Processing data: '{line}'")
```

This pattern results in a much cleaner main processing block because all the filtering happens at the top of the loop body.

-----

🧪 **Example: Reading a file but ignoring all lines starting with `#`**

This is a classic file-parsing problem that perfectly demonstrates the power of `continue`. We want to iterate through a file and only process the valid data, skipping any lines that are comments (lines starting with `#`) or are just blank.

```python
# Assuming a file named 'config.ini' exists with the following content:
# # This is a configuration file
# user=admin
# password=secret
# # Database settings below
# db_host=localhost
#
# db_port=5432

# The `with open(...)` block ensures the file is closed automatically
with open('config.ini', 'r') as config_file:
    print("Reading config file, ignoring comments and blank lines:")
    for line in config_file:
        # Use .strip() to remove leading/trailing whitespace and the newline character
        cleaned_line = line.strip()

        # Conditional skip 1: ignore blank lines
        if not cleaned_line:
            continue

        # Conditional skip 2: ignore comment lines
        if cleaned_line.startswith('#'):
            continue

        # Main logic: process the valid line
        print(f"Found setting: {cleaned_line}")
```

###### This example shows how `continue` allows you to maintain a clean and uncluttered core logic for your loop, separating the "what to process" from the "what to skip."
-----

### 6.5 `else` Clause on Loops

The `else` clause on loops is one of Python's more unique and often-misunderstood control flow features. It provides a clean, elegant way to handle a specific outcome: when a loop completes **without** being terminated by a `break` statement.

#### When and How `else` is Triggered

The `else` block attached to a `for` or `while` loop will execute only under a specific condition:

  * **The loop completed its natural course.**
  * **The loop was not exited prematurely by a `break` statement.**

If a loop is exited by a `break`, the `else` block is completely skipped. If the loop finishes iterating through all its items (for a `for` loop) or if its condition becomes `False` (for a `while` loop), then the `else` block is executed.

**Example with a `for` loop:**

```python
# The `else` block executes
for i in range(5):
    print(i)
else:
    print("Loop finished successfully.")

# The `else` block is skipped
for i in range(5):
    if i == 2:
        break
    print(i)
else:
    print("Loop finished successfully.")
```

**Example with a `while` loop:**
This example demonstrates a process that continues until a certain count is reached. The `else` clause is used to confirm a "successful" completion.

```python
# Scenario 1: The `else` block executes
# The loop completes because the condition (count < 3) becomes False
count = 0
while count < 3:
    print(f"Count is {count}")
    count += 1
else:
    print("Loop finished naturally because count reached 3.")
# Output:
# Count is 0
# Count is 1
# Count is 2
# Loop finished naturally because count reached 3.

# -----------------------------------------------

# Scenario 2: The `else` block is skipped
# The loop is terminated by a 'break' statement
count = 0
while count < 10:
    print(f"Count is {count}")
    if count == 1:
        print("Breaking the loop!")
        break
    count += 1
else:
    print("Loop finished naturally.") # This line is NOT executed
# Output:
# Count is 0
# Count is 1
# Breaking the loop!
```

#### Use-Cases: Searching in a List and Validation Checks

The `else` clause is most commonly used to perform a final action when a search or a validation check comes up empty.

**Use-Case 1: Searching for an Item**
This pattern provides a clean way to check if an item was found in a list without needing a separate `found` flag variable.

```python
names = ["Alice", "Bob", "Charlie"]
target = "David"

for name in names:
    if name == target:
        print(f"Found {target} in the list!")
        break
else:
    # This block only runs if the 'break' was not triggered
    print(f"Could not find {target} in the list.")
```

**Use-Case 2: Validation Checks**
You can use a loop to validate a sequence of items and then use the `else` block to confirm that all items passed the check.

```python
usernames = ["alex_1", "beth-2", "cathy3"]
is_valid = False

for username in usernames:
    if not username.isalnum(): # .isalnum() checks if a string is alphanumeric
        print(f"Error: Invalid username '{username}'")
        is_valid = False
        break
else:
    # This only runs if the loop completed without finding any invalid usernames
    is_valid = True
    print("All usernames are valid.")
```

#### The Logic Behind `else` on `for` and `while`

The logic for both `for` and `while` loops is consistent: the `else` clause is triggered only when the loop concludes naturally.

  * **For loop `else`**: Executes after iterating through all items in the iterable.
  * **While loop `else`**: Executes when the loop's condition becomes `False`.

This consistency allows you to use the `else` clause for a wide range of "what if not found?" or "what if all checks pass?" scenarios.

-----

⚡ **Pro Insight Box: "Why most Python beginners misuse or ignore `else` on loops — and why you shouldn’t."**

Most Python beginners either ignore the `else` clause on loops or use it incorrectly because they think it works like a conditional `else` statement, where it executes simply if the `if` block is not run. This is a common misconception.

The `else` on a loop is not tied to the `if` statement within the loop; it is tied to the **loop's completion**.

**Why you should use it:**

  * **Clarity:** It makes your code's intent explicit. The `else` block clearly separates the logic for a "successful" loop completion from the logic for an early exit.
  * **Eliminates Flags:** As shown in the search example, it removes the need for an external boolean flag variable (`found = False`). This makes the code more concise and less prone to logical errors.
  * **Readability:** It's a clean, declarative way to say "do this if the loop finishes its work and finds nothing." It is a hallmark of idiomatic Python code.

<!-- end list -->

```python
# A common non-Pythonic pattern (requires a flag)
found_item = False
for item in my_list:
    if item == 'target':
        found_item = True
        break

if not found_item:
    # Logic for when item is not found
    ...

# The Pythonic way (using the loop's `else`)
for item in my_list:
    if item == 'target':
        break
else:
    # Logic for when item is not found
    ...
```

The Pythonic pattern is simpler, more direct, and immediately tells the reader that the `else` block is related to the loop's outcome.

### 6.6 `range()` – Mastering Iterables

The `range()` function is one of Python's most essential tools for generating a sequence of integers. It is not a list; instead, it is a memory-efficient iterable that produces numbers on demand, making it perfect for controlling loops.

#### `range(start, stop[, step])`

The `range()` function has a flexible syntax that allows you to control the sequence of numbers it generates:

  * `stop` (required): The loop will go up to, but not include, this number.
  * `start` (optional): The number to begin the sequence with. The default is 0.
  * `step` (optional): The difference between each number in the sequence. The default is 1.

**Basic Examples:**

```python
# range(stop) - starts at 0, steps by 1, and stops before 5
for i in range(5):
    print(i, end=" ") # Output: 0 1 2 3 4

# range(start, stop) - starts at 2, stops before 7
for i in range(2, 7):
    print(i, end=" ") # Output: 2 3 4 5 6

# range(start, stop, step) - starts at 1, steps by 2, stops before 10
for i in range(1, 10, 2):
    print(i, end=" ") # Output: 1 3 5 7 9
```

#### Negative Ranges, Skipping Steps

The `step` parameter can be a negative number, allowing you to count backward. When using a negative step, the `start` value must be greater than the `stop` value.

```python
# Negative step - starts at 10, steps by -1, stops before 0
for i in range(10, 0, -1):
    print(i, end=" ") # Output: 10 9 8 7 6 5 4 3 2 1

# Negative step with skipping - starts at 20, steps by -3, stops before 5
for i in range(20, 5, -3):
    print(i, end=" ") # Output: 20 17 14 11 8
```

#### Converting `range` to a `list`

A `range` object is a lightweight object that does not store all its numbers in memory. To see the full sequence of numbers or to access them by index, you can convert it into a `list`.

```python
# A range object itself
my_range = range(5)
print(my_range) # Output: range(0, 5)

# Converting to a list to see the full sequence
my_list = list(my_range)
print(my_list) # Output: [0, 1, 2, 3, 4]
```

#### Large `range` Memory Efficiency

The true power of `range()` is its memory efficiency. Because it generates numbers on the fly, a `range` object for a billion numbers takes up roughly the same amount of memory as a `range` object for ten numbers. This is a significant advantage over a full list.

```python
import sys

# The range object is small
large_range = range(1_000_000)
print(f"Size of range object: {sys.getsizeof(large_range)} bytes") # e.g., 48 bytes

# A list with the same numbers is much, much larger
large_list = list(large_range)
print(f"Size of list object: {sys.getsizeof(large_list)} bytes")   # e.g., 8000056 bytes
```

#### Use Cases for `for` and `while`

  * **`for` Loop:** This is the most common use case. `range()` is a perfect iterable for a `for` loop when you need to perform a task a fixed number of times or access a sequence by index.

    ```python
    my_list = ["a", "b", "c"]
    # Iterating over a list by index
    for i in range(len(my_list)):
        print(f"Index {i}: {my_list[i]}")

    # Iterating a fixed number of times
    for i in range(3):
        print("Hello")
    ```

  * **`while` Loop:** Although less common, `range()` can be used to define a termination condition for a `while` loop, especially in a state-based system where the `for` loop's simplicity is not sufficient. However, a simple counter is often preferred.

    ```python
    # A contrived example to show range() with a while loop
    current_number = 0
    my_countdown = range(5, 0, -1) # Create the range object

    # The while loop is more complex than a for loop here
    while current_number < len(list(my_countdown)):
        print(my_countdown[current_number])
        current_number += 1

    # This is better written with a for loop:
    # for num in range(5, 0, -1):
    #     print(num)
    ```

The `for` loop is almost always the superior and more readable choice when using `range()`. The `while` loop is better reserved for indefinite iteration.

-----

💡 **Hack Tip: Using `range()` in reverse with `reversed()` and `-1`**

There are two primary ways to create a reverse sequence of numbers with `range()`. The first is with a negative step, and the second is by using the `reversed()` function, which is often considered more readable.

```python
# Method 1: Using a negative step
# This is explicit and clear but can be verbose
for i in range(5, -1, -1):
    print(i, end=" ") # Output: 5 4 3 2 1 0

print("\n")

# Method 2: Using the reversed() function
# This is often considered more Pythonic and readable
for i in reversed(range(6)):
    print(i, end=" ") # Output: 5 4 3 2 1 0
```

The `reversed()` function works on any sequence or iterable, making it a versatile and declarative way to indicate a reverse iteration.
