---
layout: post
title: TCM - practice for the bash script
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by making socket, port scanner, and simple malware(ransomware) using node.js and python
tags: [ethical hacking, tcm, pjpt, port scanner, malware]
comments: true
author: Lantana Park
---

# Socket

Sockets are the fundamental networking concept used for communication between computers over a network.

In this python example,

```python
#!/bin/python3
import socket # Import the socket module

HOST = '127.0.0.1' # Define host ip address (my ip address)
PORT = 7777 # Specify the port number on the server where the server is listening for incoming connections

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# `socket.AF_INET` is to set this socket to use IPv4 addresses for communication
#  `socket.SOCK_STREAM` is to create TCP (Transmission Control Protocol)
s.connect((HOST,PORT))
# Establish the connection to the server with these arguments
```

1. Made the py file to be ready for serving.

![ready](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2016.02.38.png)

2. And then initiated `nc` for TCP client to the specified host and port.

![ready](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2016.07.23.png)

3. Lastly, established successful connection.

![established](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2016.03.12.png)

![nc](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2016.03.07.png)

In this node.js example,

```javascript
const net = require("net"); // Import net module for TCP networking with node.js

const HOST = "127.0.0.1"; // Define host ip address (my ip address)
const PORT = 7777; //Specify the port number on the server where the server is listening for incoming connections

const client = new net.Socket(); // Create a new TCP socket object

// Connect to the server
client.connect(PORT, HOST, () => {
  console.log("Connected to server");
  // Send data to the server after connection is established
  client.write("Hello, server!");
});

// Event handling for receiving data from the server
client.on("data", (data) => {
  console.log(`Server echoed: ${data}`); // Log the data received from the server
  client.destroy(); // Close the client socket completely after receiving the data
});

// Event handling for close server
client.on("close", () => {
  console.log("Connection closed");
}); // Log when connection is closed

// Event handling for errors
client.on("error", (err) => {
  console.error(`Error: ${err.message}`);
}); // Log any errors
```

1. Made the js file to be ready for serving.

![ready](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2015.55.36.png)

2. And then initiated `nc` for TCP client to the specified host and port.

![ready](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2016.07.23.png)

3. Lastly, established successful connection

![established](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2015.50.19.png)

![final](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2015.50.09.png)

Applications of Socket Communication

- Web Servers: Serve web pages to clients (browsers).
- Chat Applications: Enable real-time text communication.
- File Transfer: Transfer files between devices.
- IoT Devices: Communicate between sensors, controllers, and cloud services.
- Remote Procedure Calls (RPC): Allow functions to be executed on remote machines.
