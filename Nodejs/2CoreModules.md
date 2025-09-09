# Node.js Core Modules

Node.js provides many built-in modules to perform different tasks without installing extra packages.

---

## 1. fs (File System)
Used to **read, write, update, and delete files**.

### Example: Reading & Writing Files
```js
const fs = require("fs");

// Write file
fs.writeFileSync("test.txt", "Hello, Node.js!");

// Read file
const data = fs.readFileSync("test.txt", "utf-8");
console.log(data);

```

## 2. path Module

Helps in working with file paths.

### Example:

```js 
const path = require("path");

console.log("Directory:", path.dirname(__filename));
console.log("Extension:", path.extname(__filename));
console.log("Base Name:", path.basename(__filename));

```

## 3. os Module

Provides system information.

### Example:

```js

const os = require("os");

console.log("OS Platform:", os.platform());
console.log("CPU Architecture:", os.arch());
console.log("Free Memory:", os.freemem());
console.log("Total Memory:", os.totalmem());

```

## 4. events Module

Helps in creating & handling custom events.

### Example: EventEmitter

```js

const EventEmitter = require("events");
const event = new EventEmitter();

event.on("greet", () => {
    console.log("Hello, Welcome!");
});

event.emit("greet");


```

## 5. http Module

Used to create web servers.

### Example:

```js 

const http = require("http");

const server = http.createServer((req, res) => {
    res.write("Hello from HTTP Server!");
    res.end();
});

server.listen(4000, () => {
    console.log("Server running at http://localhost:4000");
});

```

## 6. url Module

Used to parse URLs.

### Example:

```js 

const url = require("url");

const myURL = "http://localhost:4000/home?name=John&age=25";
const parsed = url.parse(myURL, true);

console.log("Path:", parsed.pathname);
console.log("Query Params:", parsed.query);

```

## 7. crypto Module

Used for hashing & encryption.

### Example: Hashing with SHA256

```js

const crypto = require("crypto");

const hash = crypto.createHash("sha256")
                   .update("mypassword")
                   .digest("hex");

console.log("Hashed Value:", hash);

```

## Summary Table
    Module	Purpose
    fs	File operations (read/write)
    path	File paths, directory info
    os	OS info (CPU, memory, platform)
    events	EventEmitter & custom events
    http	Creating HTTP servers
    url	Parsing & working with URLs
    crypto	Hashing & encryption

