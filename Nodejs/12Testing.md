## Testing
### 1. Unit Testing

- Tests individual functions or modules.

- Popular tools: Jest and Mocha.

#### Example with Jest

```js
// sum.js
function sum(a, b) {
    return a + b;
}
module.exports = sum;

// sum.test.js
const sum = require('./sum');
test('adds 1 + 2 = 3', () => {
    expect(sum(1, 2)).toBe(3);
});
```
Run:
```js
npx jest
```
### 2. API Testing

- Tests API endpoints for correct response.

- Tools: Postman (manual), Supertest (automated).

#### Example with Supertest

```js

const request = require('supertest');
const app = require('./app'); // your Express app

describe('GET /users', () => {
    it('should return all users', async () => {
        const res = await request(app).get('/users');
        expect(res.statusCode).toBe(200);
    });
});

```