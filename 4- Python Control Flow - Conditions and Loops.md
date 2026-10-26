# Episode 5 — Python Control Flow: Conditions and Loops

## Overview

In this episode, we learn how to control the execution flow of a Python program using conditional statements and loops.

So far, we have learned how to store data in variables, work with different data types, and understand how Python handles objects. Now, we will learn how to make decisions and repeat operations.

We will cover:

- Conditional statements: `if`, `else`, and `elif`
- Comparison and logical operators
- The walrus operator (`:=`)
- Pattern matching with `match` and `case`
- Nested conditions
- Truthy and falsy values
- Ternary expressions
- Membership operators
- Guard clauses
- `for` and `while` loops
- `range()`, `enumerate()`, and `zip()`
- `break` and `continue`
- Nested loops

## Learning Objectives

By the end of this episode, you should be able to:

1. Write conditional statements to make decisions.
2. Combine conditions using logical operators.
3. Understand how Python evaluates truthy and falsy values.
4. Use `match` to handle multiple possible cases.
5. Write `for` and `while` loops.
6. Control loop execution using `break` and `continue`.
7. Iterate through lists and dictionaries.
8. Use `enumerate()` and `zip()` to process related data.
9. Apply conditions and loops to solve practical problems.

---

# Part 1 — Conditional Statements

## 1. The `if` Statement

An `if` statement executes a block of code only when its condition evaluates to `True`.

### Example

```python
age = 20

if age >= 18:
    print("Access granted")
```

Output:

```text
Access granted
```

### Explanation

- `age >= 18` is the condition.
- If the condition is `True`, Python executes the indented block.
- If the condition is `False`, Python skips that block.

Python uses indentation to define code blocks. Four spaces per indentation level is the standard convention.

### Teaching Question

What happens if `age = 16`?

```python
age = 16

if age >= 18:
    print("Access granted")
```

**Answer:** Nothing is printed because the condition is `False`.

---

## 2. Comparison Operators

Comparison operators compare values and produce a Boolean result: `True` or `False`.

```python
x = 10

print(x == 10)
print(x != 10)
print(x > 5)
print(x < 5)
print(x >= 10)
print(x <= 10)
```

Output:

```text
True
False
True
False
True
True
```

| Operator | Meaning | Example |
|---|---|---|
| `==` | Equal to | `x == 10` |
| `!=` | Not equal to | `x != 10` |
| `>` | Greater than | `x > 5` |
| `<` | Less than | `x < 5` |
| `>=` | Greater than or equal to | `x >= 10` |
| `<=` | Less than or equal to | `x <= 10` |

**Important:** `=` assigns a value, while `==` compares two values.

```python
x = 10       # Assignment
print(x == 10)  # Comparison
```

---

## 3. The `if / else` Statement

Use `else` when you want to execute one block if the condition is `True` and another block if it is `False`.

```python
age = 16

if age >= 18:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access denied
```

Only one of the two blocks executes.

### Practical Example: Login Access

```python
is_authenticated = True

if is_authenticated:
    print("Welcome to the application")
else:
    print("Please log in")
```

---

## 4. The `if / elif / else` Statement

Use `elif` when you need to check multiple conditions in sequence.

```python
score = 75

if score >= 90:
    print("Grade A")
elif score >= 70:
    print("Grade B")
elif score >= 50:
    print("Grade C")
else:
    print("Failed")
```

Output:

```text
Grade B
```

### How Does It Work?

Python evaluates the conditions from top to bottom.

1. If `score >= 90` is true, it prints Grade A and skips the remaining branches.
2. Otherwise, it checks `score >= 70`.
3. If that condition is true, it prints Grade B and stops checking.
4. If none of the conditions is true, it executes `else`.

**Important:** Only the first matching branch executes.

### Why Does the Order Matter?

Consider this example:

```python
score = 95

if score >= 50:
    print("Grade C")
elif score >= 70:
    print("Grade B")
elif score >= 90:
    print("Grade A")
```

Output:

```text
Grade C
```

The first condition is already true, so Python never reaches the other branches.

Always order overlapping conditions carefully, usually from the most restrictive or highest threshold to the lowest.

---

## 5. The Walrus Operator (`:=`)

The walrus operator, introduced in Python 3.8, assigns a value to a variable as part of an expression.

```python
if (age := 20) >= 18:
    print("Access granted")
```

Output:

```text
Access granted
```

This statement assigns `20` to `age` and then checks whether `age >= 18`.

It is equivalent in effect to:

```python
age = 20

if age >= 18:
    print("Access granted")
```

### A More Practical Example

```python
while (command := input("Enter a command (or 'exit'): ")) != "exit":
    print(f"You entered: {command}")

print("Goodbye!")
```

The walrus operator can be useful when an assignment and a condition naturally belong together.

However, it can make code harder to read if overused. For beginners, learn ordinary assignment and conditions first.

---

## 6. The `match / case` Statement

Python 3.10 introduced structural pattern matching with `match` and `case`.

It is useful when a value may match one of several known patterns.

### Example: Command Handler

```python
command = input("Enter a command (buy, price, help, exit): ")

match command:
    case "buy":
        print("Product added to cart.")

    case "price":
        print("Product price: $100")

    case "help":
        print("Available commands: buy, price, help, exit")

    case "exit":
        print("Goodbye!")

    case _:
        print("Invalid command!")
```

If the user enters `price`, the output is:

```text
Product price: $100
```

### Explanation

- `match command` evaluates the value to match.
- Each `case` describes a possible match.
- `case _` is the wildcard case, used as a default when no earlier case matches.

For this example, `match` is similar to a `switch` statement in some other programming languages.

### When Should You Use `match`?

It works well for command handlers, state processing, and matching structured data.

For simple ranges, such as checking whether a score is above 90, ordinary `if / elif / else` is generally more appropriate.

---

# Part 2 — Logical Operators and Conditions

## 7. Logical Operator: `and`

The `and` operator combines conditions. The overall result is truthy only if both operands are truthy.

```python
age = 25
has_ticket = True

if age >= 18 and has_ticket:
    print("You can enter")
else:
    print("Entry denied")
```

Output:

```text
You can enter
```

Both requirements must be satisfied:

- The person must be at least 18.
- The person must have a ticket.

If either condition is false, the `else` block executes.

---

## 8. Logical Operator: `or`

The `or` operator is useful when at least one of multiple conditions must be satisfied.

```python
is_admin = False
is_manager = True

if is_admin or is_manager:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access granted
```

The user is a manager, so the condition is satisfied even though `is_admin` is false.

---

## 9. Logical Operator: `not`

The `not` operator reverses the truth value of an expression.

```python
is_active = False

if not is_active:
    print("User is inactive")
```

Output:

```text
User is inactive
```

Because `is_active` is false, `not is_active` evaluates to true.

### Quick Comparison

| Operator | Meaning | Example |
|---|---|---|
| `and` | Both conditions must be truthy | `age >= 18 and has_ticket` |
| `or` | At least one condition must be truthy | `is_admin or is_manager` |
| `not` | Reverses the truth value | `not is_active` |

### Short-Circuit Evaluation

Python does not always evaluate both operands of `and` or `or`.

```python
is_authenticated = False

if is_authenticated and perform_expensive_check():
    print("Access granted")
```

If `is_authenticated` is false, Python does not call `perform_expensive_check()`.

Similarly:

```python
is_admin = True

if is_admin or perform_expensive_check():
    print("Access granted")
```

If `is_admin` is true, the second operand is not evaluated.

This behavior is called *short-circuit evaluation*.

---

## 10. Nested Conditions

A nested condition is an `if` statement inside another conditional block.

```python
age = 25
has_ticket = True

if age >= 18:
    if has_ticket:
        print("You can enter")
    else:
        print("Ticket required")
else:
    print("You must be at least 18")
```

Output:

```text
You can enter
```

Python first checks the person's age. Only if the person is at least 18 does it check the ticket.

### Nested Conditions vs. Logical Operators

The same logic can often be written more concisely:

```python
if age >= 18 and has_ticket:
    print("You can enter")
else:
    print("Entry denied")
```

Use nested conditions when the second decision depends on the result of the first or when each branch needs its own handling. Use logical operators when a combined condition makes the logic clearer.

---

## 11. Truthy and Falsy Values

Python allows many types of values to be used directly in conditions.

Some values are falsy:

- `False`
- `None`
- Numeric zero, such as `0`, `0.0`, and `0j`
- Empty strings, such as `""`
- Empty collections, such as `[]`, `{}`, `()`, and `set()`

Most other values are truthy, including non-empty strings and non-empty collections.

### Example

```python
username = ""

if username:
    print("Username exists")
else:
    print("Username is empty")
```

Output:

```text
Username is empty
```

Because the string is empty, Python treats it as false in the condition.

### Understanding `bool()`

```python
values = [0, 1, "", "False", [], [0], None]

for value in values:
    print(repr(value), bool(value))
```

Output:

```text
0 False
1 True
'' False
'False' True
[] False
[0] True
None False
```

### Why Is `"False"` Truthy?

The string `"False"` contains characters, so it is a non-empty string.

Its truth value is therefore `True`.

```python
print(bool("False"))  # True
print(bool(False))   # False
```

**Important:** The truthiness of a string is not determined by the meaning of the text it contains.

### When Is Truthiness Useful?

It is common to check whether a collection contains data:

```python
students = []

if students:
    print("Students found")
else:
    print("No students found")
```

This is often clearer than explicitly checking `if len(students) > 0`.

---

## 12. Ternary Conditional Expression

A ternary expression lets you choose between two values in a single expression.

```python
age = 20

status = "Adult" if age >= 18 else "Minor"

print(status)
```

Output:

```text
Adult
```

The general syntax is:

```python
value_if_true if condition else value_if_false
```

### Equivalent Version

```python
age = 20

if age >= 18:
    status = "Adult"
else:
    status = "Minor"
```

Both versions assign the same value to `status`.

### When Should You Use It?

Use a ternary expression for simple choices. For complex logic, multiple branches, or side effects, a normal `if / else` statement is generally easier to read.

---

## 13. Membership Operators: `in` and `not in`

Membership operators check whether a value is contained in a collection or sequence.

```python
allowed_roles = ["admin", "manager", "developer"]
user_role = "manager"

if user_role in allowed_roles:
    print("Access granted")
else:
    print("Access denied")
```

Output:

```text
Access granted
```

### Using `not in`

```python
blocked_users = ["user123", "user456"]
username = "user789"

if username not in blocked_users:
    print("User is allowed")
```

Output:

```text
User is allowed
```

Membership checks behave differently depending on the collection type.

For example, checking membership in a dictionary checks its keys:

```python
user = {
    "name": "Ali",
    "age": 25,
}

print("name" in user)  # True
print("Ali" in user)   # False
```

For repeated membership checks, a set can be more efficient than a list when the data and use case are suitable.

---

## 14. Guard Clauses

A guard clause checks for a condition that should cause a function to stop early.

This can reduce deeply nested conditions and make functions easier to read.

### Example

```python
def process_user(user):
    if user is None:
        return "Rejected"

    if not user["active"]:
        return "Rejected"

    if user["age"] < 18:
        return "Rejected"

    return "Processed"


print(process_user({"age": 25, "active": True}))
print(process_user({"age": 16, "active": True}))
print(process_user(None))
```

Output:

```text
Processed
Rejected
Rejected
```

### How Does It Work?

1. If `user` is `None`, the function returns immediately.
2. If the user is inactive, the function returns immediately.
3. If the user is under 18, the function returns immediately.
4. If none of the rejection conditions applies, the function returns `"Processed"`.

### A Practical Improvement

The original example assumes that any non-`None` user has valid `"active"` and `"age"` keys. Missing keys would raise a `KeyError`.

For real applications, validate the input structure as well:

```python
def process_user(user):
    if user is None:
        return "Rejected"

    if "active" not in user or "age" not in user:
        return "Invalid user data"

    if not user["active"]:
        return "Rejected"

    if user["age"] < 18:
        return "Rejected"

    return "Processed"
```

Guard clauses are especially useful for input validation, permissions, authentication checks, and request handling.

---

## 15. Practical Example: Calculating a Discount

Consider a product with a price of 4,500,000.

```python
price = 4_500_000

if price < 1_000_000:
    discount = 0
elif price < 5_000_000:
    discount = 0.10
else:
    discount = 0.20

final_price = price * (1 - discount)

print(f"Discount: {discount:.0%}")
print(f"Final price: {final_price:,.0f}")
```

Output:

```text
Discount: 10%
Final price: 4,050,000
```

### Explanation

The underscores in `4_500_000` improve readability. They do not change the numeric value.

The price is greater than or equal to 1,000,000 but less than 5,000,000, so the discount is 10%.

The final price is calculated as:

`price × (1 − discount)`

The f-string format specifiers mean:

- `:.0%` formats a decimal as a percentage with zero decimal places.
- `:,.0f` formats a number with thousands separators and zero decimal places.

---

# Part 3 — Loops

## 16. The `for` Loop

A `for` loop iterates over the items in an iterable, such as a list, string, tuple, dictionary, or range.

```python
for number in range(5):
    print(number)
```

Output:

```text
0
1
2
3
4
```

The loop runs once for each value produced by `range(5)`.

### Iterating Through a List

```python
students = ["Ali", "Sara", "Reza"]

for student in students:
    print(student)
```

Output:

```text
Ali
Sara
Reza
```

The variable `student` receives each list element in turn.

### Iterating Through a String

```python
for character in "Python":
    print(character)
```

Each character is processed separately.

---

## 17. The `range()` Function

The `range()` function generates a sequence of integers commonly used in loops.

It supports three common forms.

### Form 1: `range(stop)`

```python
for number in range(5):
    print(number)
```

Produces `0, 1, 2, 3, 4`.

The stop value is excluded.

### Form 2: `range(start, stop)`

```python
for number in range(2, 6):
    print(number)
```

Output:

```text
2
3
4
5
```

### Form 3: `range(start, stop, step)`

```python
for number in range(0, 10, 2):
    print(number)
```

Output:

```text
0
2
4
6
8
```

The `step` determines how much the value changes on each iteration.

Negative steps are also supported:

```python
for number in range(5, 0, -1):
    print(number)
```

Output:

```text
5
4
3
2
1
```

---

## 18. Iterating Through a Dictionary

A dictionary stores key-value pairs.

```python
user = {
    "name": "Ali",
    "age": 25,
    "active": True,
}

for key, value in user.items():
    print(key, value)
```

Output:

```text
name Ali
age 25
active True
```

### Common Dictionary Iteration Methods

```python
for key in user:
    print(key)
```

Iterates through keys.

```python
for value in user.values():
    print(value)
```

Iterates through values.

```python
for key, value in user.items():
    print(key, value)
```

Iterates through key-value pairs.

In modern Python, dictionary iteration preserves insertion order.

---

## 19. The `while` Loop

A `while` loop repeats a block while its condition remains true.

```python
count = 0

while count < 5:
    print(count)
    count += 1
```

Output:

```text
0
1
2
3
4
```

### Explanation

1. `count` starts at zero.
2. Python checks whether `count < 5`.
3. If true, it prints the value.
4. `count += 1` increments the value.
5. The condition is checked again.
6. The loop stops when `count` reaches five.

### Avoiding Infinite Loops

Consider this code:

```python
count = 0

while count < 5:
    print(count)
```

The condition remains true because `count` never changes. This creates an infinite loop.

When using `while`, make sure that the loop's state can eventually cause its condition to become false, unless an intentional exit mechanism is provided.

---

## 20. `break`

The `break` statement immediately exits the nearest enclosing loop.

```python
for number in range(10):
    if number == 5:
        break

    print(number)
```

Output:

```text
0
1
2
3
4
```

When `number` reaches five, Python executes `break` and exits the loop. The value five is not printed.

### Practical Use Case

Stop searching when an item is found:

```python
numbers = [10, 20, 30, 40, 50]

for number in numbers:
    if number == 30:
        print("Number found")
        break
```

---

## 21. `continue`

The `continue` statement skips the rest of the current iteration and moves to the next iteration.

```python
for number in range(5):
    if number == 2:
        continue

    print(number)
```

Output:

```text
0
1
3
4
```

When `number` is two, Python skips the `print()` statement for that iteration.

### Comparison

| Statement | Behavior |
|---|---|
| `break` | Exits the loop entirely |
| `continue` | Skips the current iteration |

### Practical Example: Skipping Inactive Users

```python
users = [
    {"name": "Ali", "active": True},
    {"name": "Sara", "active": False},
    {"name": "Reza", "active": True},
]

for user in users:
    if not user["active"]:
        continue

    print(user["name"])
```

Output:

```text
Ali
Reza
```

---

## 22. Nested Loops

A nested loop is a loop inside another loop.

```python
for row in range(3):
    for column in range(2):
        print(row, column)
```

Output:

```text
0 0
0 1
1 0
1 1
2 0
2 1
```

### How Does It Work?

For each value of `row`, the inner loop runs through every value of `column`.

The inner loop completes all its iterations before the outer loop advances to its next value.

### Practical Example: A Small Grid

```python
for row in range(3):
    for column in range(3):
        print("*", end=" ")
    print()
```

Output:

```text
* * *
* * *
* * *
```

The inner loop prints three stars on the same line. The outer loop's `print()` starts a new line after each row.

---

## 23. `enumerate()`

Use `enumerate()` when you need both an item's value and its index while iterating.

```python
students = ["Ali", "Sara", "Reza"]

for index, student in enumerate(students, start=1):
    print(index, student)
```

Output:

```text
1 Ali
2 Sara
3 Reza
```

### Why Use `enumerate()`?

A less direct approach would be to maintain an index manually.

```python
students = ["Ali", "Sara", "Reza"]
index = 1

for student in students:
    print(index, student)
    index += 1
```

`enumerate()` is simpler and reduces the chance of mistakes.

By default, indexing starts at zero. Use `start=1` when you want human-friendly numbering.

---

## 24. `zip()`

Use `zip()` to iterate over corresponding elements from multiple iterables.

```python
students = ["Ali", "Sara", "Reza"]
scores = [85, 92, 78]

for student, score in zip(students, scores):
    print(f"{student}: {score}")
```

Output:

```text
Ali: 85
Sara: 92
Reza: 78
```

Each student's name is paired with the score at the same position.

### Important: Different Lengths

Consider the original example:

```python
students = ["Ali", "Sara", "Reza"]
scores = [85, 92, 78, 56]

for student, score in zip(students, scores):
    print(f"{student}: {score}")
```

Output:

```text
Ali: 85
Sara: 92
Reza: 78
```

The fourth score, `56`, is ignored because `zip()` stops when the shortest iterable is exhausted.

If mismatched lengths indicate a programming error, Python 3.10 and later support `strict=True`:

```python
for student, score in zip(students, scores, strict=True):
    print(f"{student}: {score}")
```

This raises a `ValueError` when the iterables have different lengths.

### When Should You Use `zip()`?

It is useful for pairing student names with scores, product names with prices, or column values from separate lists.

If the data represents related records, consider storing each record together in a dictionary or another suitable data structure rather than relying on separate lists.

---

# Part 4 — Combining Conditions and Loops

## 25. Filtering Users with Conditions

Consider a list of users:

```python
users = [
    {"name": "Ali", "age": 22, "active": True},
    {"name": "Sara", "age": 16, "active": True},
    {"name": "Reza", "age": 30, "active": False},
    {"name": "Mina", "age": 25, "active": True},
]

for user in users:
    if user["age"] >= 18 and user["active"]:
        print(f'{user["name"]}: Eligible')
    else:
        print(f'{user["name"]}: Not eligible')
```

Output:

```text
Ali: Eligible
Sara: Not eligible
Reza: Not eligible
Mina: Eligible
```

A user is eligible only if both conditions are satisfied:

- The user is at least 18 years old.
- The user is active.

This example combines a list, dictionaries, a loop, comparison operators, and a logical operator.

It is a good model for real-world filtering logic.

---

# Part 5 — Hands-on Exercises

## Exercise 1: Age Classification

Ask the user to enter their age.

Requirements:

- If the age is below 13, print `"Child"`.
- If the age is from 13 to 17, print `"Teenager"`.
- If the age is 18 or older, print `"Adult"`.
- Consider how to handle invalid input.

Hint: `input()` returns a string. Convert the input to an integer and handle invalid values with `try / except`.

## Exercise 2: Grade Calculator

Ask the user to enter a score between 0 and 100.

Requirements:

- 90–100: Grade A
- 70–89: Grade B
- 50–69: Grade C
- Below 50: Failed
- Values outside the range 0–100 should be rejected.

Challenge: Make sure that an invalid score does not accidentally receive a grade.

## Exercise 3: Role-Based Access

Create a program with these variables:

```python
username = "Ali"
user_role = "manager"
is_active = True
```

Grant access only if the user is active and has an allowed role.

Allowed roles:

```python
["admin", "manager", "developer"]
```

Use `in` and `and` in your solution.

## Exercise 4: Number Classification

Print the numbers from 1 to 20.

For each number:

- Print `"Even"` if it is divisible by two.
- Print `"Odd"` otherwise.

Challenge: Print the number and its classification on the same line.

## Exercise 5: Sum of Numbers

Calculate the sum of integers from 1 through 100.

Try solving it using:

1. A `for` loop.
2. A `while` loop.
3. Python's built-in `sum()` and `range()`.

Compare the solutions.

## Exercise 6: Find a Number

Given:

```python
numbers = [10, 25, 30, 45, 50]
target = 30
```

Use a loop to find the target.

Requirements:

- Print `"Found"` when the target is found.
- Stop searching using `break`.
- If the target is absent, print `"Not found"`.

Hint: You can use a Boolean flag or a loop's `else` clause.

## Exercise 7: Student Results

Given:

```python
students = [
    {"name": "Ali", "score": 85},
    {"name": "Sara", "score": 45},
    {"name": "Reza", "score": 92},
    {"name": "Mina", "score": 68},
]
```

Print each student's name and whether they passed.

Passing score: 50.

Challenge: Print the number of students who passed and the average score.

## Exercise 8: Pair Students with Scores

Given:

```python
students = ["Ali", "Sara", "Reza"]
scores = [85, 92, 78]
```

Use `zip()` to print each student and score.

Then use `enumerate()` to display each student with a numbered position.

Challenge: What happens when one list has more elements than the other?

## Exercise 9: Command-Line Menu

Create a simple menu that accepts one of these commands:

- `buy`
- `price`
- `help`
- `exit`

Use `match / case` to process the command.

Challenge: Keep asking for commands until the user enters `exit`.

## Exercise 10: Discount Calculator

Ask the user to enter a product price.

Apply the following rules:

- Below 1,000,000: no discount
- From 1,000,000 up to, but not including, 5,000,000: 10% discount
- 5,000,000 or above: 20% discount

Print the discount percentage and final price.

Challenge: Validate the input and reject negative prices.

---

# Key Takeaways

- `if`, `elif`, and `else` control which blocks execute.
- Comparison operators produce Boolean results.
- `and`, `or`, and `not` combine or reverse truth values.
- Python evaluates conditions using truthiness rules.
- The walrus operator (`:=`) combines assignment with an expression.
- `match / case` handles matching values or structured patterns.
- Membership operators check whether values are contained in collections.
- Guard clauses allow functions to return early.
- `for` loops iterate over items; `while` loops repeat while a condition is true.
- `range()` generates integer sequences.
- `break` exits a loop, while `continue` skips an iteration.
- `enumerate()` provides an index and an item.
- `zip()` pairs items from multiple iterables and normally stops at the shortest one.

## Recommended Teaching Order

1. `if`, `else`, and comparison operators
2. `elif` and condition ordering
3. Logical operators and nested conditions
4. Truthy and falsy values
5. Membership operators and ternary expressions
6. Guard clauses and practical decision-making
7. `for` loops and `range()`
8. Iterating through lists and dictionaries
9. `while`, `break`, and `continue`
10. Nested loops
11. `enumerate()` and `zip()`
12. Combined exercises and a small command-line application

**Instructor note:** Focus on helping students predict program behavior before running the code. Ask them to trace each condition and loop iteration manually. This builds the reasoning skills they will need for functions, API request handling, data processing, and backend development.
