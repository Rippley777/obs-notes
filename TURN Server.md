Sometimes, NAT configurations or firewall policies may prevent a direct P2P connection, even after the STUN process. This is where a **TURN server** comes into play:

1. **Relay**: If direct communication fails, the TURN server acts as an intermediary that relays data between the WebRTC clients. Unlike STUN, TURN is used when the peers cannot communicate directly with each other.
2. **Traffic Handling**: All traffic in a TURN scenario flows through the TURN server, which can increase latency and load on the TURN server but ensures that communication is possible even in stringent network environments.
