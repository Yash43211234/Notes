# 📌 MongoDB Schema Design

- Schema design in MongoDB is different from SQL because MongoDB is **schema-less** and **document-oriented**.  
- Main choice: **Embedding vs Referencing**, which affects **performance, storage, and query complexity**.  

---

## 🔹 1. Embedding Documents

- **Definition:** Store related data **inside a single document**.  
- **When to use:** Data is **accessed together frequently** and is **small in size**.  

### Example: User and their Address
```json
{
  "_id": 1,
  "name": "Rahul",
  "address": {
    "street": "MG Road",
    "city": "Bangalore",
    "zip": 560001
  }
}
```
### Pros
- Fewer queries → **fast read**  
- Keeps **related data together**  

### Cons
- **Document size limit:** 16MB  
- Harder to **update individual nested documents** frequently  

## 🔹 2. Referencing (Normalized Approach)

- **Definition:** Store related data in **separate collections** and link via **_id references**.  
- **When to use:** Data is **large**, reused by multiple documents, or **updated independently**.  

### Example: Users and Orders

```json
// User document
{ "_id": 1, "name": "Rahul" }

// Orders document
{ "_id": 101, "userId": 1, "product": "Laptop", "price": 50000 }
```
### Pros
- Flexible and **smaller documents**  
- Updates in one collection do not affect others  

### Cons
- Multiple queries or `$lookup` needed → **slower reads**  

## 🔹 3. Relationship Types in MongoDB

| **Relationship** | **Example**         | **Design Approach**                                     |
|------------------|-------------------|--------------------------------------------------------|
| One-to-One       | User → Profile     | Embed (if always accessed together) or Reference     |
| One-to-Many      | User → Orders      | Embed (small, few orders) or Reference (large, growing orders) |
| Many-to-Many     | Students → Courses | Use References with arrays of IDs in both collections |


### Examples:
```bash
One-to-One (Embed):

{
  "_id": 1,
  "name": "Rahul",
  "profile": { "age": 25, "gender": "M" }
}


One-to-Many (Reference):

// User
{ "_id": 1, "name": "Rahul" }
// Orders
{ "_id": 101, "userId": 1, "product": "Laptop" }


Many-to-Many (Reference with arrays):

// Student
{ "_id": 1, "name": "Amit", "courses": [101, 102] }
// Course
{ "_id": 101, "title": "Math", "students": [1, 2, 3] }
```
## 🔹 4. Trade-offs (Performance vs Flexibility)

| **Approach**   | **Performance**                               | **Flexibility**                  | **When to Use**                                       |
|----------------|-----------------------------------------------|---------------------------------|------------------------------------------------------|
| Embedding      | Fast reads (single query)                     | Less flexible (large docs)       | Data accessed together, small size                  |
| Referencing    | Slower reads (multiple queries or `$lookup`) | Highly flexible, scalable        | Large or growing data, reused data, frequent updates |

---

### ✅ Interview Tips
- **When to embed vs reference?**  
  Embed if data is small and accessed together; reference if data is large or reused.  

- **How to model One-to-Many in MongoDB?**  
  Either embed an array of subdocuments (small N) or use references (large N).  

- Always consider **document size limit (16MB)** and **query performance**.
