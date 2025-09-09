# 📌 Other Important MongoDB Features

MongoDB provides advanced features beyond CRUD and indexing, which are frequently asked in interviews.  

---

## 🔹 1. TTL (Time-To-Live) Index

- **Definition:** Automatically deletes documents after a **specified time**.  
- **Use Cases:** OTPs, sessions, temporary data.  

### TTL Index: Command Example
```javascript
db.sessions.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 })
```

- Explanation: Documents in the sessions collection will be automatically removed 1 hour after createdAt.

### ✅ Interview Tip

- TTL indexes run as background tasks, so they do not guarantee exact deletion time.

## 🔹 2. Capped Collections

- **Definition:** Fixed-size collections that automatically **overwrite old documents**.  
- **Use Cases:** Logs, caching, circular buffers.  

### Command Example
```javascript
db.logs.createCollection("logs", { capped: true, size: 5242880, max: 5000 })
```
### Explanation

- size → Maximum storage in bytes
- max → Maximum number of documents
- Provides fast insert and read operations due to pre-allocated space

## 🔹 3. Change Streams

- **Definition:** Allows applications to **listen to real-time changes** in a collection, database, or cluster.  
- **Use Cases:** Event-driven apps, notifications, real-time analytics.  

### Example
```javascript
const changeStream = db.orders.watch();
changeStream.on("change", (next) => {
  console.log(next); // logs insert/update/delete events
});
```
- SQL Equivalent: Database triggers (but more flexible and asynchronous).

## 🔹 4. MongoDB Atlas

- **Definition:** Cloud-hosted MongoDB platform (**fully managed**).  
- **Features:**  
  - Automated backups & scaling  
  - High availability via replica sets  
  - Monitoring & security  
  - Global clusters for low-latency access  

### ✅ Interview Tip
- Atlas is often mentioned for **production deployments** and **cloud-based applications**  

---

## 🔹 Summary Table: Other Important Features

| **Feature**         | **Purpose**                | **Use Case**                     |
|---------------------|---------------------------|---------------------------------|
| TTL Index            | Auto-expire documents     | OTP, session expiry             |
| Capped Collection    | Fixed-size, circular storage | Logs, cache                   |
| Change Streams       | Real-time data notifications | Event-driven apps, analytics  |
| Atlas                | Cloud DB service          | Production, managed DB          |

### 💡 Interview Tips
- **How can you automatically delete expired sessions?** → Use TTL index  
- **How to implement real-time notifications?** → Use Change Streams  
