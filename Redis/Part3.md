# 📘 Redis – Step 3: Commands

These are basic Redis commands you’ll use in redis-cli for different data types.

## 🔹 1. Strings Commands

- **SET key value** → Store a value.  
- **GET key** → Retrieve a value.  
- **INCR key** → Increase a number by 1.  
- **DECR key** → Decrease a number by 1.  

### 👉 Example:

```bash
SET name "Yashwant"
GET name
# Output: "Yashwant"

SET count 10
INCR count
# Output: 11
DECR count
# Output: 10
```

## 2. List Commands

- **LPUSH list value** → Add value to the left of the list.  
- **RPUSH list value** → Add value to the right of the list.  
- **LPOP list** → Remove value from left.  
- **RPOP list** → Remove value from right.  
- **LRANGE list start end** → Show values in range.  

### 👉 Example:

```bash
LPUSH tasks "task1"
LPUSH tasks "task2"
RPUSH tasks "task3"
LRANGE tasks 0 -1
# Output: ["task2", "task1", "task3"]

LPOP tasks
# Output: "task2"
RPOP tasks
# Output: "task3"
```

## 🔹 3. Set Commands

- **SADD set value** → Add a value to set (no duplicates).  
- **SMEMBERS set** → Show all values in set.  
- **SISMEMBER set value** → Check if value exists (1 = yes, 0 = no).  

### 👉 Example:

```bash
SADD tags "redis"
SADD tags "database"
SADD tags "redis"   # duplicate ignored
SMEMBERS tags
# Output: ["redis", "database"]

SISMEMBER tags "redis"
# Output: 1
SISMEMBER tags "sql"
# Output: 0
```

## 🔹 4. Hash Commands

- **HSET key field value** → Store field-value pair in a hash.  
- **HGET key field** → Get value of a field.  
- **HGETALL key** → Get all field-value pairs.  

### 👉 Example:

```bash
HSET user name "Yash" age "25" dept "IT"
HGET user name
# Output: "Yash"

HGETALL user
# Output: 
# 1) "name" "Yash"
# 2) "age"  "25"
# 3) "dept" "IT"
```

## 🔹 5. Sorted Set Commands (Optional)

- **ZADD key score value** → Add value with score.  
- **ZRANGE key start end WITHSCORES** → Show values in order.  
- **ZREVRANGE key start end WITHSCORES** → Highest score first.  

### 👉 Example:

```bash
ZADD leaderboard 100 "Alice"
ZADD leaderboard 200 "Bob"
ZRANGE leaderboard 0 -1 WITHSCORES
# Output: "Alice" 100, "Bob" 200
```
