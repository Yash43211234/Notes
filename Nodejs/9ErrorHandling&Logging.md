## Error Handling & Logging in Node.js
### 1. Try-Catch Blocks in Async Code

- Used to handle errors in async/await functions.

- Prevents the application from crashing due to unexpected errors.

#### Example:

```js
async function getData() {
  try {
    let data = await fetchData();  
    console.log(data);
  } catch (err) {
    console.error("Error:", err.message);
  }
}

```

### 2. Express Error-Handling Middleware

- In Express, error middleware has 4 parameters: (err, req, res, next)

- Helps catch and handle all errors in one place.

#### Example:

```js

app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send({ error: "Something went wrong!" });
});

```

### 3. Logging with Winston or Morgan

- Morgan: Logs HTTP requests.

- Winston: Advanced logging with levels (info, warn, error).

#### Example with Morgan:

```js
const morgan = require('morgan');
app.use(morgan('dev')); // Logs requests in console
```

#### Example with Winston:

```js

const { createLogger, transports } = require('winston');
const logger = createLogger({
  transports: [new transports.Console()]
});

logger.info("Server started");
```