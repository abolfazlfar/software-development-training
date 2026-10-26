# Episode 3 — Python Variables and Data Types

## Overview

This session introduces Python variables, naming conventions, built-in data types, operators, type conversion, formatted strings, and basic numeric calculations.

Students will learn how Python stores values, how expressions behave with different data types, and how to write readable Python code.

## Learning Objectives

By the end of this session, students will be able to:

- Create variables and assign values.
- Follow Python variable naming conventions.
- Identify common built-in data types.
- Use arithmetic and string operators.
- Understand variable reassignment and assignment behavior.
- Convert values between data types.
- Understand truthy and falsy values.
- Format output using f-strings.
- Calculate averages and format decimal numbers.
- Understand the basic behavior of mutable objects such as `bytearray`.

## 1. Variables and Assignment

A variable is a name that refers to an object in Python. The assignment operator `=` binds a name to a value.

```python
student_name = "Ali"
python_score = 20

print(student_name)
print(python_score)
```

Output:

```text
Ali
20
```

### Explanation

- `student_name` refers to a string object containing `"Ali"`.
- `python_score` refers to an integer object containing `20`.
- `print()` displays the values in the terminal.
- Python does not require variable declarations with explicit types.

### Multiple Assignments

```python
math_score = 18
python_score = 20
english_score = 16
```

Each variable can refer to a different value and type.

## 2. Comparing Values

Comparison operators evaluate a condition and return a Boolean value: `True` or `False`.

```python
python_score = 20

print(python_score == 20)
print(python_score == 18)
```

Output:

```text
True
False
```

### Common Comparison Operators

| Operator | Meaning | Example |
|---|---|---|
| `==` | Equal to | `10 == 10` |
| `!=` | Not equal to | `10 != 5` |
| `>` | Greater than | `10 > 5` |
| `<` | Less than | `5 < 10` |
| `>=` | Greater than or equal to | `10 >= 10` |
| `<=` | Less than or equal to | `5 <= 10` |

**Important:** `=` assigns a value, while `==` compares two values.

## 3. Variable Reassignment

Consider the following code:

```python
x = 10
y = x
x = 20

print(x)
print(y)
```

Output:

```text
20
10
```

### Why?

1. `x = 10` binds the name `x` to the integer `10`.
2. `y = x` binds `y` to the same integer object.
3. `x = 20` reassigns `x` to the integer `20`.
4. `y` still refers to `10`.

Reassigning `x` does not automatically change `y`.

This is an important first step toward understanding Python's object model and references.

## 4. Variable Naming Conventions

Python variable names must follow specific rules.

### Valid Variable Names

```python
student_score = 20
student_name = "Ali"
score2 = 18
_private_value = 10
```

### Invalid Variable Names

```python
# student score = 20
# 2thstudent = 20
# class = 10
```

Why are these invalid?

- `student score`: Contains a space.
- `2thstudent`: Starts with a digit.
- `class`: Uses a reserved Python keyword.

### Common Naming Styles

| Style | Example | Typical use |
|---|---|---|
| `snake_case` | `student_score` | Python variables and functions |
| `PascalCase` | `StudentRecord` | Class names |
| `camelCase` | `studentScore` | Common in JavaScript |
| `SCREAMING_SNAKE_CASE` | `MAX_SCORE` | Constants by convention |
| `kebab-case` | `student-score` | File or URL naming, not Python identifiers |

Python conventionally uses `snake_case` for variables and functions.

### Multiple Statements

```python
score = 10
print(score)
```

You may also write:

```python
score = 10; print(score)
```

However, separate lines are generally preferred for readability.

## 5. Built-in Data Types

Python provides several built-in types for representing different kinds of data.

```python
student_name = "Ali"
math_score = 18
average_score = 18.5
has_passed = True
scores = [18, 20, 16]
final_grade = None

print(type(student_name))
print(type(math_score))
print(type(average_score))
print(type(has_passed))
print(type(scores))
print(type(final_grade))
```

Output:

```text
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
<class 'list'>
<class 'NoneType'>
```

### Common Data Types

| Type | Description | Example |
|---|---|---|
| `str` | Text | `"Ali"` |
| `int` | Integer | `20` |
| `float` | Floating-point number | `18.5` |
| `bool` | Boolean value | `True` |
| `list` | Ordered, mutable collection | `[18, 20, 16]` |
| `tuple` | Ordered, immutable collection | `(18, 20, 16)` |
| `dict` | Key-value collection | `{"math": 18}` |
| `set` | Collection of unique elements | `{18, 20, 16}` |
| `NoneType` | Represents the absence of a value | `None` |

### Checking a Variable's Type

Use `type()` to inspect an object's type:

```python
score = 18
print(type(score))
```

Use `isinstance()` when checking whether an object belongs to a particular type:

```python
score = 18

print(isinstance(score, int))
```

Output:

```text
True
```

## 6. Arithmetic Operators

Python supports several arithmetic operators.

```python
print(10 / 3)
print(10 // 3)
print(10 % 3)
print(2 ** 3)
```

Output:

```text
3.3333333333333335
3
1
8
```

### Operator Explanation

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `/` | Division | `10 / 3` | `3.333...` |
| `//` | Floor division | `10 // 3` | `3` |
| `%` | Modulo (remainder) | `10 % 3` | `1` |
| `**` | Exponentiation | `2 ** 3` | `8` |
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `10 * 5` | `50` |

Floor division rounds the quotient down toward negative infinity, rather than simply removing the decimal portion.

For example:

```python
print(-10 // 3)
```

Output:

```text
-4
```

## 7. Working with Strings

Strings represent text and can be combined using the `+` operator.

```python
first_name = "Ali"
last_name = "Ahmadi"

full_name = first_name + " " + last_name

print(full_name)
```

Output:

```text
Ali Ahmadi
```

### String Repetition

```python
score = "18"

print(score + score)
print(score * 3)
```

Output:

```text
1818
181818
```

The `+` operator concatenates strings, and `*` repeats a string when multiplied by an integer.

But what happens here?

```python
score = "18"

# print(score + 2)
```

This raises a `TypeError` because Python does not automatically combine a string and an integer using `+`.

Convert the value first if arithmetic is intended:

```python
score = "18"

print(int(score) + 2)
```

Output:

```text
20
```

## 8. Type Conversion

Type conversion changes a value from one type to another when the conversion is valid.

```python
score_text = "18"
score = int(score_text)

price = float("125.5")
student_name = str(123)
is_active = bool(-123.5)

print(score, type(score))
print(price, type(price))
print(student_name, type(student_name))
print(is_active, type(is_active))
```

Output:

```text
18 <class 'int'>
125.5 <class 'float'>
123 <class 'str'>
True <class 'bool'>
```

### Common Conversion Functions

| Function | Purpose | Example |
|---|---|---|
| `int()` | Convert to integer | `int("18")` |
| `float()` | Convert to float | `float("12.5")` |
| `str()` | Convert to string | `str(123)` |
| `bool()` | Convert to Boolean | `bool(1)` |
| `list()` | Create a list | `list("abc")` |
| `tuple()` | Create a tuple | `tuple([1, 2])` |
| `set()` | Create a set | `set([1, 1, 2])` |

### Invalid Conversion

```python
score = int("eighteen")
```

This raises a `ValueError` because `"eighteen"` is not a valid integer representation.

A safer approach is to handle invalid input:

```python
score_text = input("Enter your score: ")

try:
    score = int(score_text)
    print(f"Your score is {score}")
except ValueError:
    print("Please enter a valid integer.")
```

## 9. Truthy and Falsy Values

Python values can be evaluated in a Boolean context.

```python
print(bool(0))
print(bool(1))
print(bool(""))
print(bool("False"))
```

Output:

```text
False
True
False
True
```

### Why is `bool("False")` True?

A non-empty string is truthy, even if its contents are the word `"False"`.

Common falsy values include:

- `False`
- `None`
- `0`
- `0.0`
- `""`
- `[]`
- `{}`
- `set()`

Most other values are truthy.

Example:

```python
student_name = ""

if student_name:
    print("Name provided")
else:
    print("Name is empty")
```

Output:

```text
Name is empty
```

## 10. Formatted Strings (f-strings)

f-strings provide a convenient way to insert variables and expressions into strings.

```python
student_name = "Ali"
average_score = 18.567

print(f"Student: {student_name}")
print(f"Average: {average_score:.2f}")
```

Output:

```text
Student: Ali
Average: 18.57
```

### Explanation

- `f` before the string enables expression interpolation.
- `{student_name}` inserts the variable's value.
- `{average_score:.2f}` formats the number with two digits after the decimal point.

Compare with ordinary string concatenation:

```python
print("Student: " + student_name)
print("Average:", average_score)
```

f-strings are generally easier to read when combining text and values.

## 11. Floating-Point Calculations

Let's calculate a student's average score.

```python
student_name = "Ali"
math_score = 18
python_score = 20
english_score = 16

average = (
    math_score + python_score + english_score
) / 3

print(f"Student: {student_name}")
print(f"Average: {average:.2f}")
```

Output:

```text
Student: Ali
Average: 18.00
```

### Why use `:.2f`?

It displays the number with two digits after the decimal point.

For example:

```python
average = 18.567

print(f"{average:.2f}")
```

Output:

```text
18.57
```

This changes the displayed formatting, not the original value stored in `average`.

**Important:** Floating-point arithmetic can introduce small precision errors. For financial calculations, consider using `decimal.Decimal` when exact decimal arithmetic is required.

## 12. Mutable Objects: bytearray

Python has mutable and immutable objects.

A `bytearray` is a mutable sequence of integers in the range 0–255.

```python
x = bytearray(b"1")

x[0] = 123

print(x)
print(x.decode())
```

Output:

```text
bytearray(b'{')
{
```

### Explanation

- `b"1"` represents a byte string.
- `bytearray()` creates a mutable byte sequence.
- `x[0] = 123` changes the first byte.
- The byte value `123` represents the character `{` in ASCII.
- `.decode()` converts the byte sequence into a string using the default UTF-8 encoding.

This example introduces mutability: the object can be changed without creating a new bytearray.

## 13. Hands-on Exercise

### Objective

Build a simple student score calculator using variables, data types, arithmetic, type conversion, and f-strings.

### Tasks

1. Create a file named `student_calculator.py`.
2. Define a student's name.
3. Store math, Python, and English scores in separate variables.
4. Calculate the total score.
5. Calculate the average score.
6. Determine whether the student passed based on an average of at least 10.
7. Print the student's name, total, average, and pass status using f-strings.
8. Display the average with two decimal places.
9. Ask the user to enter a score and convert the input into an integer.
10. Handle invalid input using `try` and `except`.

### Example Output

```text
Student: Ali
Total Score: 54
Average Score: 18.00
Passed: True
```

### Challenge

Create a small program that asks for:

- Student name
- Math score
- Python score
- English score

Validate the scores, calculate the average, and print a formatted report.

## 14. Important Notes

- Variables are names bound to objects.
- `=` assigns a value; `==` compares values.
- Python variable names cannot contain spaces or begin with digits.
- Python is dynamically typed.
- `type()` helps inspect an object's type.
- `int()`, `float()`, `str()`, and `bool()` perform type conversions.
- Invalid conversions can raise exceptions.
- Non-empty strings are truthy, including `"False"`.
- f-strings simplify formatted output.
- `:.2f` displays two decimal places.
- Lists and bytearrays are mutable; strings, integers, and tuples are immutable.

## Summary

In this session, students learned how to assign values, name variables, identify data types, use operators, convert values, evaluate truthiness, format strings, and perform basic calculations.

These concepts form the foundation for upcoming sessions on collections, conditions, loops, functions, and more advanced Python programming.