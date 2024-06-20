# WebSockets

🌐 WebSockets enable real-time, two-way communication between a client and server over a single, persistent connection. They offer lower latency and reduced overhead compared to HTTP. Perfect for chat apps, live updates, and IoT devices.

## Key Features of WebSockets

1. **Full-Duplex Communication:** Enables simultaneous sending and receiving of messages.
2. **Persistent Connection:** Maintains an open connection for continuous data exchange.
3. **Lower Latency:** Reduces latency compared to HTTP.
4. **Lightweight Headers:** Smaller headers reduce the amount of data transmitted.

## How WebSockets Work

1. **Handshake:** 
    - Starts with an HTTP request from the client to the server to establish a WebSocket connection.
    - Example of an HTTP upgrade request:
    ```http
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Sec-WebSocket-Version: 13
    ```
    - If the server supports WebSockets, it responds with an HTTP 101 status code, indicating the protocol switch:
    ```http
    HTTP/1.1 101 Switching Protocols
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
    ```

2. **Data Frames:**
    - After the handshake, the connection is established, and data can be sent in both directions.

## Example

### 💻 Client-Side Code
```javascript
const socket = new WebSocket('ws://example.com/chat');

socket.onopen = function(event) {
    console.log('WebSocket is open now.');
    socket.send('Hello Server!');
};

socket.onmessage = function(event) {
    console.log('Received:', event.data);
};

socket.onclose = function(event) {
    console.log('WebSocket is closed now.');
};

socket.onerror = function(error) {
    console.log('WebSocket Error:', error);
};


🖥️ Server-Side Code (Node.js)

const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
    ws.on('message', function incoming(message) {
        console.log('received:', message);
        ws.send('Hello Client!');
    });

    ws.send('Welcome to the chat server!');
});
