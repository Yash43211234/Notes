# 📌 Indexes in MongoDB

## 🔹 What are Indexes?
- Indexes are **special data structures** that improve query performance.  
- **Without indexes** → MongoDB does a *collection scan* (checks every document).  
- **With indexes** → MongoDB can directly jump to matching documents (like an index in a book).  
- **Trade-off**: Indexes speed up **read queries**, but slow down **writes** (insert/update/delete), since the index must also be updated.  

---

## 🔹 Types of Indexes in MongoDB

### 1. Single Field Index
- Created on **one field** of a document.  
- Example: Index on `age`.  


```javascript
#### Command

db.users.createIndex({ age: 1 })

#### SQL Equivalent:

CREATE INDEX idx_age ON Users(age ASC);


#### Use Case: Speeds up queries like:

db.users.find({ age: 25 })

```

## 2. Compound Index

- Index on multiple fields (order matters).

### Example: Index on name and age.
```bash 
Command:

db.users.createIndex({ name: 1, age: -1 })


SQL Equivalent:

CREATE INDEX idx_name_age ON Users(name ASC, age DESC);

```
### Important:

- Can support queries on {name} or {name, age}.

- ❌ Cannot directly use {age} alone (unless name is also included).

- Use Case: Queries with multiple filters:
```bash
db.users.find({ name: "Rahul", age: 25 })
```
### 3. Multikey Index (for Arrays)
- Used when a field contains an **array**.  
- MongoDB creates **separate index entries** for each element in the array.  

#### Example
Field:  
```json
{ "skills": ["Java", "Python", "MongoDB"] }

### Command
db.users.createIndex({ skills: 1 })

###  Query
db.users.find({ skills: "Python" })
```

#### ✅ MongoDB automatically converts it into a multikey index.

### 4. Text Index (Full-text Search)
- Allows searching **inside string fields** (like `LIKE '%word%'` in SQL).  
- Supports **stemming, stop words**, and **case-insensitive search**.  


```javascript
#### Command
db.articles.createIndex({ content: "text" })


### Query
db.articles.find({ $text: { $search: "mongodb performance" } })

### SQL Equivalent
SELECT * FROM articles 
WHERE MATCH(content) AGAINST ('mongodb performance');
```

### 5. Geospatial Index
- Used for **storing and querying location-based data** (`2D` or `2dsphere`).  
- Commonly used in **maps, ride-sharing, and delivery apps**.  

#### Command
```javascript
db.places.createIndex({ location: "2dsphere" })
Query
javascript
Copy code
db.places.find({
  location: {
    $near: {
      $geometry: { type: "Point", coordinates: [77.5946, 12.9716] }, // Bangalore
      $maxDistance: 5000 // within 5 km
    }
  }
})
```

# ✅ Indexes Summary (Interview Points)

- **Purpose:** Indexes improve **read/query performance** but add **overhead on writes** (insert/update/delete).  

- **Types of Indexes:**
  1. **Single Field** → Index on one field.  
  2. **Compound** → Index on multiple fields (**order-sensitive**).  
  3. **Multikey** → Index on **array fields**.  
  4. **Text** → Full-text search on string fields.  
  5. **Geospatial** → Location-based queries.  

- **Interview Tip:**  
  **Question:** “What happens if you query without an index?”  
  **Answer:** MongoDB performs a **COLLSCAN (collection scan)** → slow for large datasets.
