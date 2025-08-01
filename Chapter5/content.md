# Control Flow — If, Else, Elif Patterns

### 🧠 FOUNDATIONAL THEORY

#### 1\. **Decision-Making in Programs**

Imagine your daily life. You constantly make decisions: "If it's raining, I'll take an umbrella. Else, I'll walk without one." Or, "If I finish my work early, I can watch a movie. Otherwise, I'll keep working." These choices, based on certain conditions, guide your actions.

Just like us, computer programs need to make decisions to adapt to different situations, process varied inputs, and execute specific tasks. This ability to make choices is the core of **conditional logic** or **decision-making** in programming.

**Why Conditional Logic Exists:**

1.  **Adaptability:** Programs aren't static. They interact with users, data, and external systems that constantly change. Conditional logic allows a program to respond dynamically to these changes.
      * *Example:* A website might show a "Login" button if a user is not authenticated, but a "Profile" link if they are.
2.  **Handling Diverse Inputs:** Not all inputs are the same. A program needs to behave differently based on the type, value, or format of data it receives.
      * *Example:* A calculator needs to perform addition if the user enters `+`, subtraction if `-`, and so on.
3.  **Error Handling & Validation:** Programs need to ensure data is valid and prevent crashes. Conditional logic helps check for erroneous inputs or unexpected states.
      * *Example:* Before dividing two numbers, a program should check if the divisor is zero to avoid a `ZeroDivisionError`.
4.  **Implementing Business Rules:** Most applications embody specific business rules, which are inherently conditional.
      * *Example:* "Customers spending over ₹5000 get a 10% discount."
5.  **Controlling Program Flow:** Conditional statements dictate the exact path of execution a program takes, skipping certain blocks of code and executing others based on conditions.

-----

**Mapping Real-World Decision Trees to `if/else` Structures:**

A powerful way to think about conditional logic is by visualizing real-world decision processes as "decision trees." Each branch represents a condition, and each leaf represents an action.

Let's take the "morning routine" example:

**Real-World Decision Tree:**

  * **Start:** Wake Up
      * **Condition:** Is it a weekday?
          * **YES:**
              * **Condition:** Do I have an early meeting?
                  * **YES:** Get dressed quickly.
                  * **NO:** Have a leisurely breakfast.
              * Go to work.
          * **NO (Weekend):**
              * Sleep in.
              * Do chores.
      * **End:** Day continues.

**Mapping to `if/else` Structure (Conceptual Code):**

```python
# Simplified Conceptual Code

is_weekday = True
has_early_meeting = False # Or True, depending on the day

if is_weekday:
    # This block executes only if it's a weekday
    if has_early_meeting: # Nested decision
        print("Get dressed quickly.")
    else:
        print("Have a leisurely breakfast.")
    print("Go to work.")
else:
    # This block executes only if it's NOT a weekday (i.e., weekend)
    print("Sleep in.")
    print("Do chores.")

print("Day continues.")
```

**Key Takeaways from Mapping:**

  * **Conditions:** Real-world questions ("Is it raining?", "Is it a weekday?") become **Boolean expressions** (expressions that evaluate to `True` or `False`).
  * **Actions:** What you do based on the answer ("Take umbrella," "Go to work") become **blocks of code** that execute if the condition is met.
  * **Alternatives:** The "otherwise" or "else" scenarios are handled by `else` or `elif` (else if) clauses, ensuring that different paths are taken based on different conditions.
  * **Nesting:** Decisions can be nested within other decisions, just like branches on a tree can have sub-branches.

-----

**Flowchart to Code Mapping:**

Flowcharts are visual diagrams that represent the steps and decisions in a process. They are excellent tools for designing and understanding control flow before writing actual code.

**Common Flowchart Symbols:**

  * **Oval (Terminal):** Start or End of a process.
  * **Rectangle (Process):** An action or operation.
  * **Diamond (Decision):** A point where a decision is made, usually with "Yes/No" or "True/False" branches.
  * **Arrow (Flow Line):** Indicates the direction of flow.

**Example: Check if a number is positive, negative, or zero.**

**Flowchart:**


```mermaid
flowchart TD
    A(Start) --> B(Input Number)
    B --> C{Number > 0?}
    C -->|Yes| D(Print Positive)
    C -->|No| E{Number < 0?}
    E -->|Yes| F(Print Negative)
    E -->|No| G(Print Zero)
    D --> H(End)
    F --> H
    G --> H

```

**Mapping to Python `if/elif/else` Code:**

```python
# Python Code
number = float(input("Enter a number: ")) # Input Number

if number > 0: # Number > 0? (Decision Diamond)
    print("Positive") # Print "Positive" (Process Rectangle)
elif number < 0: # Number < 0? (Decision Diamond)
    print("Negative") # Print "Negative" (Process Rectangle)
else: # If neither of the above conditions is met
    print("Zero") # Print "Zero" (Process Rectangle)

# The program naturally ends after one path is executed.
```

**Key Principles for Flowchart-to-Code:**

  * **Diamond Shapes** directly translate to `if` or `elif` statements, representing a condition.
  * **Rectangles** translate to the code blocks (indented lines) that execute if a condition is met.
  * **Flow Lines** indicate the sequence of execution. Multiple lines converging into one point (e.g., to `End`) show that different paths eventually lead to the same subsequent step.

Understanding this mapping helps you break down complex logic into manageable, visual steps, making it easier to write correct and efficient conditional code.
