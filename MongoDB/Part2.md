# 📌 CRUD Operations: MongoDB vs SQL

CRUD = **Create, Read, Update, Delete**  
- **SQL** uses queries on **tables**.  
- **MongoDB** uses methods on **collections**.  

---

## 1. Create (Insert)

### SQL (RDBMS)
```sql
INSERT INTO Users (id, name, age) 
VALUES (1, 'Rahul', 25);
```
## MongoDB (NoSQL)

```sql
db.users.insertOne(
  { _id: 1, name: "Rahul", age: 25 }
)
```

- 🔹 insertMany() can insert multiple documents at once.
- 🔹 SQL inserts into tables, MongoDB inserts into collections.

## 2. Read (Select / Find)

### SQL
```sql
SELECT * FROM Users WHERE age > 25;
```
## MongoDB
```sql
db.users.find({ age: { $gt: 25 } })
```
- 🔹 SQL uses SELECT ... WHERE.
- 🔹 MongoDB uses find() with query operators ($gt, $lt, $eq, $in, etc.).

## 3. Projection (Selecting specific fields/columns)

```bash
SQL:

SELECT name, age FROM Users;

MongoDB:

db.users.find({}, { name: 1, age: 1 })
```

- 🔹 1 = include field, 0 = exclude field.
- 🔹 By default, _id is always included unless explicitly excluded ({ _id: 0 }).

## 4. Update
```bash
SQL:

UPDATE Users 
SET age = 26 
WHERE name = 'Rahul';


MongoDB:

db.users.updateOne(
  { name: "Rahul" },
  { $set: { age: 26 } }
)

```
- 🔹 updateOne() → updates first matching document.
- 🔹 updateMany() → updates all matching documents.

## 5. Delete
```bash
SQL:

DELETE FROM Users WHERE name = 'Rahul';


MongoDB:

db.users.deleteOne({ name: "Rahul" })
```

- 🔹 deleteOne() → deletes first matching doc.
- 🔹 deleteMany() → deletes all matching docs.

# ✅ Quick Comparison Table: SQL vs MongoDB CRUD

| **Operation** | **SQL (RDBMS)** | **MongoDB (NoSQL)** |
|---------------|-----------------|----------------------|
| **Insert**    | `INSERT INTO table ...` | `db.collection.insertOne()` |
| **Read**      | `SELECT * FROM table WHERE ...` | `db.collection.find({ ... })` |
| **Projection**| `SELECT col1, col2 FROM table` | `db.collection.find({}, { col1:1, col2:1 })` |
| **Update**    | `UPDATE table SET col=val WHERE ...` | `db.collection.updateOne({query}, {$set:{...}})` |
| **Delete**    | `DELETE FROM table WHERE ...` | `db.collection.deleteOne({query})` |
