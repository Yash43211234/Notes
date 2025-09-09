# Node.js Basics

## 1. What is Node.js?
- Node.js is an **open-source**, **cross-platform** runtime environment.
- Built on **Chrome's V8 JavaScript Engine**.
- Used to run JavaScript **outside the browser**.
- Suitable for **server-side** and **network applications**.

---

## 2. Features of Node.js

### a) Single-threaded
- Node.js uses a **single-threaded event loop** architecture.
- Handles multiple requests without creating multiple threads.

### b) Event-driven
- Everything in Node.js is based on **events**.
- Example: Server starts → Event triggers → Executes callback.

### c) Non-blocking I/O
- Node.js uses **asynchronous I/O**.
- Operations like file reading or database queries don’t block the main thread.

---

## 3. Node.js vs JavaScript

| Aspect           | JavaScript                               | Node.js                                  |
|------------------|-------------------------------------------|------------------------------------------|
| Definition        | A **programming language**               | A **runtime environment** for JS          |
| Environment       | Runs in **browsers**                     | Runs on **servers** & local systems        |
| APIs              | Has DOM, Browser APIs                    | Has File System, OS, HTTP, DB APIs         |
| Usage             | Client-side scripting                   | Server-side scripting                     |

---

## 4. Node.js Architecture

### Components:
1. **Event Loop** – Listens for events & triggers callbacks.
2. **Callbacks** – Functions executed when a task completes.
3. **Event-driven Model** – Execution continues without waiting for tasks.

**Flow:**
Request → Event Queue → Event Loop → Worker Threads (if needed) → Callback → Response

---

## 5. Node.js vs Traditional Backend (Java, PHP)

| Feature             | Node.js                      | Java/PHP                              |
|---------------------|-------------------------------|---------------------------------------|
| Concurrency Model    | Non-blocking, Event-driven     | Multi-threaded, Blocking I/O           |
| Performance         | High for I/O operations        | Slower for I/O heavy tasks             |
| Scalability         | Highly scalable                | Less scalable due to thread overhead   |
| Learning Curve       | Easy (JS-based)               | Moderate to difficult                  |

---

## Example: Simple Node.js Server
```js
// Import http module
const http = require("http");

// Create server
const server = http.createServer((req, res) => {
    res.write("Hello from Node.js!");
    res.end();
});

// Listen on port 3000
server.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
