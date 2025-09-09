# Advanced Python (Detailed Notes)

# 1. Object-Oriented Programming (OOP)

## Classes & Objects

- **Class:** Blueprint of an object  
- **Object:** Instance of a class  

```python
class Person:
    def __init__(self, name, age):  # constructor
        self.name = name
        self.age = age
    
    def greet(self):
        print(f"Hello, I am {self.name}")

# Create object
p1 = Person("Alice", 25)
p1.greet()  # Hello, I am Alice
```

## Inheritance

**Description:** Reuse parent class  

```python
class Student(Person):
    def __init__(self, name, age, grade):
        super().__init__(name, age)
        self.grade = grade
    
    def show_grade(self):
        print(f"Grade: {self.grade}")

# Create object
s1 = Student("Bob", 20, "A")
s1.greet()      # Hello, I am Bob
s1.show_grade() # Grade: A
```

## Polymorphism

**Description:** Same method works for different objects  

```python
class Dog:
    def speak(self):
        print("Woof!")

class Cat:
    def speak(self):
        print("Meow!")

def animal_speak(animal):
    animal.speak()

animal_speak(Dog())  # Woof!
animal_speak(Cat())  # Meow!
```

## Encapsulation

**Description:** Restrict access to variables  

```python
class Bank:
    def __init__(self, balance):
        self.__balance = balance  # private

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

# Create object
b = Bank(1000)
b.deposit(500)
print(b.get_balance())  # 1500
```


# 2. Modules & Packages

## Module

**Description:** Python file containing functions or classes  

```python
# file: mymodule.py
def add(a, b):
    return a + b
```

```python
# main.py
import mymodule
print(mymodule.add(3,4))  # 7
```

### Packages: **Description:** Folder of modules containing an `__init__.py` file  

**Pip:** Install external libraries  

```bash
pip install requests
```

### Virtual Environment

**Description:** Create isolated Python environment  

```bash
python -m venv myenv

# Activate environment
source myenv/bin/activate  # Linux/Mac
myenv\Scripts\activate     # Windows
```

## CSV Files

```python
import csv

# Write to CSV
with open("data.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Age"])
    writer.writerow(["Alice", 25])

# Read from CSV
with open("data.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

```

## JSON Files

```python
import json

data = {"name": "Bob", "age": 30}

# Write to JSON
with open("data.json", "w") as f:
    json.dump(data, f)

# Read from JSON
with open("data.json", "r") as f:
    data = json.load(f)
    print(data)
```

# 4. Decorators, Generators, Iterators

## Decorators

**Description:** Modify functions without changing their code  

```python
def decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")
    return wrapper

@decorator
def say_hello():
    print("Hello")

say_hello()
```

## Generators

**Description:** Yield values one by one → memory efficient  

```python
def gen_numbers(n):
    for i in range(n):
        yield i

for num in gen_numbers(5):
    print(num)
```

## Iterators

**Description:** Objects you can loop over  

```python
lst = [1, 2, 3]
it = iter(lst)

print(next(it))  # 1
print(next(it))  # 2
```


# 5. Lambda, map, filter, reduce, Comprehension

## Lambda (Anonymous Function)

```python
square = lambda x: x**2
print(square(5))  # 25
```

## `map()` Function

**Description:** Apply a function to all elements of an iterable  

```python
nums = [1, 2, 3]
squares = list(map(lambda x: x**2, nums))  # [1, 4, 9]
```
## `filter()` Function

**Description:** Filter elements based on a condition  

```python
nums = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, nums))  # [2, 4]
```

## `reduce()` Function

**Description:** Reduce a list to a single value (from `functools`)  

```python
from functools import reduce

nums = [1, 2, 3, 4]
sum_all = reduce(lambda x, y: x + y, nums)  # 10
```

## List/Dict/Set Comprehension

```python
# List comprehension
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]

# Dictionary comprehension
d = {x: x**2 for x in range(5)}  # {0:0, 1:1, 2:4, 3:9, 4:16}

# Set comprehension
s = {x for x in range(5) if x % 2 == 0}  # {0, 2, 4}
```

## Why Important

- **OOP:** Structure large projects → backend, game development, AI models.  
- **Modules & Packages:** Code reuse, third-party libraries.  
- **File Handling:** Persist data, read CSV/JSON → real-world apps & AI preprocessing.  
- **Decorators & Generators:** Efficient, modular, memory-friendly code.  
- **Lambda, map/filter/reduce/comprehension:** Functional programming → concise, fast data processing.
```

## ✅ Practice Examples

- Create a class hierarchy: `Person → Student → Teacher`  
- Read a CSV file and calculate average age  
- Write a generator for Fibonacci numbers  
- Use `map` and `filter` to process a list of numbers  
- Create a decorator that times a function execution
```