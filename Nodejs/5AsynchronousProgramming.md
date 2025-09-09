# Asynchronous Programming in Node.js

Asynchronous programming allows tasks to **run in the background** without blocking the main thread.

---

## 1. Callbacks

A **callback** is a function passed as an argument to another function, executed after the task completes.

### Example:
```js
function fetchData(callback) {
    setTimeout(() => {
        callback("Data fetched!");
    }, 1000);
}

fetchData((msg) => {
    console.log(msg);
});
```

## Pros:

- Simple for small tasks.

- Works well for basic async operations.

## Cons:

- Leads to Callback Hell when nested.

- Difficult to maintain and debug.

## 2. Promises

Promises represent a value that may be available now, in the future, or never.

### Example:

```js 

const fetchData = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Data fetched!");
    }, 1000);
});

fetchData
    .then((msg) => console.log(msg))       // Success
    .catch((err) => console.log(err))      // Error
    .finally(() => console.log("Done"));   // Always runs

```

## 3. async/await

async/await makes asynchronous code look synchronous and easy to read.

### Example:

```js

function getData() {
    return new Promise((resolve) => {
        setTimeout(() => resolve("Data fetched!"), 1000);
    });
}

async function showData() {
    try {
        const data = await getData();
        console.log(data);
    } catch (err) {
        console.log("Error:", err);
    }
}

showData();
```

## 4. Callback Hell & How to Avoid It
Callback Hell Example:

```js

doTask1(() => {
    doTask2(() => {
        doTask3(() => {
            console.log("All tasks done!");
        });
    });
});

```

### How to Avoid:

- Use Promises → then(), catch()

- Use async/await → Cleaner, more readable code

- Use libraries like async.js

## Comparison Table
- Concept	- Syntax Style	- Error Handling	- Readability
- Callbacks	- Nested functions	- Manual try-catch	- Harder (Callback Hell)
- Promises	- then(), catch(), finally	- Built-in -	Moderate
- async/await	- async function + await -	try-catch blocks	- Easy & Clean