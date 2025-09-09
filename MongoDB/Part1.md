# 📌 MongoDB Basics vs SQL (RDBMS)

## 1. SQL (RDBMS) vs NoSQL (MongoDB)

| **Feature**       | **SQL (RDBMS)** | **NoSQL (MongoDB)** |
|--------------------|-----------------|----------------------|
| **Data Model**     | Table-based (rows & columns) | Document-oriented (BSON/JSON) |
| **Schema**         | Fixed schema (must define before inserting data) | Flexible schema (documents in same collection can have different fields) |
| **Relationships**  | Strong support (Primary Key, Foreign Key, Joins) | No joins (but supports embedded documents & references) |
| **Query Language** | SQL (Structured Query Language) | MongoDB Query Language (MQL – JSON-like syntax) |
| **Transactions**   | ACID compliant (strong consistency) | Supports transactions (since v4.0) but mainly BASE (Basically Available, Soft state, Eventually consistent) |
| **Scaling**        | Vertical Scaling (add more CPU/RAM to one server) | Horizontal Scaling (sharding across multiple servers) |
| **Use Cases**      | Banking, ERP, structured data systems | Big Data, IoT, social media, e-commerce, flexible data apps |

# 📌 2. Document-Oriented (BSON/JSON) vs Table-Based

## SQL (RDBMS)
- Data stored in **tables** (rows and columns).  
- Each **row = record**, each **column = attribute**.  

### Example: Users Table
+----+----------+-----+
| ID | Name | Age |
+----+----------+-----+
| 1 | Rahul | 25 |
| 2 | Priya | 30 |
+----+----------+-----+


---

## MongoDB (NoSQL)
- Data stored in **documents** (JSON/BSON format).  
- Each **document** can have **nested structures** and different fields.  

### Example: Users Collection
```json
{
  "_id": 1,
  "name": "Rahul",
  "age": 25,
  "hobbies": ["cricket", "music"]
}
{
  "_id": 2,
  "name": "Priya",
  "age": 30,
  "address": { "city": "Delhi", "pincode": 110001 }
}
```

 📌 3. Collections vs Tables

## Tables (SQL)
- Group of **rows** with the same **columns**.  
- **Schema is strict**, all rows must follow the defined structure.  

### Example: Users Table
+----+----------+-----+
| ID | Name | Age |
+----+----------+-----+
| 1 | Rahul | 25 |
| 2 | Priya | 30 |
+----+----------+-----+

yaml
Copy code

---

## Collections (MongoDB)
- Group of **documents**.  
- **No strict schema**, each document can have different fields.  

### Example: Users Collection
```json
// Document 1
{ "name": "Rahul", "age": 25 }

// Document 2
{ "name": "Priya", "city": "Delhi", "skills": ["Java", "React"] }
```
# 📌 4. Flexible Schema vs Fixed Schema

## SQL (RDBMS – Fixed Schema)
- Must **define schema** before inserting data.  
- Every record must follow the same structure.  

### Example
```sql
CREATE TABLE Users (
  id INT PRIMARY KEY,
  name VARCHAR(50),
  age INT
);
```
## MongoDB (Flexible Schema)

- Schema-less, allows different structures in the same collection.

- Documents can have different fields.

### Example
```json
{ "name": "Rahul", "age": 25 }
{ "name": "Priya", "city": "Delhi" }
```

#  Interview Summary: SQL vs MongoDB

| **Aspect**        | **SQL (RDBMS)**                           | **MongoDB (NoSQL)**                                                    |
|-------------------|-------------------------------------------|-------------------------------------------------------------------------|
| Data Model        | Structured, relational                    | Document-based (JSON/BSON)                                             |
| Schema            | Strict (fixed schema required)            | Flexible (schema-less)                                                 |
| Transactions      | Strong ACID guarantees                    | Supports multi-document transactions since v4.0; generally BASE model   |
| Use Cases         | Ideal for structured data and transactions (e.g., banking, ERP) | Excellent for scalability, big data, semi/unstructured data (e.g., IoT, social media) |
| Terminology       | Tables, Rows, Columns                     | Collections, Documents, Fields                                         |

