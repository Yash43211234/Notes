# 📘 Redis – Step 2: Data Structures

Redis does not only store simple strings.  
It supports different types of data structures that make it very powerful.  

---

## 🔹 1. Strings  
- Most basic data type in Redis.  
- Stores a simple **key → value**.  
- Value can be:  
  - Text  
  - Number  
  - Binary (image, JSON, etc.)  

**Example:**  
```bash
set user "Yashwant"
get user
```
- 👉 Output: "Yashwant"

- 👉 Numbers:

```bash
set count 10
incr count   # count = 11
decr count   # count = 10
```

## 🔹 2. Lists  
- An **ordered collection of strings**.  
- Works like **Queue (FIFO)** or **Stack (LIFO)**.  
- You can push values at **left** or **right**, and pop them.  

---

### 👉 Example  
```bash
lpush mylist "A"     # push A to left
rpush mylist "B"     # push B to right
lpush mylist "C"     # push C to left
lrange mylist 0 -1   # view all elements
```

- Output:

```bash 
"C" "A" "B"
```

- 👉 Pop Example:
```bash
lpop tasks   # removes from left → "task2"
rpop tasks   # removes from right → "task3"
```

## 🔹 3. Sets

- A collection of unique values (no duplicates).
- Order is not guaranteed.
- Useful for things like tags, followers list.

- 👉 Example:

```bash 
sadd tags "redis"
sadd tags "database"
sadd tags "redis"   # duplicate, won’t be added
smembers tags
```

- Output:

```bash
["redis", "database"]
```

- 👉 Check membership:
```bash

sismember tags "redis"   # returns 1 (true)
sismember tags "sql"     # returns 0 (false)

```

## 🔹 4. Sorted Sets (ZSETs)  
- Like **sets** but each value has a **score**.  
- Automatically keeps items in **sorted order**.  
- Very useful for **leaderboards** or **ranking systems**.  

---

### 👉 Example (Game Scores)  
```bash
zadd gamescore 100 "Alice"
zadd gamescore 200 "Bob"
zadd gamescore 150 "Charlie"

zrange gamescore 0 -1 withscores   # ascending order
zrevrange gamescore 0 -1 withscores  # descending order

```

Output (zrevrange):

1) "Bob"      200  
2) "Charlie"  150  
3) "Alice"    100  

## 🔹 5. Hashes

A map of fields and values inside a single Redis key.  

Like a mini JSON object.  

Best for storing user profiles, objects, structured data.  

👉 Example (user profile):  

```bash
hset user:101 name "Rahul" age "25" dept "IT"
hget user:101 name
```

### Output:

- "name" "Rahul"

- "age" "25"

- "dept" "IT"

## ✅ Summary

- **Strings** → Simple key-value.  
- **Lists** → Ordered collection (Queue/Stack).  
- **Sets** → Unique values (no duplicates).  
- **Sorted Sets (ZSETs)** → Sets with scores (leaderboards).  
- **Hashes** → Key with multiple fields (like JSON).  
