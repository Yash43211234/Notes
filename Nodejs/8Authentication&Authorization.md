# Authentication & Authorization in Node.js

Authentication → Verifies **who you are** (Login/Signup).  
Authorization → Decides **what you can access** (Permissions, Roles).

---

## 1. JWT (JSON Web Token)

JWT is used for **stateless authentication** between client and server.

### Install Packages
```bash
npm install jsonwebtoken bcryptjs
```

## Signup Flow (Hash Password)

```js

const bcrypt = require("bcryptjs");
const jwt = require("jsonwebtoken");

app.post("/signup", async (req, res) => {
    const { username, password } = req.body;
    const hashedPassword = await bcrypt.hash(password, 10);

    // Save user with hashedPassword to DB (example only)
    const user = { id: 1, username, password: hashedPassword };

    res.status(201).json({ message: "User created", user });
});

```

## Login Flow (Generate Token)

```js

app.post("/login", async (req, res) => {
    const { username, password } = req.body;

    // Fetch user from DB (example)
    const user = { id: 1, username: "john", password: "$2a$10$..." };

    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) return res.status(401).json({ error: "Invalid credentials" });

    const token = jwt.sign({ userId: user.id }, "secretKey", { expiresIn: "1h" });
    res.json({ message: "Login successful", token });
});

```

## Protect Routes with JWT

```js

function authMiddleware(req, res, next) {
    const token = req.headers.authorization?.split(" ")[1];
    if (!token) return res.status(401).json({ error: "No token provided" });

    try {
        const decoded = jwt.verify(token, "secretKey");
        req.user = decoded;
        next();
    } catch (err) {
        res.status(401).json({ error: "Invalid token" });
    }
}

app.get("/dashboard", authMiddleware, (req, res) => {
    res.send("Welcome to Dashboard!");
});

```

## 2. Sessions & Cookies

Sessions store user data on the server; cookies store data in the browser.

### Install Packages

```js
npm install express-session cookie-parser

```

```js
const session = require("express-session");
const cookieParser = require("cookie-parser");

app.use(cookieParser());
app.use(session({
    secret: "mySecret",
    resave: false,
    saveUninitialized: true
}));

app.get("/set-session", (req, res) => {
    req.session.username = "John";
    res.send("Session Set!");
});

app.get("/get-session", (req, res) => {
    res.send(`Hello ${req.session.username}`);
});
```

### 3. Role-Based Access Control (RBAC)

Assign roles like admin, user, manager and allow access based on roles.

#### Example:

```js
function roleMiddleware(roles) {
    return (req, res, next) => {
        const userRole = req.user.role; // Assume role from JWT payload
        if (!roles.includes(userRole)) {
            return res.status(403).json({ error: "Access denied" });
        }
        next();
    };
}

app.get("/admin", authMiddleware, roleMiddleware(["admin"]), (req, res) => {
    res.send("Welcome Admin!");
});
```

### 4. Summary Table

| Concept            | Description                              |
|--------------------|------------------------------------------|
| JWT                | Stateless authentication with tokens     |
| Sessions & Cookies | Server-side session storage               |
| Role-based Access   | Restrict access based on user roles       |
| Middleware          | Used for auth & role checks               |

