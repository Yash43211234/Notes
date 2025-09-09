# Database Integration in Node.js

Node.js supports multiple databases like **MongoDB** (NoSQL) and **MySQL/PostgreSQL** (SQL).  
We can use ORMs like **Mongoose** for MongoDB and **Sequelize/pg** for SQL databases.

---

## 1. MongoDB Basics with Mongoose

### Install Packages
```bash
npm install mongoose
```

## Connect to MongoDB

```js

const mongoose = require("mongoose");

mongoose.connect("mongodb://127.0.0.1:27017/mydb")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));
```

## Create Schema & Model

```js

const userSchema = new mongoose.Schema({
    name: String,
    age: Number
});

const User = mongoose.model("User", userSchema);

```

## CRUD Operations

```js

// Create
app.post("/users", async (req, res) => {
    const user = new User(req.body);
    await user.save();
    res.status(201).json(user);
});

// Read
app.get("/users", async (req, res) => {
    const users = await User.find();
    res.json(users);
});

// Update
app.put("/users/:id", async (req, res) => {
    const user = await User.findByIdAndUpdate(req.params.id, req.body, { new: true });
    res.json(user);
});

// Delete
app.delete("/users/:id", async (req, res) => {
    await User.findByIdAndDelete(req.params.id);
    res.send("User deleted");
});

```

## 2. MySQL/PostgreSQL Basics with Sequelize

### Install Packages

```js

npm install sequelize mysql2        # For MySQL
npm install sequelize pg pg-hstore  # For PostgreSQL

```

### Connect to Database

```js

const { Sequelize, DataTypes } = require("sequelize");
const sequelize = new Sequelize("mydb", "root", "password", {
    host: "localhost",
    dialect: "mysql"  // change to "postgres" for PostgreSQL
});

sequelize.authenticate()
    .then(() => console.log("Database Connected"))
    .catch(err => console.log(err));

```
## Define Model

```js

const User = sequelize.define("User", {
    name: DataTypes.STRING,
    age: DataTypes.INTEGER
});

```

## Sync Database

```js
    sequelize.sync();

```

## CRUD Operations

```js
// Create
app.post("/users", async (req, res) => {
    const user = await User.create(req.body);
    res.status(201).json(user);
});

// Read
app.get("/users", async (req, res) => {
    const users = await User.findAll();
    res.json(users);
});

// Update
app.put("/users/:id", async (req, res) => {
    await User.update(req.body, { where: { id: req.params.id } });
    res.send("User updated");
});

// Delete
app.delete("/users/:id", async (req, res) => {
    await User.destroy({ where: { id: req.params.id } });
    res.send("User deleted");
});

```

## Summary Table:

| Feature            | MongoDB (Mongoose)           | MySQL/PostgreSQL (Sequelize)      |
|--------------------|-------------------------------|-----------------------------------|
| Type               | NoSQL (Document-based)        | SQL (Relational)                  |
| Schema Definition   | Flexible JSON-like docs       | Tables with strict schema          |
| CRUD Methods        | find(), save(), update()      | findAll(), create(), update()      |
| Connection String   | MongoDB URL                   | Host, DB name, Username, Password  |
| Best for            | JSON-heavy, unstructured data | Structured, relational data        |
