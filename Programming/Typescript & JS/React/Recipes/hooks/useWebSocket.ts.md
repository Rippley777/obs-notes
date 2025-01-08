
# V2 
```
import { useState, useEffect, useCallback } from 'react';

// Define a type for the message handling function
type SendMessageFunction = (message: string) => void;

// Define the shape of the hook's return value
interface WebSocketHook {
    socket: WebSocket | null;
    messages: string[];
    status: string;
    sendMessage: SendMessageFunction;
}

function useWebSocket(url: string): WebSocketHook {
    const [socket, setSocket] = useState<WebSocket | null>(null);
    const [messages, setMessages] = useState<string[]>([]);
    const [status, setStatus] = useState<string>('disconnected');

    useEffect(() => {
        // Create WebSocket connection.
        const ws = new WebSocket(url);

        // Connection opened
        ws.onopen = () => {
            console.log('WebSocket connection opened.');
            setStatus('connected');
        };

        // Listen for messages
        ws.onmessage = (e: MessageEvent) => {
            console.log('Message from server ', e.data);
            setMessages(prevMessages => [...prevMessages, e.data]);
        };

        // Listen for errors
        ws.onerror = (e: Event) => {
            console.error('WebSocket encountered error: ', e);
            setStatus('error');
        };

        // Connection closed
        ws.onclose = (e: CloseEvent) => {
            console.log('WebSocket connection closed: ', e.code, e.reason);
            setStatus('disconnected');
        };

        // Set WebSocket in state
        setSocket(ws);

        // Cleanup function
        return () => {
            ws.close();
        };
    }, [url]);

    // Function to send messages
    const sendMessage: SendMessageFunction = useCallback((message: string) => {
        if (socket && socket.readyState === WebSocket.OPEN) {
            socket.send(message);
        }
    }, [socket]);

    return { socket, messages, status, sendMessage };
}

export default useWebSocket;

```


## Usage

```
import React from 'react';
import { View, Text, Button } from 'react-native';  // Assuming using React Native components

import useWebSocket from './hooks/useWebSocket';

const WebSocketComponent: React.FC = () => {
    const { messages, sendMessage, status } = useWebSocket('ws://example.com/socket');

    return (
        <View>
            <Text>Status: {status}</Text>
            {messages.map((message, index) => (
                <Text key={index}>{message}</Text>
            ))}
            <Button title="Send Message" onPress={() => sendMessage('Hello Server!')} />
        </View>
    );
};

export default WebSocketComponent;


```

## Advanced Notes

#### **Environment-Specific Code**: 
If there are parts of the hook or components that need to be different depending on the platform (web vs. mobile), you can handle these differences inside the hook or use platform-specific files (like `.native.js` and `.js`) to define environment-specific implementations.



### History: V1
```
import { useState, useEffect, useCallback } from 'react';

function useWebSocket(url) {
    const [socket, setSocket] = useState(null);
    const [messages, setMessages] = useState([]);
    const [status, setStatus] = useState('disconnected');

    useEffect(() => {
        // Create WebSocket connection.
        const ws = new WebSocket(url);

        // Connection opened
        ws.onopen = () => {
            console.log('WebSocket connection opened.');
            setStatus('connected');
        };

        // Listen for messages
        ws.onmessage = (e) => {
            console.log('Message from server ', e.data);
            setMessages(prevMessages => [...prevMessages, e.data]);
        };

        // Listen for errors
        ws.onerror = (e) => {
            console.error('WebSocket encountered error: ', e.message);
            setStatus('error');
        };

        // Connection closed
        ws.onclose = (e) => {
            console.log('WebSocket connection closed: ', e.code, e.reason);
            setStatus('disconnected');
        };

        // Set WebSocket in state
        setSocket(ws);

        // Cleanup function
        return () => {
            ws.close();
        };
    }, [url]);

    // Function to send messages
    const sendMessage = useCallback((message) => {
        if (socket && socket.readyState === WebSocket.OPEN) {
            socket.send(message);
        }
    }, [socket]);

    return { socket, messages, status, sendMessage };
}

export default useWebSocket;

```
