# Solve It If You Can

### Debugging & Error Analysis

**Question 1: The Deceptive Default**

The following function is intended to create independent user profiles, each with a default set of permissions. However, when a new permission is granted to one user, it unexpectedly affects other users. Identify the bug, explain why it happens, and provide a corrected version of the code.

```python
# BUGGY CODE
def create_user_profile(username, permissions={'read', 'comment'}):
    # This function is intended to create isolated user profiles.
    profile = {
        'username': username,
        'permissions': permissions
    }
    def grant_permission(permission):
        # This inner function should only modify the current user's permissions.
        profile['permissions'].add(permission)
        print(f"Granted '{permission}' to {profile['username']}.")
    
    return profile, grant_permission

# Usage
user1_profile, grant_perm_user1 = create_user_profile("Alice")
user2_profile, grant_perm_user2 = create_user_profile("Bob")

# Grant 'write' permission only to Alice
grant_perm_user1('write')

# Check Bob's permissions - Why was he also affected?
print(f"Bob's permissions: {user2_profile['permissions']}")
```

**Question 2: The Misunderstood `nonlocal`**

The `create_game` function is designed to manage a game's state using closures. The `decrease_score` function, however, fails with a `SyntaxError` or doesn't modify the score as intended. Explain the exact reason for the error and the flaw in its scope logic. Correct the `create_game` function so it works as expected.

```python
# BUGGY CODE
def create_game(initial_score):
    history = []
    
    def increase_score(points):
        nonlocal initial_score # This is incorrect
        initial_score += points
        history.append(f"Increased by {points}")
        return initial_score

    def decrease_score(points):
        # This function causes a SyntaxError: no binding for nonlocal 'initial_score' found
        # Or if we assign, it creates a new local variable.
        nonlocal initial_score 
        initial_score -= points
        history.append(f"Decreased by {points}")
        return initial_score
        
    def get_history():
        return history
        
    return increase_score, decrease_score, get_history

# This will fail
inc, dec, hist = create_game(100)
```

**Question 3: The Unpacking Order Trap**

The following function call raises a `TypeError`. Explain the precise rule of argument ordering that is being violated. Rearrange the arguments in the function call to fix the error while still using both unpacking operators.

```python
# BUGGY CODE
def setup_environment(name, *configs, is_prod, **options):
    print(f"Environment: {name}")
    print(f"Configs: {configs}")
    print(f"Production Mode: {is_prod}")
    print(f"Options: {options}")

config_list = ['network.conf', 'db.conf']
option_dict = {'retries': 3, 'timeout': 60}

# This call will fail
setup_environment('prod-db', **option_dict, *config_list, is_prod=True)
```

**Question 4: The Flawed Recursive Validator**

This recursive function aims to validate a nested data structure where every string must be at least 3 characters long. It works for some cases but fails silently for others (returns `True` when it should be `False`). Identify the logical flaw in the recursion and correct it.

```python
# BUGGY CODE
def validate_structure(data):
    if isinstance(data, str):
        return len(data) >= 3
    if isinstance(data, list):
        for item in data:
            validate_structure(item) # The mistake is here
    return True # And here

# Test cases
print(validate_structure(["abc", ["def", ["ghi"]]]))  # Correctly returns True
print(validate_structure(["abc", ["de", ["fgh"]]]))   # Incorrectly returns True
```

**Question 5: The Impure Memoization**

The `@lru_cache` decorator is used to optimize `get_user_status`, but the system behaves unpredictably. The status for a user seems to be "stuck" even after their data has changed in the "database". Why is memoization failing here, and what core principle of its usage is being violated? How would you redesign this interaction?

```python
from functools import lru_cache

# A fake database
USER_DATABASE = {
    1: {'name': 'Alice', 'status': 'active'},
    2: {'name': 'Bob', 'status': 'pending'}
}

@lru_cache(maxsize=None)
def get_user_status(user_id):
    # This function reads from an external state
    print(f"Fetching status for user {user_id} from database...")
    return USER_DATABASE.get(user_id, {}).get('status')

# First call for user 2
print(get_user_status(2))

# Update user 2's status in the database
USER_DATABASE[2]['status'] = 'active'

# Second call for user 2 - it returns the old, cached value!
print(get_user_status(2))
```

-----

### Output Prediction

**Question 6: The Decorator and Closure Interaction**

Predict the exact output of the following code. Explain the flow of execution, paying close attention to when each `print` statement is executed and what the values of `x` and `y` are at each step.

```python
def outer(x):
    def decorator(func):
        def wrapper(*args, **kwargs):
            print(f"Outer x: {x}")
            result = func(*args, **kwargs)
            print(f"Inner y: {wrapper.y}")
            return result
        wrapper.y = x * 10
        return wrapper
    return decorator

@outer(x=5)
def my_func(z):
    print(f"Function z: {z}")
    return z + 1

my_func(2)
```

**Question 7: The `*args`, `**kwargs`, and Partial Application Puzzle**

What will be the exact output of the final `print` statement? Trace how the arguments are collected, passed, and overwritten through the layers of `partial` and function calls.

```python
from functools import partial

def processor(a, b, *args, c=10, **kwargs):
    print(f"a={a}, b={b}, c={c}, args={args}, kwargs={kwargs}")

p1 = partial(processor, 1, 2, 3, c=5)
p2 = partial(p1, 4, d=20, e=30)

p2(5, b=6) # What happens here?
```

**Question 8: The Recursive Generator Mind-Bender**

Trace the execution of `reversed_gen` and predict the exact list that `final_list` will hold. Explain the role of `yield from` in achieving the final order.

```python
def reversed_gen(data):
    if len(data) > 0:
        yield from reversed_gen(data[1:])
        yield data[0]

final_list = list(reversed_gen("abc"))
print(final_list)
```

**Question 9: The `__call__` and First-Class Function Conundrum**

Predict the output of this code. Explain how a class instance can be used as a function within a higher-order function like `process_data`.

```python
class Multiplier:
    def __init__(self, factor):
        self._factor = factor
    
    def __call__(self, value):
        return self._factor * value

def process_data(func, value):
    return func(value + 1)

doubler = Multiplier(2)
result = process_data(doubler, 4)
print(result)
```

**Question 10: The `nonlocal` and Lambda Interaction**

What is the output of the final `print` statement? Explain how the `nonlocal` keyword allows the lambda to modify the state of its enclosing scope.

```python
def create_event_handler():
    triggered_count = 0
    
    def on_event(x):
        nonlocal triggered_count
        triggered_count += 1
        return x % triggered_count == 0

    return on_event

handler = create_event_handler()
results = [handler(i) for i in range(1, 6)]
print(results)
```

-----

### Constraint Mapping & Edge Case Analysis

**Question 11: Breaking the Sorter**

The `sort_by_priority` function uses a `lambda` as a key. Identify three distinct types of input for the `items` list that would cause this function to raise an exception. For each case, name the specific exception (`TypeError`, `KeyError`, etc.) and explain why it occurs.

```python
# The function to analyze
def sort_by_priority(items):
    # Priorities: 'high' -> 0, 'medium' -> 1, 'low' -> 2
    priority_map = {'high': 0, 'medium': 1, 'low': 2}
    return sorted(items, key=lambda x: priority_map[x['priority']])

# Example valid input:
# sort_by_priority([{'priority': 'low', 'task': 'b'}, {'priority': 'high', 'task': 'a'}])
```

**Question 12: Ineffective `lru_cache`**

The `process_data` function is memoized, but for a certain category of inputs, the cache provides no performance benefit. Describe this category of inputs and explain why `@lru_cache` fails to be effective.

```python
from functools import lru_cache
import time

@lru_cache(maxsize=128)
def process_data(config):
    # A costly operation
    time.sleep(1) 
    return config['id'] * 2

# What kind of inputs to 'process_data' would make the cache useless?
```

**Question 13: The Fragile Unpacker**

The function `create_report` expects to receive data by unpacking a dictionary. What specific key in the `report_data` dictionary would cause this function to fail with a `TypeError`? Explain the underlying conflict between keyword arguments and `**kwargs`.

```python
def create_report(title, **metadata):
    print(f"Title: {title}")
    for key, value in metadata.items():
        print(f"- {key}: {value}")

report_data = {'title': 'Q1 Sales', 'author': 'Jim', 'year': 2025}

# What key, if added to or renamed in report_data, would break this call?
# create_report(**report_data) 
```

**Question 14: The Ambiguous Positional Argument**

Consider the function `flexible_sum`. Determine for what inputs the function returns a mathematically correct sum as intended, and identify a class of inputs where it runs without error but produces a logically incorrect or nonsensical result due to the flexibility of `*args`.

```python
def flexible_sum(base_value, *additions):
    total = base_value
    for val in additions:
        total += val
    return total

# What inputs would produce a valid but nonsensical output?
```

**Question 15: The Limits of Recursion**

The `deep_get` function recursively retrieves a value from a nested dictionary. What is the primary constraint of this implementation in standard CPython? Describe a realistic input for `data` and `keys` that would cause the program to crash, and name the error it would raise.

```python
def deep_get(data, keys):
    if not keys or data is None:
        return data
    return deep_get(data.get(keys[0]), keys[1:])

# How can you make this function crash?
```

-----

### Conceptual & Design Challenges

**Question 16: Reimplementing `partial`**

Without using `functools.partial`, write your own higher-order function named `custom_partial` that mimics its behavior. It should take a function, `*args`, and `**kwargs` and return a new callable object that holds the pre-filled arguments.

```python
# Your implementation here
def custom_partial(func, *p_args, **p_kwargs):
    # ... your code ...
    pass

# Example Usage:
# def power(base, exponent):
#     return base ** exponent
#
# square = custom_partial(power, exponent=2)
# print(square(5)) # Expected: 25
```

**Question 17: State with Closures vs. Callables**

Implement a stateful counter that can be incremented, decremented, and have its value retrieved. Provide two complete implementations:

1.  Using a closure that returns a dictionary of functions.
2.  Using a callable class instance (`__call__`).

After implementing both, write a brief analysis comparing the two approaches in terms of readability, extensibility, and state encapsulation.

**Question 18: A Decorator that Accepts Arguments**

Write a decorator named `enforce_types` that takes type arguments (e.g., `@enforce_types(int, int, returns=str)`). The decorator should check if the decorated function is called with arguments of the specified types and if its return value matches the `returns` type. If not, it should raise a `TypeError`.

```python
# Your decorator implementation here

# Example Usage:
# @enforce_types(int, int, returns=str)
# def combine_values(a, b):
#     return str(a) + str(b)
#
# combine_values(5, 10) # Should work
# combine_types(5, '10') # Should raise TypeError
```

**Question 19: The Purest Refactoring**

The following function is "impure" and has side effects. Refactor it into a set of smaller, pure functions. The final call should compose these pure functions to achieve the same result as the original. Explain why your new design is more testable and referentially transparent.

```python
# Impure function to refactor
USER_DISCOUNTS = {'premium': 0.15, 'standard': 0.05}
PROCESSED_ORDERS = []

def process_order(user, cart):
    # 1. Calculate total
    total_price = sum(item['price'] for item in cart)
    
    # 2. Apply discount (side effect: reads global)
    discount_rate = USER_DISCOUNTS.get(user['plan'], 0)
    final_price = total_price * (1 - discount_rate)
    
    # 3. Record order (side effect: modifies global)
    PROCESSED_ORDERS.append({
        'user_id': user['id'],
        'price': final_price
    })
    
    # 4. Print confirmation (side effect: I/O)
    print(f"Order processed for user {user['id']}. Final price: ${final_price:.2f}")
    return final_price
```

**Question 20: The WET vs. DRY Dilemma**

The two functions below share similar but not identical logic. A junior developer argues they should be refactored into a single function to adhere to the DRY principle. A senior developer argues they should remain separate. Make a compelling argument for the **senior developer's position**, referencing the concept of "accidental vs. intentional" repetition and the principle of balancing DRY with clarity.

```python
def generate_web_report(data):
    # Generates an HTML report
    html = "<h1>Web Report</h1>"
    html += f"<p>Items processed: {len(data)}</p>"
    for item in data:
        html += f"<div>{item['id']} - {item['value']}</div>"
    return html

def generate_api_summary(data):
    # Generates a JSON summary for an API
    summary = {
        'type': 'api_summary',
        'items_processed': len(data),
        'items': [{'id': item['id'], 'value': item['value']} for item in data]
    }
    return summary
```

**Question 21: Deep Argument Unpacking and Forwarding**

Write a generic "wrapper" function that accepts another function `func` as an argument. This wrapper must be able to accept any combination of positional and keyword arguments and forward them *perfectly* to `func`. Then, create a `logged_call` function that uses this wrapper to print the arguments *before* calling the original function. Demonstrate its use on a function with a complex signature (e.g., positional, keyword-only, `*args`, and `**kwargs`).

**Question 22: Combining `yield` and `return` in a Generator**

While a function can have both `yield` and `return` statements, a `return` with a value inside a generator has a special meaning. What is that meaning as of Python 3.3+? Write a small piece of code that demonstrates how to capture this return value from a generator. Explain a practical scenario where this feature might be useful.

**Question 23: Memoizing an Unhashable Type**

The `@lru_cache` decorator fails when a function's arguments are unhashable (like a dictionary). Write a custom memoization decorator that can handle a function that takes a single dictionary argument. Your decorator must serialize the dictionary into a hashable format (e.g., a frozen string representation) to use it as a cache key.

**Question 24: Fail Early, Fail Loudly**

Refactor the following function to adhere strictly to the "fail early, fail loudly" principle. The current implementation mixes validation with logic and returns `None`, which can hide errors. Your version should perform all validation up front and raise specific, informative exceptions.

```python
# Refactor this function
def create_user_record(data):
    if 'username' in data and len(data['username']) > 3:
        username = data['username']
        if 'email' in data and '@' in data['email']:
            email = data['email']
            # ...imagine more logic here...
            return {'username': username, 'email': email}
    return None # This is bad practice
```

**Question 25: Callable Class for Event Handling**

Design a callable class `EventDispatcher` that manages a list of callback functions.

  - The `__init__` should accept an event name.
  - The instance should be callable (`__call__`), which will trigger all registered callbacks, passing any arguments it receives to them.
  - It should have a `register()` method to add a callback function.

Demonstrate its use by creating a dispatcher for an "on\_click" event and registering two different lambda functions as callbacks.

**Question 26: Predict the Shadowing**

Predict the output of this code. Explain the concept of variable shadowing and how the LEGB rule applies to both `x` and `my_list` in this specific, tricky example.

```python
x = 100
my_list = [1]

def update_stuff(my_list):
    x = 50
    my_list.append(x)
    return my_list

new_list = update_stuff(my_list)

print(x)
print(my_list)
print(new_list)
```

**Question 27: The `global` vs. `nonlocal` Nuance**

Explain the difference in behavior between `func1` and `func2`. Why does one work and the other raise an error? What does this tell you about where `nonlocal` looks for variables?

```python
# Scenario 1
def func1():
    x = 1
    def inner():
        nonlocal x
        x = 2
    inner()
    return x

# Scenario 2
x = 1
def func2():
    def inner():
        nonlocal x # This will cause an error
        x = 2
    inner()
    return x

print(func1())
# print(func2()) # This call would fail
```

**Question 28: A Recursive Palindrome with a Twist**

The standard recursive palindrome checker works on strings. Write a more generic recursive function, `is_reversible`, that checks if a list is a palindrome *without converting it to any other data type or using slicing*. It must use only indexing and recursion. What is the performance complexity (Big O notation) of your solution in terms of time and space?

**Question 29: Abusing Lambdas**

While lambdas are meant for simple expressions, they can be abused to perform complex, multi-step logic. The following lambda attempts to find the first even number in a list. It is syntactically valid. Explain how it works, why it is considered terrible practice, and rewrite it as a proper, readable `def` function.

```python
# Obscure lambda
find_first_even = (lambda l: (lambda f, a: f(f, a))(lambda f, a: a[0] if a and a[0] % 2 == 0 else f(f, a[1:]), l))

# Why is this so bad, and what's the better way?
# print(find_first_even([1, 3, 5, 6, 7, 8])) # Correctly returns 6
```

**Question 30: The Ultimate Function Design**

You are tasked with creating a function that fetches data from an API. Design the *signature* and *docstring* for this function, applying as many principles from the chapter as possible. Your design should include:

  - A clear, expressive name.
  - Type hints for all parameters and the return value, using the `typing` module for complex types.
  - At least one parameter with a sensible default value.
  - Use of `*args` or `**kwargs` for flexibility.
  - At least one keyword-only argument to enforce clarity.
  - A docstring that explains the function's purpose, its parameters (the contract), and what it returns, including any potential exceptions it might raise (fail-loudly).

You do not need to implement the function's body; the goal is to design the perfect, self-documenting interface.
