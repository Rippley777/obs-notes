
STUN (Session Traversal Utilities for NAT) and TURN (Traversal Using Relays around NAT) servers are essential components used in the establishment of peer-to-peer (P2P) connections through NAT (Network Address Translation) firewalls, commonly found in WebRTC applications like video conferencing, live streaming, and online gaming. These servers help to facilitate the connection between devices in different networks or behind NATs.

### [[STUN Server]]


### [[TURN Server]]

### Usage in WebRTC

In WebRTC, both STUN and TURN servers are specified in the ICE (Interactive Connectivity Establishment) configuration, which is part of the session description protocol used during the connection establishment. For example

```javascript
const pcConfig = {
  iceServers: [
    {
      urls: 'stun:stun.l.google.com:19302'  // Google's public STUN server
    },
    {
      urls: 'turn:turn.example.com:3478',  // TURN server
      username: 'user',                   // TURN username
      credential: 'pass'                  // TURN credential
    }
  ]
};

const pc = new RTCPeerConnection(pcConfig);

```

In this configuration:

- **STUN server** is used to get the public IP.
- **TURN server** is included as a fallback to relay traffic if direct P2P communication fails.

Using both STUN and TURN servers maximizes the likelihood that peers in a WebRTC application can establish a reliable and efficient connection, despite potential obstacles like firewalls and NATs. This is particularly important in applications where real-time connectivity and data flow are critical, such as in video conferencing or collaborative platforms.
