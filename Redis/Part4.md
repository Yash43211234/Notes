# 📘 Redis – Step 4: Integration with Backend (Node.js)

Redis is often used with backend applications to make them faster and more efficient.

## 🔹 1. Install Redis Client in Node.js

You can use **ioredis** (popular) or **redis** package.

**Using ioredis:**  
```bash
npm install ioredis
```
#### Using redis (official):
``` bash
- npm install redis
```
## 🔹 2. Connect Redis to Node.js

**ioredis Example:**  
```javascript
const Redis = require("ioredis");
const redis = new Redis();  // connects to localhost:6379

// Test connection
redis.set("name", "Yashwant");
redis.get("name", (err, result) => {
  console.log(result);  // Output: Yashwant
});
```
## 🔹 3. Use Cases in Backend

### ✅ 1. Cache API Responses

- Store frequently requested data in Redis.  
- Reduces load on main database and speeds up response.  

```javascript
const cacheKey = "user:101";
const cachedData = await redis.get(cacheKey);

if (cachedData) {
  console.log("From Redis:", JSON.parse(cachedData));
} else {
  const userData = await getUserFromDB(101); // hypothetical DB call
  await redis.set(cacheKey, JSON.stringify(userData), "EX", 3600); // expires in 1 hour
  console.log("From DB:", userData);
}
```
### ✅ 2. Store User Sessions

- Redis is perfect for session management.  
- Fast and can auto-expire sessions.  

```javascript
// When user logs in
redis.set("session:123", JSON.stringify({ userId: 101 }), "EX", 3600); // 1 hour session

// To check session
const session = await redis.get("session:123");
console.log(JSON.parse(session));
```
### ✅ 3. Implement Queue System

- Use Redis lists for job queues (background tasks).  
- Workers can push tasks and pop tasks.  

```javascript
// Producer: Add job to queue
await redis.lpush("jobs", JSON.stringify({ task: "sendEmail", user: 101 }));

// Worker: Process job
const job = await redis.rpop("jobs");
if (job) {
  const task = JSON.parse(job);
  console.log("Processing:", task);
}
```
## 🔹 4. Tips

- Always set expiry for cache/session data to avoid memory overflow.  
- Use namespaces in keys to avoid conflicts: `user:101`, `session:123`.  
- Use Redis pipelines or `multi` for batch operations (advanced).  
