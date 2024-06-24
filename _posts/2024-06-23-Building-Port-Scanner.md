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
#!/usr/bin/env node // Define interpreter
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

3. Lastly, established successful connection.

![established](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2015.50.19.png)

![final](../assets/img/PJPT/coding/Screenshot%202024-06-23%20at%2015.50.09.png)

Applications of Socket Communication

- Web Servers: Serve web pages to clients (browsers).
- Chat Applications: Enable real-time text communication.
- File Transfer: Transfer files between devices.
- IoT Devices: Communicate between sensors, controllers, and cloud services.
- Remote Procedure Calls (RPC): Allow functions to be executed on remote machines.

# Port scanner

Even though I can use some port scanning tools, like `nmap`, `pnscan`, or `netcat`, I just made my port scanning tool using node.js and python.

This port scanning tool I made is really **slow**. To make the port scanner faster, I can implement multithreading. However, in this example, I did not add the multithreading feature.

In this python example,

```python
#!/bin/python3

import sys # import `sys` to handle command-line arguments and exiting the script
import socket # import `socket` to create network connection
from datetime import datetime # import `datetime` to get the current time for making pretty banner

# Define our target
if len(sys.argv) == 2:
    # It is to check if a hostname is provided as a command-line argument
	target = socket.gethostbyname(sys.argv[1]) # Convert the provided hostname (google.com) to IPv4 address (142.250.72.110)
else:
	print("Invalid amount of arguments.")
	print("Syntax: python3 scanner.py")
    # If a hostname is not provided, It will print this log

# Add a pretty banner to indicate the start of the scan, the target, and the start time.
print("-" * 50)
print("Scanning target " + target)
print("Time started: " + str(datetime.now()))
print("-" * 50)

try:
	for port in range(0,65535):
        # Loop through all possible ports
		s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        # Create a new socket connection
		socket.setdefaulttimeout(1) # Set timeout for each port
		result = s.connect_ex((target,port)) # Attempt to connect to the current port
		if result == 0:
			print("Port {} is open".format(port))
		s.close()
        # Finally close the socket connection

except KeyboardInterrupt:
	print("\nExiting program.")
	sys.exit()
    # It is to handle Ctrl + C interruption

except socket.gaierror:
	print("Hostname could not be resolved.")
	sys.exit()
    # It is to handle invalid hostname

except socket.error:
	print("Could not connect to server.")
	sys.exit()
    # It is to handle connection errors
```

1. Made a python file above
   ![portscanningpython1](../assets/img/PJPT/coding/Screenshot%202024-06-24%20at%2022.21.40.png)

2. Started the port scanning tool for scanning my website port.
   ![portscanningpython2](../assets/img/PJPT/coding/Screenshot%202024-06-24%20at%2022.21.26.png)

![portscanningpython3](../assets/img/PJPT/coding/Screenshot%202024-06-24%20at%2022.26.31.png)

In this node.js example,

```javascript
#!/usr/bin/env node // Define interpreter

const net = require("net"); // Import the `net` module for networking capabilities such as creating servers and clients.
const dns = require("dns"); // Import the `dns` for resolving DNS resolution
const readline = require("readline"); // Import the `readline` module to handle reading from the command line.

// Get the target from command line arguments
// Retrieve command-line arguments, excluding the first two (node and script path).
// Ex, node scanner.js https://google.com, I want to slice only `https://google.com`
const args = process.argv.slice(2);

// If there is no valid hostname, the error log will be printed
if (args.length !== 1) {
  console.log("Invalid amount of arguments.");
  console.log("Syntax: node scanner.js <hostname>");
  process.exit(1);
}

// Extract only the string `https://google.com`
const target = args[0];

// Resolve the hostname to an IP address using dns lookup
dns.lookup(target, (err, address) => {
  // If there is an error, the network will be closed
  if (err) {
    console.error("Hostname could not be resolved.");
    process.exit(1);
  }
  // For pretty banner
  console.log("-".repeat(50));
  console.log(`Scanning target ${address}`);
  console.log(`Time started: ${new Date()}`);
  console.log("-".repeat(50));

  // Function to scan a single port
  const scanPort = (port) => {
    return new Promise((resolve) => {
      const socket = new net.Socket();

      // Set a timeout for the connection attempt
      socket.setTimeout(1000);

      // Attempt to connect to the target port
      socket.connect(port, address, () => {
        console.log(`Port ${port} is open`);
        socket.destroy(); // Close the connection
        resolve();
      });

      // Handle errors and timeouts
      socket.on("error", () => {
        socket.destroy();
        resolve();
      });

      socket.on("timeout", () => {
        socket.destroy();
        resolve();
      });
    });
  };

  // Function to scan all ports
  const scanAllPorts = async () => {
    for (let port = 0; port <= 65535; port++) {
      await scanPort(port);
    }
  };

  scanAllPorts()
    .then(() => {
      console.log("\nScanning complete.");
    })
    .catch((err) => {
      console.error(`Error: ${err.message}`);
    });
});
```

1. Made a python file above
   ![portscanningjavascript1](../assets/img/PJPT/coding/Screenshot%202024-06-24%20at%2022.37.38.png)

2. Started the port scanning tool for scanning my website port.
   ![portscanningpython3](../assets/img/PJPT/coding/Screenshot%202024-06-24%20at%2022.37.34.png)

# Ransomware

It is to have an experiment of creating a simple malware.
