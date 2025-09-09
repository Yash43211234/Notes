# 📌 MongoDB Replication & Sharding

MongoDB uses **Replication** and **Sharding** for **scalability** and **high availability**.  

---

## 🔹 1. Replication (High Availability)

- **Definition:** Copying the same data to multiple servers (nodes) to prevent data loss and downtime.  
- **Primary Concept:** **Replica Set**  
  - **Primary Node:** Handles write operations  
  - **Secondary Nodes:** Replicate data from primary; can serve read operations  
  - **Automatic Failover:** If primary fails, a secondary is elected as new primary  

### Command to view replica set
```javascript
rs.status()
```
### Pros
- High availability  
- Data redundancy  
- Disaster recovery  
- Can scale reads (read from secondary nodes)  

### Cons
- Does not improve write performance significantly  
- Slight lag in secondary replication  

**SQL Equivalent:** Database mirroring or master-slave replication  

---

## 🔹 2. Sharding (Horizontal Scaling)

- **Definition:** Splitting data across multiple servers (shards) to handle large datasets and high traffic.  

### Components
- **Shards:** Store actual data  
- **Config servers:** Store metadata  
- **Query routers (mongos):** Direct queries to correct shards  

### Example: Shard Users collection based on `userId`
```javascript
sh.shardCollection("mydb.Users", { userId: 1 })
```

## 🔹 Sharding (Horizontal Scaling)

### Pros
- Handles huge datasets  
- Improves write & read performance  
- Scales horizontally (add more servers)  

### Cons
- Complex setup & maintenance  
- Queries across shards can be slower (if not sharded properly)  
- Data balancing required  

**SQL Equivalent:** Partitioning / Distributed databases  

---

## 🔹 3. Replication vs Sharding

| **Feature**     | **Replication**                           | **Sharding**                                     |
|-----------------|-------------------------------------------|------------------------------------------------|
| Purpose          | High availability                          | Horizontal scaling                              |
| Data Storage     | Copies of same data on multiple nodes      | Different subsets of data on different nodes  |
| Read/Write       | Read can be scaled, write still goes to primary | Read & write both distributed               |
| Failover         | Automatic failover if primary fails        | Not for failover (each shard may have its own replica set) |
| Use Case         | Protect against server failure             | Handle huge data & high traffic               |

---

### ✅ Interview Tips
- **When to use replication vs sharding?**  
  - Replication → High availability and disaster recovery  
  - Sharding → Scale horizontally for large datasets or high write/read throughput  

- **Often used together:** Each shard is a **replica set** → High availability + scalability  

