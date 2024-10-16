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

### Two different Network methods

- Deterministic Networks (e.g., Token Ring) : Devices wait for a turn to transmit using a token-passing method.

- Contention-Based Networks (Ethernet) : Devices can transmit data whenever the network is clear, which can result in collisions.

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

VLAN is a logical subdivision of a given network that segments into separate broadcast domains. The logical grouping of devices is achieved through a software configuration. When we use VLANs, we can consolidate all four of those switches into just two switches.

VLANs operate at the layer two or the data link layer of the OSI model. Whenever a switch is configured to utilize a VLAN, it will tag each frame of data with a VLAN ID as it passes through the switch.

Reasons for using VLAN

1. Enhanced security because segmenting the networks into VLANs allows sensitive data to be isolated to reduce data breaches
2. Improved performance because VLAN reduces the size of a broadcast domain helps to decrease the amount of traffic begin sent over that segment
3. Increased management because VLAN provides greater control over the management of networks to implement policy changes and troubleshoot issue
4. Improved cost efficiency because VLAN allows us to better utilize our existing network infrastructure by breaking it up into smaller logical segments

Effective VLANs must maintain a VLAN database that contains all of the VLAN configurations for a particular switch.

Switch Virtual Interface (SVI) allows switching to route traffic between different VLANs without requiring/buying a separate router. It provides layer three or network layer processing to the VLAN. By configuring a SVI for the VLAN, the switch can handle the routing decision for any data within that VLAN.

Cisco switch - VLAN.DAT

## VLAN Configuration

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

Network Access Control (NAC) is a security mechanism used to **ensure that devices connecting to a network meet specific security requirements**. It acts as a gatekeeper, inspecting devices for compliance before granting them access, similar to customs at an airport. Here’s an overview of key NAC concepts:

1. Device Inspection

   - Devices are inspected upon trying to connect to the network.
   - If they meet security criteria, they gain access; otherwise, they may be quarantined for remediation.

2. NAC Components

   - Port Security: Limits physical devices that can connect to network ports. Port security mechanism can be configured to allow only specific MAC addresses to access a port.
   - MAC Filtering: Controls access based on a device’s MAC address (using allowlists or blocklists). Block-listing is considered less secure than allowlisting.
   - 802.1x Authentication: Ensures only authenticated users can access the network using usernames, passwords, certificates, etc. This protocol works by encapsulating the extensible authentication protocol, also known as EAP within the network's frames. It involves three components:

     - Supplicant is a user device that's seeking to access the network.
     - Authenticator is the network device the user wants to connect to like switches or a wireless access point.
     - Authentication server is a server on the network that will authenticate the user's device's username, password, smart card, or digital certificate.

3. Implementation in Organizations

   - Employees can connect company or personal devices, which must comply with the organization's security policies.
   - Persistent or Non-Persistent Agents are used to assess device compliance:
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

- MTU Definition: The largest size of a data packet (frame) that can be sent over a network, measured in bytes.

- Impact: Affects network performance and efficiency. A properly set MTU avoids packet loss and excessive overhead.

1. Common MTU Sizes

   - Wired Ethernet: 1500 bytes (default, balances efficiency and compatibility).
   - Wireless Networks: Often smaller (~1420 bytes) to handle instability and higher error rates.
   - VPN/PPPoE: Smaller MTU (1400–1450 bytes) to accommodate overhead from encapsulation.
   - Jumbo Frames: Typically 9000 bytes, used in high-bandwidth environments like data centers or for large file transfers.

2. Considerations

   - Jumbo Frames: Boost efficiency but require network devices to support them. Improper configuration leads to packet fragmentation, latency, and troubleshooting difficulties.

   - Real-World Use: Configure different MTUs for wired, wireless, VPN, and high-speed network segments to optimize performance.
