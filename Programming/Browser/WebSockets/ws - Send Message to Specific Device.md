Here's a basic setup on how to send messages to specific connected users using `ws`:

### 1. Server Setup

Install the `ws` package if you haven't already:

bash

Copy

`npm install ws`

Set up a WebSocket server and manage connected clients:

javascript

Copy

``const WebSocket = require('ws'); const http = require('http');  const server = http.createServer(); const wss = new WebSocket.Server({ server });  const clients = new Map(); // Map to store clients with a custom identifier  wss.on('connection', function(socket) {     console.log('A user connected');      // Handle incoming messages     socket.on('message', function(message) {         console.log('Received:', message);         const msg = JSON.parse(message);          if (msg.type === 'register') {             // Register user ID with this socket             clients.set(msg.userID, socket);             console.log(`User ${msg.userID} registered`);         }     });      socket.on('close', function() {         console.log('A user disconnected');         // Remove the socket from the map on disconnect         clients.forEach((value, key) => {             if (value === socket) {                 clients.delete(key);                 console.log(`User ${key} disconnected and removed from map.`);             }         });     }); });  function sendMessageToUser(userID, message) {     const userSocket = clients.get(userID);     if (userSocket && userSocket.readyState === WebSocket.OPEN) {         userSocket.send(JSON.stringify(message));         console.log(`Message sent to user ${userID}`);     } else {         console.log(`No active connection found for user ${userID}`);     } }  const PORT = 3000; server.listen(PORT, () => {     console.log(`Server running on port ${PORT}`); });``

### 2. Client Setup

Create a simple HTML file to connect to this server and interact with it:

html

Copy

`<!DOCTYPE html> <html lang="en"> <head>     <meta charset="UTF-8">     <meta name="viewport" content="width=device-width, initial-scale=1.0">     <title>WebSocket Client</title>     <script>         const socket = new WebSocket('ws://localhost:3000');          socket.addEventListener('open', function(event) {             console.log('Connected to WS Server');             // Register this client with a user ID             socket.send(JSON.stringify({ type: 'register', userID: 'user123' }));         });          socket.addEventListener('message', function(event) {             console.log('Message from server ', event.data);         });     </script> </head> <body>     <h1>WebSocket Client</h1> </body> </html>`

### Summary

In this setup:

- The server uses a `Map` to associate user IDs with their respective WebSocket connections (`socket`).
- Clients send a registration message upon connection to link their session with a userID.
- The server listens for connections, handles incoming messages to register users, and maintains a list of active clients.
- `sendMessageToUser` function can be called on the server side to send messages to a specific user if their socket is still open.

This method using `ws` requires manual management of user IDs and their associated WebSocket connections but offers flexibility and direct control over the WebSocket communication.