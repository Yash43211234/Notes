# Express.js Framework

Express.js is a **fast, minimal, and flexible** Node.js web framework for building APIs and web applications.

---

## 1. Setting Up a Basic Express Server

### Install Express
```bash
npm install express
```

## Basic Server Example

```js 

const express = require("express");
const app = express();

// Home route
app.get("/", (req, res) => {
    res.send("Hello from Express.js!");
});

// Start server
app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});

```

## 2. Middleware in Express

- Middleware functions are executed in the order they are defined.
- They have access to req, res, and next.

### Types of Middleware:

- 1 Built-in Middleware
#### Example: express.json() parses incoming JSON requests.

```js

app.use(express.json());

```

- 2 Custom Middleware
#### Example:

```js

app.use((req, res, next) => {
    console.log("Request URL:", req.url);
    next(); // Pass control to the next handler
});

```

- 3 Third-party Middleware

#### Example: Install morgan for logging.

```js 

npm install morgan


const morgan = require("morgan");
app.use(morgan("dev"));


```

## 3. Route Handling → GET, POST, PUT, DELETE

#### Example: 

```js

// GET request
app.get("/users", (req, res) => {
    res.send("Get all users");
});

// POST request
app.post("/users", (req, res) => {
    res.send("Create a new user");
});

// PUT request
app.put("/users/:id", (req, res) => {
    res.send(`Update user with ID ${req.params.id}`);
});

// DELETE request
app.delete("/users/:id", (req, res) => {
    res.send(`Delete user with ID ${req.params.id}`);
});

```

## 4. Error Handling Middleware
#### Example:

```js 

// Normal routes
app.get("/", (req, res) => {
    throw new Error("Something went wrong!");
});

// Error handling middleware
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send("Internal Server Error");
});

```

## 5. Working with req and res Objects

### Common req properties:

- req.params → Route parameters

- req.query → Query strings

- req.body → Request body (need express.json() middleware)

### Common res methods:

- res.send() → Send response

- res.json() → Send JSON response

- res.status() → Set status code

#### Example:

```js

app.get("/user/:id", (req, res) => {
    console.log("Params:", req.params.id);
    console.log("Query:", req.query);
    res.json({ message: "User details fetched" });
});

```

## Summary Table
- Concept	Example / Usage
- Basic Server	app.listen(port, callback)
- Built-in Middleware	express.json(), express.urlencoded()
- Custom Middleware	app.use((req,res,next)=>{...})
- Routes	GET, POST, PUT, DELETE
- Error Handling	app.use((err,req,res,next)=>{...})
- Request Object	req.params, req.query, req.body
- Response Object	res.send(), res.json(), res.status()
