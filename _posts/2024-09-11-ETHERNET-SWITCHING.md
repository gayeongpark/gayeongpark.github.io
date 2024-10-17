---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ | Ethernet Switching
tags: [network, compTia, fundamentals, ethernet, switching]
comments: true
author: Lantana Park
---

# Ethernet Switching

It is focused heavily on the second layer of the OSI model because layer two - Data Link Layer is where switching occurs within a local area network when we are using ethernet.

## Ethernet Fundamentals

Early networking technologies were diverse, including Ethernet, Token Ring, LocalTalk, AppleTalk, and others. Over time, Ethernet emerged as the dominant Layer 2 protocol, used widely in local area networks (LANs).

Initially, Ethernet used coaxial cables (10Base2 and 10Base5), which allowed for long distances but were eventually replaced by **10Base-T Ethernet** using **twisted-pair cables** known as category 3 or CAT 3 with **RJ-45 connectors**. 10Base-T could transmit data at **10 Mbps** over a maximum distance of **100 meters**.

### Two different Network methods

- Deterministic Networks (e.g., Token Ring) : Means that the network access should be very organized and orderly.

- Contention-Based Networks (Ethernet) : Used to determine who gets to access and communicate on the network at any given time.

How to prevent collision?

1. CSMA/CD : Carrier Sense Multiple Access with Collision Detection helps manage collisions by having devices listen to the network before transmitting and stop when a collision occurs.

2. Collision Domains and Network Efficiency : A network segment where data collisions can occur. As networks grow, more devices can cause more collisions, reducing efficiency. I need to keep collision domains small inside networks. Switches/bridges help segment networks into smaller collision domains, enabling more efficient data transmission and supporting full-duplex communication.

## Network Devices

1.  Hubs

    - Layer 1 Device : Physical device, known as a multi-port repeater.
      ### Types
      - Passive Hub : Repeats signals without amplification.
      - Active Hub : Boosts signal, extending cable distances (resets 100-meter twisted pair limit).
      - Smart Hub : Adds management features (e.g., SNMP).
    - Collision Domains : Hubs connect multiple devices, extending a single collision domain, increasing the chance of collisions in large networks.

2.  Bridges

    - Layer 2 Device : Used to segment networks, breaking up collision domains by filtering traffic based on MAC addresses.
    - Collision Domains : Bridges break collision domains but maintain one broadcast domain.

3.  Switches

    - Layer 2 Device : Similar to a multi-port bridge, connects multiple segments and manages traffic using MAC addresses.
    - Collision Domains : Each port on a switch represents a unique collision domain, enhancing network efficiency by preventing collisions.
    - Broadcast Domains : Switches operate within a single broadcast domain.
    - Switching Logic : Learns MAC addresses on each port, forwards data only to the appropriate port, minimizing unnecessary traffic.

4.  Routers

    - Layer 3 Device : Connects different networks and makes forwarding decisions based on IP addresses(IPv4, IPv6).
    - Collision and Broadcast Domains : Each router port has a separate collision and broadcast domain.
    - Functionality : Routers handle different types of networks and interface types (e.g., RJ45, fiber, serial), making routing decisions between internal LANs and external networks (e.g., the internet).

5.  Layer 3 Switches (Multilayer Switches)

    - Layer 3 Device : Combines the functionality of switches and routers.
    - Routing : Capable of performing routing functions and breaking up broadcast domains, making them ideal for internal network routing.
    - Efficiency : Suitable for smaller networks but less efficient than dedicated routers for large-scale routing.

Device Type | Collision Domains | Broadcast Domains | OSI Layer
Hub | 1 | 1 | 1
Bridge | 1 per port | 1 | 2
Switch | 1 per port | 1 | 2
Multilayer Switch | 1 per port | 1 per port | 3+
Router | 1 per port | 1 per port | 3+

## Virtual Local Area Network (VLAN)

A VLAN is a logical segmentation of a network, used to create separate broadcast domains within the same physical network infrastructure. Devices in the same VLAN can communicate with each other as if they were on the same network, even if they are physically connected to different switches. VLANs operate at Layer 2 (Data Link Layer) of the OSI model, and they allow for better network segmentation and control.

When VLANs are implemented, each frame of data is tagged with a VLAN ID, ensuring that traffic from different VLANs remains separate.

VLAN (Virtual Local Area Network) is a type of network configuration used in Ethernet networks.

### Reasons for using VLAN

1. Enhanced Security: VLANs allow sensitive data to be isolated. For example, separating the HR department from the Finance department can help protect confidential data and reduce security risks.

2. Improved Performance: By reducing the size of the broadcast domain, VLANs help minimize broadcast traffic, improving the overall performance of the network.

3. Simplified Management: VLANs provide greater control over the network, enabling easier policy implementation, segmentation, and troubleshooting.

4. Cost Efficiency: VLANs allow more efficient use of existing infrastructure by creating logical segments, reducing the need for additional physical hardware.

### VLAN Configurations

- VLAN Database : Each switch maintains a VLAN database that holds all VLAN configurations, allowing for easy management and identification of the VLANs associated with the switch.

- Switch Virtual Interface (SVI) : An SVI enables inter-VLAN routing, allowing traffic to be routed between VLANs without the need for an external router. The switch can perform Layer 3 (Network Layer) operations for the VLAN, making it capable of routing traffic within and between VLANs.

- Cisco VLAN.DAT : On Cisco switches, VLAN configurations are stored in a file called VLAN.DAT. It is important for maintaining the integrity of the VLAN configuration.

### Key VLAN Concepts

- 802.1Q Tagging : A VLAN tagging standard that adds VLAN IDs to Ethernet frames, helping manage multiple VLANs on the same physical network infrastructure(Trunking). This ensures data separation between different departments (e.g., HR and finance) by tagging their traffic for secure, isolated communication.

- Trunking : The transmission of traffic from different VLANs across the same physical network infrastructure, while keeping the traffic from each VLAN separate and secure.

- Native VLAN : The default VLAN on a trunk port, used for untagged traffic. It's crucial for legacy devices that don’t support VLAN tags. Ensuring consistent native VLAN configurations across switches helps avoid traffic mis-routing. Cybersecurity experts recommend renaming the default VLAN(VLAN10 or VLAN100) to prevent VLAN hopping attacks.

- Voice VLAN : A dedicated VLAN for Voice over IP (VoIP) traffic, prioritizing voice data over regular traffic to maintain high-quality communications. This reduces latency, jitter, and packet loss for critical voice calls in business environments.

- Link Aggregation : A method of combining multiple network connections into one logical link, increasing bandwidth and providing redundancy. This is often used in data centers to prevent network bottlenecks and ensure high-speed connectivity.

- Speed and Duplex Configurations : These settings control data transmission speed (in Mbps or Gbps) and whether data is sent and received simultaneously (full duplex) or alternately (half duplex). Misconfigurations can reduce performance, and auto-negotiation may sometimes select lower-than-optimal speeds, requiring manual adjustments.

## Spanning Tree Protocol (STP) / 802.1d

It defined by IEEE standard 802.1d, it **prevents loops in network traffic** by allowing redundant links between switches. Without STP, switching loops can lead to broadcast storms that overwhelm the network.

- Key Concepts

  - Root Bridge : The switch with the lowest Bridge ID (based on priority value and MAC address) is elected as the root bridge.
  - Non-Root Bridges : All other switches in the topology.
  - Root Port : Each non-root bridge has a root port, the one closest to the root bridge in terms of cost (lower cost = faster link).
  - Designated Ports : Ports on each network segment closest to the root bridge, forwarding traffic. All the ports on root bridge are designated ports.
  - Non-Designated Ports : Block traffic to prevent loops.

- Port States : STP ports transition through blocking, listening, learning, and forwarding states, ensuring loop-free topologies.

- Link Cost : Faster links have lower costs. For example, Cat 3 (10 Mbps) has a higher cost than Cat 5 (100 Mbps), and fiber (10 Gbps) has an even lower cost. **faster links = lower cost, slower links = higher cost**

**STP ensures loop-free network operations while maintaining redundancy for high availability**.

## Network Access Control (NAC)

Network Access Control (NAC) is a security mechanism used to **ensure that devices connecting to a network meet specific security requirements**. NAC is effectively implemented in switches to enforce security policies and control access to the network. It acts as a gatekeeper, inspecting devices for compliance before granting them access, similar to customs at an airport.

1. Device Inspection

   - Devices are inspected upon trying to connect to the network.
   - If they meet security criteria, they gain access; otherwise, they may be quarantined for remediation.

2. NAC Components

   - Port Security : Limits physical devices that can connect to network ports. Port security mechanism can be configured to allow only specific MAC addresses to access a port.

   - MAC Filtering : Controls access based on a device’s MAC address (using allowlists or blocklists). Block-listing is considered less secure than allowlisting.

   - 802.1x Authentication : Ensures only authenticated users can access the network using usernames, passwords, certificates, etc. This protocol works by encapsulating the extensible authentication protocol, also known as EAP within the network's frames. It involves three components

     - Supplicant is a user device that's seeking to access the network.
     - Authenticator is the network device the user wants to connect to like switches or a wireless access point.
     - Authentication server is a server on the network that will authenticate the user's device's username, password, smart card, or digital certificate.

3. Implementation in Organizations

   - Employees can connect company or personal devices, which must comply with the organization's security policies.
   - Persistent or Non-Persistent Agents are used to assess device compliance.
     - Persistent Agents (on company devices) continuously monitor security compliance.
     - Non-Persistent Agents (on personal devices) perform a temporary security check.
   - When a device is connected to the network, the persistent or non-persistent agent is first going to check the MAC address and verify the device's identity.

4. Advanced Access Controls

   - Time-Based Access: Limits access during specific hours.
   - Location-Based Access: Controls access based on the physical location of the device.
   - Role-Based Access: Grants access based on the user's role within the organization. This access control is a powerful way to enforce the principle of least privilege.
   - Rule-Based Access: Uses predefined rules (e.g., devices must have antivirus installed) to grant or deny access.

5. Purpose

   - NAC enhances network security by ensuring only secure, compliant devices and users can access the network. It adapts to various scenarios, providing flexibility in enforcing security policies.

## Maximum Transmission Unit (MTU)

Maximum Transmission Unit (MTU) settings can be configured on switches.
The largest size of a data packet (frame) that can be sent over a network, measured in bytes. It affects network performance and efficiency. A properly set MTU avoids packet loss and excessive overhead.

1. Common MTU Sizes

   - Wired Ethernet : The standard MTU size is 1500 bytes. This is widely used because it strikes a good balance between efficiency and compatibility with different types of networks.

   - Wireless Networks : MTU sizes for wireless networks are often smaller, around 1420 bytes. This helps manage issues like instability and higher error rates that are common in wireless communications.

   - VPN/PPPoE : For VPN connections or Point-to-Point Protocol over Ethernet (PPPoE), the MTU is usually smaller, typically ranging from 1400 to 1450 bytes. This is necessary to account for the extra data (overhead) added during encapsulation.

   - Jumbo Frames : In specialized environments like data centers, MTUs can be increased to 9000 bytes. This is known as a Jumbo Frame and is used for transferring large files efficiently, reducing the number of packets sent over the network.

2. Considerations

   - While Jumbo Frames can enhance efficiency, all network devices must support them. If they don’t, it can lead to packet fragmentation (breaking packets into smaller pieces), increased latency (delays), and challenges in troubleshooting network issues.

   - To get the best performance, it’s important to configure MTUs appropriately based on the type of network being used (wired, wireless, VPN, etc.). This helps ensure smooth data transmission without bottlenecks or interruptions.
