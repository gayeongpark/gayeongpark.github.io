---
layout: post
title: Comptia network+ certification
subtitle: Preparing for Comptia network+ - Network Fundamentals
tags: [network, comptia, fundamentals]
comments: true
author: Lantana Park
---

# Network fundamentals

## Network Components

### What does the networks actually consist of?

- Client : Devices that users access the network with.

- Server : Provide resources/services to the network.

- **Hubs** : Are older network devices that connect other devices like clients and servers over **a local area network**.

![hubImage](../assets/img/networkFundamental/What-is-a-Computer-Network-Hub-Diagram.jpg)

They are simple devices that broadcast incoming data packets to all connected devices, so if two devices send data simultaneously, a collision occurs, and the data must be resent. Thus this can lead to network inefficiencies.

Moreover, Hubs lack any form of security features, so data is indiscriminately sent to all devices, which can be a security risk.

- **Bridges** : Are network devices used to connect and filter traffic between two or more LAN segments within a local area network.

Bridges use MAC addresses to forward data only to the appropriate segment. By doing so, they help reduce network collisions by creating separate collision domains for each segment. Bridges also play a crucial role in segmenting large networks into smaller, more manageable sections, enhancing performance and security. However, bridges do not have the advanced features of modern switches and are less scalable for larger networks.

- **Switches** : Are much smarter version of hub. They provides more security and more efficient bandwidth utilization. Because they forward traffic from one port to the intended destination port. And They can receive and analyze the data packets from devices on the network in order to determine the correct destination.

They forward traffic from one port to the intended destination port based on the MAC address of the devices, which eliminates unnecessary data transmission and significantly reduces collisions.

- **Wireless Access Points (WAPs/APs)** : Allow wireless devices to connect to a wired network. They are used to broadcast data, that means a data packet is sent from one device to all other devices on the same network segment, over a radio frequency wave.

- **Routers** : are a crucial component in the modern networks because they are used to connect different networks together. They can forward data based on the IP addresses of the clients, servers, and other devices over the network.

Modern routers predominantly rely on the internet protocol to route the traffic across the network using many different types of routing protocols.

- **Firewalls** : serve as security barriers between internal networks and the external world. They can monitor incoming and outgoing network traffic based upon predetermined security rules by using Access Control Lists(ACL).

It helps protect our network from unauthorized access, cyber attacks, and other online threats. Firewalls can be either hardware based, software based, or a combination of both of these.

- **Load Balancers** : are can be devices or software that distribute network or application traffic across multiple servers. These increase efficiency, capacity, and reliability of the services by ensuring that no single server is going to bear too much of that demand.

So Load balancers prevent any one server from becoming a bottleneck, improving overall network performance.

- **Proxy** : Acts as an intermediary between a user's device and the internet.

It provides functionalities including web filtering, shared network connections, data caching to improve overall performance, and enhanced security and privacy by hiding the user's real IP address and limiting their exposure to the internet.

- **Intrusion Detection Systems (IDS)** : Are to detect unauthorized access or anomalies malicious access and alert administrators. The IDS is a listen-only device.

- **Intrusion Prevention Systems (IPS)** : Are not only detect threats, but also take action to prevent intrusion like blocking that traffic from entering network or dropping any kind of harmful packets.

- **Security Information Management (SIM)** : Involves the collection, storage, and analysis of log data from various sources across an organization's IT infrastructure. SIM helps in identifying long-term trends and providing reports that aid in compliance and auditing.

- **Security Event Management (SEM)** : Focuses on real-time monitoring and correlation of events across the network, allowing security teams to detect and respond to potential threats more quickly.

- **Controllers** : Are central units used to manage flow control to networking devices. This enables administrators to dictate the behavior of the network switches and routers through software and this gives us more flexibility and efficiency.

- **Network-Attached Storage (NAS) Device**: Dedicated file storage system that provides data access to a heterogeneous group of clients.

- **Media** : Refers to the physical materials used to transmit data.

- **Wide Area Network (WAN) Link** : Used to connect networks over large geographical areas.

## Network resources

- Client-Server Model : Used a server to access to network resources (files, scanners, printers, etc.)

It is a leading model we use in business networks.

Pros,

1. This network model serves centralized administration.
2. It is easier management.
3. It has better scalability.

Cons,

1. It costs more money because it requires dedicated hardware, software, or OS.
2. It requires specialized skill-set to run all those things.

- Peer-to-Peer Model : Peers or other machines can share resources together directly.

The administration and backup is very difficult because all the files are located on different machines in different places. So it can occur redundancy.

### Where the Peer-to-Peer useful?

Each person of the network have and received files. 

Pros,
1. There is lower costs because there is no dedicated hardware.
2. There is no specialized OS or dedicated resources.

Cons,
1. It is decentralized management system.
2. It is extremely inefficient for large networks. 
3. It has poor scalability.

## Network Geography

- Personal Area Network (PAN)

Smallest type of wired or wireless network which usually covers a distance about 10 feet or less




