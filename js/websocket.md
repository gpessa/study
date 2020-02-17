## WebSocket

The WebSocket object provides the API for creating and managing a WebSocket connection to a server, as well as for sending and receiving data on the connection.
WebSockets provide a persistent connection between a client and server that both parties can use to start sending data at any time. The client establishes aWebSocket connection through a process known as the WebSocket handshake. This process starts with the client sending a regular HTTP request to the server.

#### How to use it

```js
// Create WebSocket connection.
const socket = new WebSocket("ws://localhost:8080");
```

```js
// Connection opened
socket.addEventListener("open", function(event) {
  socket.send("Hello Server!");
});
```

```js
// Listen for messages
socket.addEventListener("message", function(event) {
  console.log("Message from server ", event.data);
});
```

```js
// Message sent to the server
socket.send("Hello Server!");
```
