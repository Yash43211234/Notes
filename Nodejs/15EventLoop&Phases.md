# Node.js Common Interview Questions Notes

## 1. Event Loop & Its Phases
- **Event Loop**: Handles asynchronous tasks in Node.js using a single thread.
- **Phases**:
  1. **Timers Phase** → Executes `setTimeout` & `setInterval` callbacks.
  2. **Pending Callbacks** → Executes I/O callbacks.
  3. **Idle, Prepare** → Internal processes.
  4. **Poll Phase** → Retrieves new I/O events; executes callbacks.
  5. **Check Phase** → Executes `setImmediate()` callbacks.
  6. **Close Callbacks** → Executes close events like `socket.on('close')`.

---

## 2. Synchronous vs Asynchronous Programming
| Feature                | Synchronous                       | Asynchronous                     |
|------------------------|-----------------------------------|-----------------------------------|
| Execution              | Line by line                     | Non-blocking, parallel tasks      |
| Example                | `fs.readFileSync()`               | `fs.readFile()`                   |
| Performance            | Slower if task is heavy           | Faster due to event loop          |

---

## 3. Handling Multiple Requests on a Single Thread
- Node.js uses **non-blocking I/O** and the **event loop**.
- When a request involves I/O (e.g., DB query), Node.js delegates it to the OS or worker threads.
- Main thread stays free to handle other requests while I/O completes.

---

## 4. Middleware Flow in Express.js
1. **Request** → comes to Express server.
2. **Middleware 1** → modifies `req`, calls `next()`.
3. **Middleware 2** → further processing, calls `next()`.
4. **Route Handler** → final response is sent.

Example:
```js
app.use((req, res, next) => {
  console.log("Middleware 1");
  next();
});

app.get("/", (req, res) => {
  res.send("Hello World");
});
```

| Feature           | process.nextTick()                       | setImmediate()                        |
|-------------------|-------------------------------------------|----------------------------------------|
| Execution Time     | Before the next Event Loop iteration      | In the "Check" phase                   |
| Priority           | Higher priority                          | Lower priority                          |
| Use Case           | Quick async tasks                        | Scheduled tasks after I/O events        |


#### Example Code in Node.js:

```js

console.log("Start");

process.nextTick(() => {
    console.log("process.nextTick callback");
});

setImmediate(() => {
    console.log("setImmediate callback");
});

console.log("End");
```