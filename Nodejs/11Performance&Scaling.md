## 1. Clustering in Node.js

- Node.js is single-threaded.

- Clustering allows using all CPU cores to handle more requests.

- cluster module helps run multiple instances.

#### Example:

```js
const cluster = require('cluster');
const os = require('os');
const totalCPUs = os.cpus().length;

if (cluster.isMaster) {
    for (let i = 0; i < totalCPUs; i++) cluster.fork();
} else {
    // Start your server here
    console.log(`Worker ${process.pid} started`);
}
```

## 2. Load Balancing Basics

- Distributes incoming traffic across multiple servers.

- Prevents one server from being overloaded.

- Tools: NGINX, HAProxy, AWS ELB, Cloud Load Balancers.

## 3. Caching with Redis or Memory Caching

- Caching stores frequently used data temporarily to serve it faster.

- Redis: In-memory data store, supports persistence.

- Memory Cache: Stored directly in app memory, good for small-scale apps.

#### Example with Redis:

```js
const redis = require('redis');
const client = redis.createClient();

client.set('key', 'value');
client.get('key', (err, data) => console.log(data));
```