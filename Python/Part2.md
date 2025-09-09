# Data Structures in Python

## 1. Lists

**Definition:** Ordered, mutable collection of elements. Can store any data type.

**Syntax:**  

```python
lst = [1, 2, 3, "Python", True]
```
## Important Methods

## `append()` Method

**Description:** Add an item at the end of the list  

```python
lst.append(4)  # [1, 2, 3, "Python", True, 4]
```

## `pop()` Method

**Description:** Remove and return element at index (default is last)  

```python
lst.pop()      # removes 4
lst.pop(1)     # removes 2
```
## `insert()` Method

**Description:** Insert a value at a specific index  

```python
lst.insert(1, "New")  # [1, "New", 3, "Python", True]
```

## `remove()` Method

**Description:** Removes the first occurrence of a value  

```python
lst.remove("Python")
```

## `sort()` Method

**Description:** Sorts elements in ascending order (works for numbers or strings)  

```python
nums = [3, 1, 2]
nums.sort()  # [1, 2, 3]
```
## `reverse()` Method

**Description:** Reverses the elements of the list  

```python
lst.reverse()
```

## Slicing

```python
lst = [0, 1, 2, 3, 4, 5]

lst[1:4]   # [1, 2, 3] → start to end-1
lst[:3]    # [0, 1, 2] → from start
lst[2:]    # [2, 3, 4, 5] → till end
lst[::2]   # [0, 2, 4] → step
lst[::-1]  # [5, 4, 3, 2, 1, 0] → reverse
```
## List Comprehension

**Description:** Create lists in a single line  

```python
squares = [x**2 for x in range(5)]            # [0, 1, 4, 9, 16]
even_nums = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```

## 2. Tuples

**Definition:** Ordered, immutable collection  

**Syntax:**  

```python
tup = (1, 2, 3, "Python")
single = (5,)  # single element tuple
```

## Key Points for Tuples

- **Immutable:** Cannot add, remove, or change elements  
- **Access by index:** `tup[0]`  

**Unpacking:**  

```python
a, b, c = (10, 20, 30)
print(a)  # 10
```

- Methods: count(), index()

- Use Cases: Fixed data storage, dictionary keys, function returns

## 3. Dictionaries

**Definition:** Unordered collection of key-value pairs. Keys must be unique and immutable.  

**Syntax:**  

```python
d = {"name": "Alice", "age": 25}
```

## Important Dictionary Methods

**`get(key, default)`** → Safe way to access a value  

```python
d.get("name")        # "Alice"
d.get("gender", "NA")  # "NA"
```

## More Dictionary Methods

**`update({key: value})`** → Add or update key-value pairs  

```python
d.update({"age": 26, "city": "Delhi"})

keys(), values(), items() → Returns iterable of keys, values, or key-value pairs

pop(key) → Remove a key and return its value
```

## Example

```python
for key, value in d.items():
    print(f"{key} → {value}")
```

## 4. Sets

**Definition:** Unordered collection of unique elements  

**Syntax:**  

```python
s = {1, 2, 3, 3, 4}  # {1, 2, 3, 4} → duplicates removed
```

## Important Set Methods

- **`add(value)`** → Add an element  
- **`remove(value)`** → Remove element, raises error if not found  
- **`discard(value)`** → Remove element, no error if not found  

## Set Operations

```python
a = {1,2,3}
b = {2,3,4}
a.union(b)        # {1,2,3,4}
a.intersection(b) # {2,3}
a.difference(b)   # {1}
a.symmetric_difference(b) # {1,4}

# Use Cases: Removing duplicates, membership testing, DSA set problems.
```

## 5. Strings

**Definition:** Immutable sequence of characters  

**Syntax:**  

```python
s = "Hello Python"
```

## String Slicing

```python
s = "Hello Python"

s[0:5]   # "Hello"
s[:5]    # "Hello"
s[6:]    # "Python"
s[::2]   # "HloPto"
s[::-1]  # "nohtyP olleH"
```

## Common String Methods

- **`upper()`**, **`lower()`**, **`title()`** → Change case  
- **`strip()`** → Remove leading/trailing spaces  
- **`replace("old", "new")`** → Replace substring  
- **`split()`** → Returns list of words  
- **`join(iterable)`** → Joins elements into a string  
- **`find("x")`** → Index of substring  
- **`count("x")`** → Number of occurrences

## String Formatting

```python
name = "Alice"
age = 25

# Using f-string
print(f"{name} is {age} years old")

# Using format() method
print("{} is {}".format(name, age))
```

- Use Cases: Text processing, user input, AI preprocessing (NLP).

## Why Important

- **Lists & Tuples:** Store sequences → used in algorithms, loops, and AI feature lists.  
- **Dictionaries:** Store key-value structured data → backend, JSON, API handling.  
- **Sets:** Handle unique elements → quick lookups, DSA problems.  
- **Strings:** Text data → input/output, parsing, AI preprocessing (NLP, ML).


## ✅ Practice Examples

1. Create a list of squares using list comprehension.  
2. Unpack a tuple into variables.  
3. Create a dictionary with student names and grades, update and retrieve.  
4. Use sets to remove duplicates from a list.  
5. Slice a string to reverse it and format a sentence with f-string.
