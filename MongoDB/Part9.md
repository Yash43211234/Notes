# 📌 MongoDB Performance & Best Practices

Performance depends on **indexes, schema design, document size, and query patterns**. Following best practices ensures **scalable and fast applications**.  

---

## 🔹 1. Indexing Strategies

- Use indexes to **improve query performance**, but avoid over-indexing (slows writes).  

**Best Practices:**
- Index fields used in **filters, sorts, and joins ($lookup)**  
- Use **compound indexes** when multiple fields are queried together  
- Use **multikey indexes** for arrays if needed  
- Avoid indexing **highly volatile fields**  
- Use **TTL indexes** for temporary data (sessions, OTP)  

**Interview Tip:**  
- *“How to optimize query performance in MongoDB?”* → Use **proper indexes**, **projection**, and **limit returned fields**  

---

## 🔹 2. Avoiding Large Documents

- MongoDB **document size limit:** 16MB  

**Best Practices:**
- Keep documents **small and manageable**  
- Use **referencing** for large or growing data instead of embedding  
- Use **GridFS** for storing files larger than 16MB  

---

## 🔹 3. Schema Design for Scaling

- **Embed or reference wisely** based on access patterns  

**Sharding Considerations:**
- Choose a **shard key** that ensures even data distribution  
- Avoid **monotonically increasing keys** (like auto-increment `_id`) → causes hotspot  
- **Read-heavy workloads:** Use **replica sets** to scale reads  
- **Write-heavy workloads:** Consider **sharding** to distribute writes  

---

## 🔹 4. Normalized (SQL) vs Denormalized (MongoDB) Design

| **Feature**       | **SQL (Normalized)**             | **MongoDB (Denormalized / Embedded)** |
|------------------|---------------------------------|-------------------------------------|
| Data Redundancy   | Low                             | Can be high (embedded docs)         |
| Joins             | Common                          | Avoid joins if possible ($lookup)   |
| Read Performance  | Slower for many joins           | Faster if data embedded together    |
| Write Performance | Faster updates on single table  | Slower if multiple copies of embedded data |
| Flexibility       | Schema strict                   | Schema flexible                     |
