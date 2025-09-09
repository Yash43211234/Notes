Redis also has advanced features that make it powerful for real-world apps.

## 🔹 1. Persistence (Saving Data to Disk)

- Redis is in-memory, but you can save data to disk so it’s not lost if the server restarts.  

**Two ways:**  

### RDB (Redis Database Backup)
- Takes snapshots of Redis data at intervals.  
- Good for backups.  
- Example config: save every 5 minutes if ≥ 100 changes.  

### AOF (Append Only File)
- Logs every write operation.  
- Can replay logs to restore data.  
- Safer than RDB for critical data.  

## 🔹 2. Pub/Sub (Publish/Subscribe)

- Redis can send messages between apps in real-time.  
- Used in chat apps, notifications, live updates.  

### Example:
```bash
## Subscriber
SUBSCRIBE chat_channel

## Publisher
PUBLISH chat_channel "Hello everyone!"
```

- All subscribers of chat_channel receive the message instantly.

## 🔹 3. Redis Cluster (Scaling)

- For large data, a single Redis server may not be enough.  
- Redis Cluster splits data into multiple nodes.  
- Provides high availability and automatic sharding.  

**Concept:**  
- Keys are distributed across nodes.  
- If one node fails → others keep running.  

## 🔹 4. TTL (Time To Live)

- TTL allows keys to expire automatically.  
- Perfect for OTP, session tokens, temporary cache.  

**Commands:**  
```bash
SET otp:101 "123456" EX 120   # expires in 120 seconds
TTL otp:101                   # check remaining time
```

After 120 seconds, the key `otp:101` is deleted automatically.

## ✅ Summary of Advanced Concepts

| Feature       | Use Case                               |
|---------------|----------------------------------------|
| Persistence   | Save data to disk (RDB, AOF)          |
| Pub/Sub       | Real-time messaging (chat, notifications) |
| Redis Cluster | Scaling, high availability             |
| TTL           | Auto-expiring keys (OTP, sessions)    |

✨ With these advanced features, Redis is fast, reliable, and scalable.
