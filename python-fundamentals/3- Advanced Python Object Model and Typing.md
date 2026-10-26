# Episode 4 — Advanced Python: Dynamic Typing, Type Hints, Object Identity, and Copying

## Overview

In this optional advanced episode, we explore how Python handles types, objects, variables, and memory references.

The goal is to understand not only how to write Python code, but also why certain expressions behave differently from what we might expect.

By the end of this episode, you should understand:

- Dynamic typing and type safety
- Type hints and static type checkers
- The difference between object identity and equality
- The `id()` function and the `is` operator
- Mutable and immutable objects
- References and assignment behavior
- Shallow copies and deep copies

## Learning Objectives

After completing this episode, you should be able to:

1. Explain how a Python variable can refer to objects of different types.
2. Recognize type-related errors at runtime.
3. Add type hints to variables and collections.
4. Understand the difference between `==` and `is`.
5. Explain how multiple variables can reference the same object.
6. Distinguish mutable objects from immutable objects.
7. Predict how modifying a list affects other references to that list.
8. Use shallow and deep copying appropriately.

---

## 1. Dynamic Typing

Python is a dynamically typed language.

This means that a variable does not have a permanently fixed type. Instead, a variable name can refer to objects of different types during program execution.

### Example

```python
value = 10
print(type(value))

value = "Hello"
print(type(value))

value = [1, 2, 3]
print(type(value))
```

Output:

```text
<class 'int'>
<class 'str'>
<class 'list'>
```

### Explanation

Initially, `value` refers to an integer object.

```python
value = 10
```

Then, it refers to a string object.

```python
value = "Hello"
```

Finally, it refers to a list object.

```python
value = [1, 2, 3]
```

The variable name is the same, but the objects it refers to have different types.

**Important:** Python is dynamically typed, but values still have types. Dynamic typing does not mean that Python ignores types.

### Teaching Question

What will happen here?

```python
value = 100
value = "Python"
value = True

print(value)
print(type(value))
```

Expected output:

```text
True
<class 'bool'>
```

---

## 2. Type Safety and Runtime Errors

Dynamic typing does not mean that every operation is valid.

Python checks whether an operation is supported when the code executes.

### Example

```python
score = "Excellent"
print(score + 10)
```

This raises a `TypeError` because Python cannot concatenate a string and an integer using the `+` operator.

Typical error:

```text
TypeError: can only concatenate str (not "int") to str
```

The exact error wording can vary by Python version.

### How Can We Fix It?

The correct solution depends on what the program is supposed to do.

**Option 1: Convert the string to a number**

```python
score = "10"
print(int(score) + 10)
```

Output:

```text
20
```

**Option 2: Convert the number to a string**

```python
score = "Excellent"
print(score + " 10")
```

Output:

```text
Excellent 10
```

These solutions produce different results because they represent different intentions.

### Teaching Point

Type safety is a broad concept related to preventing invalid operations and incompatible values. Python permits many types of operations to be attempted at runtime, but invalid operations can raise exceptions.

Python's dynamic typing does not mean every expression is valid.

---

## 3. Type Hints

Type hints allow developers to indicate the expected types of variables, function parameters, and return values.

They improve readability, documentation, editor support, and static analysis.

### Example

```python
student_name: str = "Ali"
math_score: int = 18
average_score: float = 18.5
scores: list[int] = [18, 20, 16]
```

Explanation:

| Type hint | Meaning |
|---|---|
| `str` | String |
| `int` | Integer |
| `float` | Floating-point number |
| `list[int]` | List whose elements are intended to be integers |

The annotation `list[int]` is supported in Python 3.9 and later. Older Python versions commonly use `List[int]` from `typing`.

### Type Hints for Functions

```python
def calculate_average(scores: list[int]) -> float:
    return sum(scores) / len(scores)


student_scores = [18, 20, 16]

average = calculate_average(student_scores)

print(average)
```

Output:

```text
18.0
```

Here:

- `scores: list[int]` indicates that `scores` is expected to be a list of integers.
- `-> float` indicates that the function is expected to return a floating-point number.

**Important:** Type hints are not normally enforced automatically by the Python runtime. They primarily support static analysis and development tools.

---

## 4. Type Hints Do Not Automatically Enforce Types

Consider the following code:

```python
score: int = "Excellent"

print(score)
```

The annotation says that `score` is expected to be an integer, but the assigned value is a string.

When this code runs in ordinary Python, it prints:

```text
Excellent
```

Python does not automatically reject the assignment because of the annotation.

However, a static type checker can identify the mismatch.

### Static Type Checkers

Two commonly used tools are:

- **mypy**
- **Pyright**

For example, install mypy:

```bash
python -m pip install mypy
```

Save the following code in `type_checking.py`:

```python
score: int = "Excellent"

print(score)
```

Run:

```bash
mypy type_checking.py
```

The checker should report an incompatible assignment.

You can also use Pyright through your editor or command-line setup.

### Why Is This Useful?

Imagine a large application with hundreds of functions. Type hints and static analysis can help detect mistakes before the application runs.

For example:

```python
def add_scores(first: int, second: int) -> int:
    return first + second


result = add_scores(10, "20")
```

Ordinary Python may raise a `TypeError` when the function executes. A static type checker can identify the incompatible argument before runtime.

### Teaching Question

Will this code fail because of the annotation?

```python
age: int = "25"
print(age)
```

**Answer:** Not in ordinary Python solely because of the annotation. It prints `25` as a string. A static type checker should report the mismatch.

---

## 5. The `id()` Function

The built-in `id()` function returns an integer that identifies an object during its lifetime.

In CPython, this value is commonly related to the object's memory address, but Python does not guarantee that interpretation for every implementation.

### Example

```python
x = 5
y = x

print(x)
print(y)

print(id(x))
print(id(y))
```

Both variables refer to the integer object representing `5` in this example. Therefore, their IDs will be equal.

The actual numeric ID is implementation-dependent.

### Reassignment

```python
x = 5
y = x

x = 5.0

print(x)
print(y)

print(type(x))
print(type(y))
```

Output:

```text
5.0
5
<class 'float'>
<class 'int'>
```

Reassigning `x` does not change the object that `y` refers to.

After the reassignment, `x` refers to a float object, while `y` still refers to the integer object.

**Key idea:** Assignment binds a name to an object. Reassigning one name does not automatically reassign another name.

---

## 6. Equality (`==`) vs. Identity (`is`)

These operators answer two different questions.

| Operator | Meaning |
|---|---|
| `==` | Do these objects compare as equal? |
| `is` | Are these references pointing to the exact same object? |

### Example 1: Equal Values, Different Objects

```python
a = [10, 20]
b = [10, 20]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

Explanation:

- `a == b` is `True` because both lists contain the same values.
- `a is b` is `False` because they are two separate list objects.

### Example 2: Two Names, One Object

```python
a = [10, 20]
c = a

print(a == c)
print(a is c)
```

Output:

```text
True
True
```

Both names refer to the same list object.

### Example 3: Comparing Numbers

```python
a = 1000
b = 1000

print(a == b)
print(a is b)
```

The equality comparison is `True`.

Do not rely on the identity comparison being `True` or `False` for integer values like these. Python implementations may reuse or optimize objects in implementation-dependent ways.

**Rule:** Use `==` for value comparisons. Use `is` when you need to test whether two references identify the same object.

### The Standard Use Case for `is`

```python
result = None

if result is None:
    print("Result is None")
```

Output:

```text
Result is None
```

Use `is None` to check whether a value is the singleton `None` object.

Although `result == None` can work for ordinary values, `result is None` is the recommended and conventional approach.

---

## 7. Mutable vs. Immutable Objects

An object's mutability determines whether its contents or state can be changed after the object has been created.

### Common Immutable Types

- `int`
- `float`
- `bool`
- `str`
- `tuple` (the tuple structure itself is immutable)

### Common Mutable Types

- `list`
- `dict`
- `set`
- `bytearray`

A tuple can contain a mutable object, such as a list. The tuple's references cannot be reassigned, but the contained list can still be modified.

### Example 1: Mutable List

```python
scores = [18, 20, 16]
another_scores = scores

scores.append(19)

print(scores)
print(another_scores)
```

Output:

```text
[18, 20, 16, 19]
[18, 20, 16, 19]
```

Both names refer to the same list object. Modifying that object is visible through both names.

### Example 2: Immutable String

```python
name = "Ali"
another_name = name

name = name + " Ahmadi"

print(name)
print(another_name)
```

Output:

```text
Ali Ahmadi
Ali
```

Strings are immutable. The expression `name + " Ahmadi"` creates a new string value, and the name `name` is rebound to it.

The variable `another_name` continues to refer to the original string.

**Important:** Immutability does not mean a variable cannot be reassigned. It means the existing object itself cannot be changed in place.

---

## 8. List Assignment: `+` vs. `append()`

Consider these two examples.

### Example 1: Using `+`

```python
a = [1, 2, 3]
b = a

b = b + [4]

print(a)
print(b)
print(a is b)
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
False
```

The expression `b + [4]` creates a new list. Assigning the result to `b` makes `b` refer to that new list.

The original list referenced by `a` remains unchanged.

### Example 2: Using `append()`

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
print(b)
print(a is b)
```

Output:

```text
[1, 2, 3, 4]
[1, 2, 3, 4]
True
```

The `append()` method modifies the existing list. Because `a` and `b` reference the same object, both names observe the change.

### Comparison

| Operation | Creates a new list? | Modifies the existing list? |
|---|---|---|
| `b = b + [4]` | Yes | No |
| `b.append(4)` | No | Yes |

This distinction is especially important when working with lists, dictionaries, and other mutable objects.

---

## 9. Shallow Copy

A shallow copy creates a new outer collection, but it does not recursively copy nested objects.

### Example

```python
original = [1, 2, 3]
copied = original.copy()

copied.append(4)

print(original)
print(copied)
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

The lists are separate objects.

```python
print(original is copied)
```

Output:

```text
False
```

Because the list contains immutable integers, this example is straightforward: appending to the copied list does not affect the original.

However, shallow copying becomes more interesting when a collection contains other mutable objects.

### Nested List Example

```python
original = [[1, 2], [3, 4]]
copied = original.copy()

copied[0].append(99)

print(original)
print(copied)
```

Output:

```text
[[1, 2, 99], [3, 4]]
[[1, 2, 99], [3, 4]]
```

Why did modifying `copied` affect `original`?

The outer lists are different objects, but their corresponding inner lists are shared.

Conceptually:

```text
original ──> outer list ──> inner list [1, 2]
                              ↑
copied   ──> outer list ──────┘
```

Both outer lists reference the same first inner list.

---

## 10. Deep Copy

A deep copy recursively copies nested objects, creating independent copies of the nested mutable structures in the copied object graph.

Python provides the `copy` module for this purpose.

### Example

```python
import copy

original = [[1, 2], [3, 4]]
copied = copy.deepcopy(original)

copied[0].append(99)

print(original)
print(copied)
```

Output:

```text
[[1, 2], [3, 4]]
[[1, 2, 99], [3, 4]]
```

Now the original nested list remains unchanged.

### Shallow Copy vs. Deep Copy

| Feature | Shallow copy | Deep copy |
|---|---|---|
| Creates a new outer collection | Yes | Yes |
| Recursively copies nested objects | No | Yes, generally |
| Shares nested mutable objects | Often | Generally avoids sharing copied nested objects |
| Typical approach | `original.copy()` | `copy.deepcopy(original)` |

Deep copying has limitations: some objects cannot be copied, and custom classes may define their own copying behavior. It can also be more expensive in time and memory.

Use the type of copy that matches your application's requirements.

---

## 11. Putting It All Together

Review the following example and predict the output before running it.

```python
first = [[10, 20], [30, 40]]
second = first.copy()
third = first

second[0].append(99)
third.append([50, 60])

print(first)
print(second)
print(third)

print(first is second)
print(first is third)
```

### Expected Output

```text
[[10, 20, 99], [30, 40], [50, 60]]
[[10, 20, 99], [30, 40]]
[[10, 20, 99], [30, 40], [50, 60]]
False
True
```

### Explanation

1. `first.copy()` creates a new outer list, so `first is second` is `False`.
2. The inner lists are shared, so appending `99` through `second` also changes what `first` sees.
3. `third = first` makes both names refer to the same outer list.
4. Appending through `third` therefore changes the outer list seen through `first`.

---

## 12. Hands-on Exercises

### Exercise 1: Dynamic Typing

Predict the output:

```python
value = 10
value = "10"
value = float(value)

print(value)
print(type(value))
```

### Exercise 2: Type Hints

Identify the type mismatch:

```python
student_name: str = "Sara"
student_age: int = "21"
scores: list[int] = [18, 20, "19"]
```

Correct the code so that the annotations and values are consistent.

### Exercise 3: Identity and Equality

Predict the output:

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)
print(a is b)
print(a is c)
```

Explain each result.

### Exercise 4: Mutability

Predict the output:

```python
a = [10, 20]
b = a

b.append(30)
a = [40, 50]

print(a)
print(b)
```

Explain why changing `a` in the final assignment does not replace the list referenced by `b`.

### Exercise 5: Shallow Copy

Predict the output:

```python
original = [[1, 2], [3, 4]]
copied = original.copy()

copied.append([5, 6])
copied[1].append(99)

print(original)
print(copied)
```

Which changes affect the original, and why?

### Exercise 6: Deep Copy

Modify Exercise 5 to use `copy.deepcopy()` and verify how the output changes.

### Exercise 7: Debugging with Type Hints

Create a function that calculates a student's average score.

Requirements:

- Accept a list of integer scores.
- Return a floating-point average.
- Add appropriate type hints.
- Run a static type checker against your code.
- Handle the case where the list is empty.

---

## 13. Key Takeaways

- Python uses dynamic typing: a name can be rebound to objects of different types.
- Type hints communicate expected types but are not automatically enforced by ordinary Python execution.
- Static type checkers such as mypy and Pyright can detect many type mismatches before runtime.
- `==` compares values; `is` compares object identity.
- Use `is None` for checking whether a value is `None`.
- Assignment does not copy an object. It binds a name to an object.
- Lists, dictionaries, and sets are mutable; integers, floats, booleans, strings, and tuple structures are immutable.
- `append()` modifies an existing list, while `list + [...]` creates a new list.
- A shallow copy creates a new outer collection but can share nested objects.
- A deep copy recursively copies nested structures where supported.

## Recommended Teaching Order

1. Dynamic typing and `type()`
2. Runtime type errors
3. Type hints and static type checking
4. `id()`, equality, and identity
5. Mutable vs. immutable objects
6. Assignment and shared references
7. Shallow copy
8. Deep copy
9. Exercises and debugging discussion

**Instructor note:** This is an optional advanced episode. Spend the most time on `==` versus `is`, assignment versus copying, and shallow versus deep copy. These concepts explain many bugs that students encounter later when building real applications.
