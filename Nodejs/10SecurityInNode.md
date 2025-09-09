## 1. Environment Variables with dotenv

- Store sensitive data like DB passwords, API keys in .env file.

- Use dotenv to load variables into process.env.

#### Example:

```js
require('dotenv').config();
const dbPassword = process.env.DB_PASSWORD;

```

## 2. Helmet Middleware for Security Headers

- Adds secure HTTP headers to protect from attacks.

- Commonly used in Express apps.
#### Example:

```js
const helmet = require('helmet');
app.use(helmet());
```

## 3. Preventing Attacks

- SQL Injection: Use parameterized queries or ORM (like Sequelize).

```js
db.query("SELECT * FROM users WHERE id = ?", [userId]);
```

- XSS (Cross-Site Scripting): Use libraries like xss-clean or sanitize inputs.

```js
const xss = require('xss-clean');
app.use(xss());
```
- CSRF (Cross-Site Request Forgery): Use csurf middleware.
```js
const csurf = require('csurf');
app.use(csurf());
```
## 4. CORS Handling

- CORS (Cross-Origin Resource Sharing) allows secure API calls from other domains.

### Example:

```js

const cors = require('cors');
app.use(cors({ origin: "http://example.com" }));

```