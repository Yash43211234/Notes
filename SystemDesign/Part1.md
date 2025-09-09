# 📘 System Design – Basics & Foundations (Detailed Easy Notes)

---

## 1. What is System Design?  

System design means **planning and creating the structure of a software system** so it can handle users, data, and performance requirements.  

### Two levels of design:  

🔹 **High-Level Design (HLD):**  
- Big picture view of the system.  
- Shows how different main components connect (UI, backend, database, cache, load balancer).  
- Example: In an e-commerce site → HLD shows modules like **User Service**, **Product Service**, **Order Service**, and how they talk to each other.  

🔹 **Low-Level Design (LLD):**  
- Detailed view of how each component will work.  
- Includes database schema, class diagrams, APIs, functions.  
- Example: For **User Service**, LLD shows how login API works, which tables are created, what validations are applied.  

👉 In short:  
- **HLD = Architecture**  
- **LLD = Implementation details**  

---

## 2. Scalability  

Scalability means a system’s ability to **grow and handle more users, requests, or data** without failing.  

### Types of scaling:  

🔹 **Vertical Scaling (Scaling Up):**  
- Make one server more powerful (add CPU, RAM, storage).  
- Easy to implement.  
- Limited by hardware (you can’t upgrade forever).  
- Example: Upgrading from a **8 GB RAM server** → **64 GB RAM server**.  

🔹 **Horizontal Scaling (Scaling Out):**  
- Add more servers/machines to share the load.  
- Needs load balancer + distributed system.  
- More flexible and fault tolerant.  
- Example: Adding **10 web servers** behind a load balancer to handle traffic.  

👉 In real-world big systems (Google, Amazon, Netflix) → **Horizontal Scaling is preferred**.  

---

## 3. Latency vs Throughput  

🔹 **Latency:**  
- Time taken to handle a single request.  
- Measures delay.  
- Example: Searching for “Laptop” on Amazon takes **200 ms**.  

🔹 **Throughput:**  
- Number of requests processed per unit time.  
- Shows capacity of the system.  
- Example: Amazon can handle **100,000 requests per second**.  

👉 Goal of good system design: **Low latency + High throughput**  

---

## 4. CAP Theorem  

In a **distributed system** (data stored on many servers), we can’t have all three guarantees at once:  

1. **Consistency (C):**  
   Every server has the same data at the same time.  
   Example: If you update your profile picture, it should be updated everywhere instantly.  

2. **Availability (A):**  
   System always gives a response (even if it’s not the latest data).  
   Example: Amazon product page still loads even if some data is slightly old.  

3. **Partition Tolerance (P):**  
   System keeps working even if there are network issues or servers can’t talk to each other.  

👉 **Rule:** Partition tolerance is a must in distributed systems.  
So, systems choose:  
- **CP (Consistency + Partition Tolerance):** e.g., MongoDB (with strong consistency), SQL databases.  
- **AP (Availability + Partition Tolerance):** e.g., Cassandra, DynamoDB.  

---

## 5. Load Balancing  

A **Load Balancer** is like a **traffic police** that distributes incoming requests across multiple servers.  

### Why needed?  
- Prevents one server from overloading.  
- Ensures high availability.  
- Helps in scaling (more servers can be added easily).  

### Load Balancing Strategies:  
- **Round Robin:** Each request goes to the next server in order.  
- **Least Connections:** Request goes to the server with the fewest active connections.  
- **IP Hash:** Same client goes to the same server (good for sessions).  

👉 Tools used: Nginx, HAProxy, AWS Elastic Load Balancer.  

**Example:** Netflix uses load balancing → when millions of people watch movies at the same time, requests are divided across many servers.  

---

## 6. Caching  

**Cache = temporary storage** for frequently used data, usually stored in memory (faster than disk).  

### Why cache?  
- Reduces load on database.  
- Makes system faster (low latency).  
- Improves throughput.  

### Types of caching:  
- **Browser Cache (Client-side):** Saves images, scripts, styles → page loads faster next time.  
- **Server-side Cache:** API responses stored in Redis/Memcached.  
- **Database Cache:** Frequently run queries are cached.  

👉 Example: Google search → results load super fast because most popular searches are cached.  

---

## ✅ Summary of Concepts  
- **System Design:** Planning architecture (HLD = big picture, LLD = details).  
- **Scalability:** Grow system (Vertical = stronger machine, Horizontal = more machines).  
- **Latency vs Throughput:** Delay vs capacity.  
- **CAP Theorem:** Pick 2 of (Consistency, Availability, Partition Tolerance).  
- **Load Balancing:** Spread requests across servers.  
- **Caching:** Store frequently used data in memory for faster access.  
