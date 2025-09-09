# 📘 Redis – Step 1: Basics (Simple Notes)

## 🔹 What is Redis?

- **Redis** = Remote Dictionary Server  
- It is a database that stores data in **memory (RAM)** instead of hard disk.  
- Because it uses **RAM → it is very fast**.  
- It is a **NoSQL database** (does not use tables like SQL).  
- It stores data in the form of **key → value pairs**.  

### Example:

```js
key   → value
name  → "Yashwant"
age   → 25
```

## 🔹 Why Redis?

- **Fast** → Can answer requests in microseconds.  
- **Persistent** → Can save data to disk if you want (so data is not lost).  
- **Scalable** → Can work in clusters and handle large traffic.  
- **Flexible** → Supports many data formats, not just text.  

## 🔹 Redis Use Cases

### 1. Caching  
- Keep frequently used data in memory.  
- **Example:** Store product details so the website loads faster.  

### 2. Session Store  
- Store user login sessions (like when you log into a website).  
- **Example:** Keep “logged-in” info for each user.  

### 3. Pub/Sub (Publish-Subscribe)  
- Redis can send messages between apps in real time.  
- **Example:** Chat app or notification system.  

### 4. Leaderboard / Ranking  
- Use **sorted sets** to make a live ranking system.  
- **Example:** Online games “Top 10 Players”.  

### 5. Queues (Task Management)  
- Store tasks in a queue for background workers.  
- **Example:** A job queue that processes orders.  

## 🔹 How to Install Redis?

### ✅ Method 1: Install Directly  

**Ubuntu/Linux**  

```bash
sudo apt update  
sudo apt install redis-server  
redis-server   # start Redis  
redis-cli      # open Redis CLI  
```

**Mac (Homebrew)**

```bash
brew install redis
brew services start redis
```

### ✅ Method 2: Install using Docker

- Pull image:
```bash 
docker pull redis
```
- Run container:
```bash
docker run --name redis-container -d redis
```
- Access Redis CLI inside container:
```bash
docker exec -it redis-container redis-cli
```

## 🔹 Check if Redis is Working

Open **Redis CLI** and run:  

```bash
set name "Yashwant"
get name
```
### 👉 Output will be:

```bash
"Yashwant"
```
