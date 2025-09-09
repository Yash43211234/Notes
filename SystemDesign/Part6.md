# 📘 Scalability Techniques

## 1. Vertical vs Horizontal Scaling

- **Vertical Scaling (Scale Up):**
  - Increase power of a single machine (more CPU, RAM, SSD).
  - Simple but limited by hardware capacity.
  - Example: Upgrading from 8 GB RAM server to 64 GB RAM.

- **Horizontal Scaling (Scale Out):**
  - Add more servers to share the load.
  - Requires load balancing and distributed architecture.
  - Example: Adding 10 web servers behind a load balancer.

👉 Most large systems use **horizontal scaling**.

---

## 2. Database Scaling (Read Replicas, Write Splitting)

- **Read Replicas:**
  - Copies of the main database (master → replicas).
  - All **writes** go to master; **reads** go to replicas.
  - Helps in reducing load on master.
  - Example: MySQL replication, PostgreSQL replication.

- **Write Splitting:**
  - Directs write operations to master and read operations to replicas.
  - Needs proper routing logic in application or middleware.

---

## 3. Caching Patterns

- **Write-Through Cache:**
  - Data written to cache **and** database at the same time.
  - Ensures cache is always updated.
  - Slightly slower writes.

- **Write-Around Cache:**
  - Data written directly to database, cache updated only on read.
  - Good for infrequently accessed data.
  - Risk of cache miss on first read.

- **Write-Back Cache:**
  - Data written to cache first, then updated in database later (async).
  - Fast writes but risk of data loss if cache fails.

---

## 4. Content Delivery Networks (CDNs)

- **What is a CDN?**
  - Network of globally distributed servers.
  - Stores cached copies of static content (images, CSS, videos).
  - Serves content from the nearest server → low latency.

- **Examples:** Cloudflare, Akamai, AWS CloudFront.

👉 Improves website speed, reduces bandwidth usage, and handles traffic spikes.

---

## 5. Data Partitioning and Consistency Challenges

- **Data Partitioning (Sharding):**
  - Splitting data across multiple databases/servers.
  - Example: Users A–M in Shard 1, N–Z in Shard 2.
  - Helps in handling very large datasets.

- **Challenges:**
  - **Hotspots:** Some shards may get more traffic.
  - **Joins across shards:** Hard to implement efficiently.
  - **Rebalancing:** Moving data if shards get unbalanced.

- **Consistency Challenges:**
  - In distributed systems, ensuring strong consistency is hard.
  - Solutions: 
    - Use **eventual consistency** for scalable systems.
    - Use **quorum reads/writes** to balance consistency and availability.
