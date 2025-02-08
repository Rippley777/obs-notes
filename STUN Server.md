
A **STUN server** allows clients (typically web browsers or other endpoints in a WebRTC application) to discover their public IP address and the type of NAT they are behind. This information is used to enable NAT traversal by letting the peers know how to reach each other over the internet. Here’s how it works:

1. **Discovery**: The client sends a request to a STUN server, which is located on the public internet.
2. **Response**: The STUN server examines the incoming request and responds with the public IP address and port of the client as seen from the server’s perspective.

This process helps each client to know its own external (public) address, which is crucial for setting up a direct P2P connection if possible.