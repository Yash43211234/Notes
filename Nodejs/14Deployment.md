## 1. Running Node.js apps on servers (PM2)

- PM2 = Process Manager for Node.js

- Keeps the app running 24/7, handles restarts if app crashes.

#### Install & Run

```js

npm install -g pm2
pm2 start app.js        # Start app
pm2 status              # Check status
pm2 restart app.js      # Restart app
pm2 stop app.js         # Stop app
pm2 logs                # Show logs

```

### 2. Environment setup for production

- Use .env file to store secrets (e.g., DB password).

- Example:

#### .env

```js
PORT=3000
DB_URL=mongodb://localhost:27017/mydb
```
#### app.js
```js
require('dotenv').config();
const port = process.env.PORT;
```

- Use NGINX for reverse proxy and load balancing.

### 3. CI/CD basics with GitHub Actions

- CI/CD = Continuous Integration / Continuous Deployment

- Automates testing and deployment after each push.

Example GitHub Action file:
.github/workflows/node.js.yml

```js
name: Node.js CI/CD

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm test
```
