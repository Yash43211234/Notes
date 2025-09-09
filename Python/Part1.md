# 1. Syntax, Indentation, Comments

## Python Syntax

- Python is **case-sensitive**: `Var` ≠ `var`.
- Statements end with a **newline**, not `;`.
- Code blocks are defined by **indentation**, not braces `{}`.

```python
# Correct indentation
if True:
    print("Hello Python")

# Wrong indentation → Error
if True:
print("Hello")  # IndentationError
```

### Comments

#### Single-line comment:

```python
            # This is a comment
```

### Multi-line comment: Triple quotes """ or '''

```python
         """
        This is a multi-line
        comment in Python
        """

 ```

 ## 2. Variables, Data Types, Type Casting

**Variables:** Store data values. No need to declare type explicitly.

```python
x = 10        # int
name = "John" # string
pi = 3.14     # float
```
## Data Types

**Numbers:** `int`, `float`, `complex`

```python
a = 10        # int
b = 3.5       # float
c = 2 + 3j    # complex

```
## Text (String)

**Type:** `str`

```python
s = "Python"
```

## Boolean

**Type:** `bool` (`True` / `False`)

```python
flag = True
```
## Sequence

**Types:** `list`, `tuple`, `range`

```python
lst = [1, 2, 3]
tup = (1, 2, 3)
r = range(5)  # 0, 1, 2, 3, 4
```

## Set

**Types:** `set`, `frozenset` (unique items, unordered)

```python
s = {1, 2, 3}
```

## Mapping

**Type:** `dict` (key-value pairs)

```python
d = {"name": "Alice", "age": 25}
```

## None Type

**Type:** `None`

```python
x = None
```

## Type Casting / Conversion

```python
x = int(3.9)      # 3
y = float(5)      # 5.0
z = str(10)       # "10"
is_true = bool(1) # True
```

## 3. Operators

**Arithmetic Operators:** `+`, `-`, `*`, `/`, `%`, `//`, `**`

```python
7 + 2   # 9
7 - 2   # 5
7 * 2   # 14
7 / 2   # 3.5 (float)
7 // 2  # 3 (floor division)
7 % 2   # 1 (remainder)
2 ** 3  # 8 (exponent)
```
## Comparison Operators

**Operators:** `==`, `!=`, `>`, `<`, `>=`, `<=`

```python
5 == 5   # True
5 != 3   # True
5 > 3    # True
```
## Logical Operators

**Operators:** `and`, `or`, `not`

```python
True and False  # False
True or False   # True
not True        # False
```
## Assignment Operators

**Operators:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`  

```python
x = 5
x += 2   # x = 7
x *= 3   # x = 21
```
## Membership Operators

**Operators:** `in`, `not in`  

```python
"a" in "apple"    # True
4 not in [1, 2, 3] # True
```

## Identity Operators

**Operators:** `is`, `is not`  

```python
a = [1, 2]
b = a
c = [1, 2]

a is b  # True
a is c  # False
```

## 4. Input/Output

**Input from user:** `input()` always returns a string  

```python
name = input("Enter your name: ")
age = int(input("Enter your age: "))  # Convert to int
```
## Output to Screen

**Function:** `print()`

```python
print("Hello", name)
print(f"You are {age} years old")  # f-string formatting
print("Sum:", 5 + 3)
```

## 5. Conditional Statements

**If-Else**

```python
age = int(input("Enter age: "))

if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")
```
## Nested If

```python
num = 10

if num > 0:
    if num % 2 == 0:
        print("Positive even")
```

## Tips: Using Logical Operators for Complex Conditions

```python
if age >= 18 and age <= 60:
    print("Working age")
```

## 6. Loops

**For Loop:** Iterate over sequences  

```python
for i in range(5):  # 0 to 4
    print(i)

for ch in "Python":
    print(ch)
```

## While Loop

**While Loop:** Execute while condition is true  

```python
i = 0
while i < 5:
    print(i)
    i += 1
```
## Break & Continue

```python
# Break example
for i in range(5):
    if i == 3:
        break     # stops loop
    print(i)

# Continue example
for i in range(5):
    if i == 3:
        continue  # skips this iteration
    print(i)
```

## Else with Loops

**Executes if loop completes normally**  

```python
for i in range(3):
    print(i)
else:
    print("Loop finished")
```
## 7. Functions

**Defining Functions**  

```python
def greet(name):
    return f"Hello {name}"

print(greet("Alice"))
```
## Parameters & Arguments

```python
def add(a, b=5):  # default parameter
    return a + b

print(add(3))       # 8
print(add(3, 2))    # 5
```
## Arbitrary Arguments

```python
def sum_all(*args):  # tuple of arguments
    return sum(args)

print(sum_all(1, 2, 3, 4))  # 10

```
## Keyword Arguments

```python
def info(name, age):
    print(f"{name} is {age} years old")

info(age=25, name="Bob")  # order doesn't matter
```
## Recursion

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n-1)

print(factorial(5))  # 120
```
## 8. Exception Handling

**Try-Except-Finally**  

```python
try:
    num = int(input("Enter number: "))
    print(10 / num)
except ValueError:
    print("Invalid input, enter a number!")
except ZeroDivisionError:
    print("Cannot divide by zero!")
finally:
    print("Execution completed")
```
## Raise Custom Exception

```python
x = -5
if x < 0:
    raise ValueError("x cannot be negative")
```

## ✅ Practice Examples

1. Create a calculator using `if-elif-else`.  
2. Find factorial using recursion.  
3. Print all even numbers using a loop.  
4. Handle user input errors using `try-except`.  
5. Write a function to check if a number is prime.
