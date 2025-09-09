# 📘 Storage & Databases

## 1. Relational (MySQL) vs NoSQL (MongoDB, DynamoDB)

- **Relational Database (SQL):**
  - Structured tables (rows & columns).
  - Follows schema (fixed structure).
  - Good for transactions (ACID).
  - Example: MySQL, PostgreSQL, Oracle.

- **NoSQL Database:**
  - Flexible schema (documents, key-value, graph, column-based).
  - Handles unstructured or semi-structured data.
  - Good for scalability & large data.
  - Example: MongoDB (documents), DynamoDB (key-value).

---

## 2. Indexing and Query Optimization

- **Indexing:**
  - Like a **book’s index** → helps to find data faster.
  - Without index → full table scan.
  - With index → quick lookup using index tree.

- **Query Optimization:**
  - Use proper indexes.
  - Avoid `SELECT *`.
  - Normalize/denormalize wisely.
  - Cache results if query is heavy.

---

## 3. Database Partitioning

- **Sharding:**
  - Splitting data into multiple databases/servers.
  - Example: Users with A–M in one shard, N–Z in another.
  - Helps in handling very large data.

- **Replication:**
  - Copying data across multiple servers.
  - **Master-Slave:** Writes go to master, reads from slaves.
  - Provides high availability and backup.

---

## 4. SQL vs NoSQL Trade-offs

- **SQL (Relational):**
  - Strong consistency (ACID).
  - Complex queries with JOINs.
  - Less scalable for massive data.

- **NoSQL:**
  - Flexible, faster for large-scale systems.
  - Better horizontal scaling.
  - Weaker consistency sometimes (eventual consistency).

👉 Choice depends on **use case** (banking → SQL, social media → NoSQL).

---

## 5. Caching Layers (Redis, Memcached)

- **Redis:**
  - In-memory key-value store.
  - Supports advanced data types (lists, sets, hashes).
  - Great for caching, session store, real-time analytics.

- **Memcached:**
  - Simple in-memory cache.
  - Fast but less feature-rich than Redis.

👉 Both reduce load on databases and improve response time.
