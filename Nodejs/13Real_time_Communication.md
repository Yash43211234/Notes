## Real-time Communication
### 1. WebSockets Basics with socket.io

- WebSockets: Allow two-way real-time communication between client & server.

- socket.io makes it easy to use WebSockets in Node.js.

#### Example

```js
// server.js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);

io.on('connection', (socket) => {
    console.log('New client connected');
    socket.emit('welcome', 'Hello Client!');

    socket.on('message', (msg) => {
        console.log('Message from client:', msg);
    });
});

server.listen(3000, () => console.log('Server running on port 3000'));

```

### 2. Event-driven Communication

- Uses events to handle messages asynchronously.

- Works like on (listen) and emit (send).

#### Example

```js

const EventEmitter = require('events');
const event = new EventEmitter();

event.on('greet', (name) => {
    console.log(`Hello ${name}`);
});

event.emit('greet', 'Yashwant');

```
