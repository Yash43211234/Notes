# REST APIs in Node.js

REST (Representational State Transfer) is a standard for building APIs where resources are identified by URLs and operations are performed using HTTP methods.

---

## 1. Designing RESTful Endpoints

| HTTP Method  | Purpose               | Example Endpoint          |
|--------------|-----------------------|----------------------------|
| GET          | Read data             | /api/users                 |
| POST         | Create new data       | /api/users                 |
| PUT          | Update entire data    | /api/users/:id             |
| PATCH        | Update partial data   | /api/users/:id             |
| DELETE       | Delete data           | /api/users/:id             |

### Example with Express:
```js
const express = require("express");
const app = express();

app.use(express.json()); // To parse JSON body

// GET - Read
app.get("/api/users", (req, res) => {
    res.status(200).json({ message: "Get all users" });
});

// POST - Create
app.post("/api/users", (req, res) => {
    res.status(201).json({ message: "User created", data: req.body });
});

// PUT - Update
app.put("/api/users/:id", (req, res) => {
    res.status(200).json({ message: `User ${req.params.id} updated` });
});

// DELETE - Delete
app.delete("/api/users/:id", (req, res) => {
    res.status(200).json({ message: `User ${req.params.id} deleted` });
});

app.listen(3000, () => console.log("Server running on port 3000"));
```

| Code | Meaning                  | Usage Example                 |
|------|---------------------------|-------------------------------|
| 200  | OK                        | Successful request            |
| 201  | Created                   | Resource successfully created |
| 400  | Bad Request               | Invalid request data           |
| 401  | Unauthorized              | Authentication required        |
| 403  | Forbidden                 | No permission to access        |
| 404  | Not Found                 | Resource not found             |
| 500  | Internal Server Error      | Server-side error              |


## 3. Sending & Receiving JSON Data
Sending JSON Response:

```js 
app.get("/api/info", (req, res) => {
    res.status(200).json({ name: "John", age: 25 });
});
```
Receiving JSON Request:
```js
app.post("/api/info", (req, res) => {
    const userData = req.body;
    res.status(201).json({ message: "Data received", data: userData });
});
```

## 4. Query Parameters vs URL Parameters

| Type              | Example URL                   | Access in Express | Usage                       |
|-------------------|-------------------------------|------------------|-----------------------------|
| Query Parameters   | /api/users?name=John&age=25    | req.query         | Filtering, searching        |
| URL Parameters     | /api/users/123                 | req.params        | Identifying specific resource |

### Example:

```js 

// URL Param
app.get("/api/users/:id", (req, res) => {
    res.send(`User ID: ${req.params.id}`);
});

// Query Param
app.get("/api/search", (req, res) => {
    res.send(`Name: ${req.query.name}, Age: ${req.query.age}`);
});

```
### Summary Table

| Concept                  | Example / Usage                                |
|---------------------------|-----------------------------------------------|
| GET, POST, PUT, DELETE     | REST API operations                           |
| Status Codes               | 200, 201, 400, 401, 403, 404, 500             |
| JSON Data                  | res.json(), req.body                          |
| Query Params               | req.query (e.g., /api?name=John)               |
| URL Params                 | req.params (e.g., /api/123)                    |
