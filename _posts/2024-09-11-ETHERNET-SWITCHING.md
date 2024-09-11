---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - ethernet switching
tags: [network, compTia, fundamentals, ethernet, switching]
comments: true
author: Lantana Park
---

# Ethernet Switching

We are going to be focused heavily on layer two of the OSI model because layer two is where switching occurs within a local area network when we are using ethernet.

## Ethernet Fundamentals

Early networking technologies were diverse, including Ethernet, Token Ring, LocalTalk, AppleTalk, and others. Over time, Ethernet emerged as the dominant Layer 2 protocol, used widely in local area networks (LANs).

Initial versions of Ethernet ran over coaxial cables, like 10Base2 (Thin Net) and 10Base5 (Thick Net). These older systems could reach distances of up to 500 meters but are no longer relevant in modern networks. The migration to 10Base-T Ethernet introduced twisted-pair cabling (e.g., CAT 3), offering 10 Mbps over 100 meters.

Two different Network methods:

- Deterministic Networks (e.g., Token Ring): Devices wait for a turn to transmit using a token-passing method.
- Contention-Based Networks (Ethernet): Devices can transmit data whenever the network is clear, which can result in collisions.

How to prevent collision?

1. CSMA/CD (Carrier Sense Multiple Access with Collision Detection):

   Devices listen (carrier sense) for network traffic before transmitting (multiple access).
   If a collision occurs, devices stop, wait for a random amount of time, and then attempt to retransmit.

2. Collision Domains and Network Efficiency:

   Collision Domain: A network segment where data collisions can occur.
   As networks grow, more devices can cause more collisions, reducing efficiency. I need to keep collision domains small inside networks.
   Switches/bridges help segment networks into smaller collision domains, enabling more efficient data transmission and supporting full-duplex communication.

## Network Devices

1.  Hubs

    - Layer 1 Device: Physical device, known as a multi-port repeater.
      Types:
      - Passive Hub: Repeats signals without amplification.
      - Active Hub: Boosts signal, extending cable distances (resets 100-meter twisted pair limit).
      - Smart Hub: Adds management features (e.g., SNMP).
    - Collision Domains: Hubs connect multiple devices, extending a single collision domain, increasing the chance of collisions in large networks.

2.  Bridges

    - Layer 2 Device: Used to segment networks, breaking up collision domains by filtering traffic based on MAC addresses.
    - Collision Domains: Bridges break collision domains but maintain one broadcast domain.

3.  Switches

    - Layer 2 Device: Similar to a multi-port bridge, connects multiple segments and manages traffic using MAC addresses.
    - Collision Domains: Each port on a switch represents a unique collision domain, enhancing network efficiency by preventing collisions.
    - Broadcast Domains: Switches operate within a single broadcast domain.
    - Switching Logic: Learns MAC addresses on each port, forwards data only to the appropriate port, minimizing unnecessary traffic.

4.  Routers

    - Layer 3 Device: Connects different networks and makes forwarding decisions based on IP addresses(IPv4, IPv6).
    - Collision and Broadcast Domains: Each router port has a separate collision and broadcast domain.
    - Functionality: Routers handle different types of networks and interface types (e.g., RJ45, fiber, serial), making routing decisions between internal LANs and external networks (e.g., the internet).

5.  Layer 3 Switches (Multilayer Switches)

    - Layer 3 Device: Combines the functionality of switches and routers.
    - Routing: Capable of performing routing functions and breaking up broadcast domains, making them ideal for internal network routing.
    - Efficiency: Suitable for smaller networks but less efficient than dedicated routers for large-scale routing.

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
3. Increase management because VLAN provides greater control over the management of networks to implement policy changes and troubleshoot issue
4. Improved cost efficiency because VLAN allows us to better utilize our existing network infrastructure by breaking it up into smaller logical segments

Effective VLANs must maintain a VLAN database that contains all of the VLAN configurations for a particular switch.

Switch Virtual Interface (SVI) allows switching to route traffic between different VLANs without requiring/buying a separate router. It provides layer three or network layer processing to the VLAN. By configuring a SVI for the VLAN, the switch can handle the routing decision for any data within that VLAN.

Cisco switch - VLAN.DAT

## VLAN Configuration

- 802.1Q Tagging: A VLAN tagging standard that adds VLAN IDs to Ethernet frames, helping manage multiple VLANs on the same physical network infrastructure(Trunking). This ensures data separation between different departments (e.g., HR and finance) by tagging their traffic for secure, isolated communication.

  - Trunking is the transmission of traffic from different VLANs across the same physical network infrastructure, while keeping the traffic from each VLAN separate and secure.

- Native VLAN: The default VLAN on a trunk port, used for untagged traffic. It's crucial for legacy devices that don’t support VLAN tags. Ensuring consistent native VLAN configurations across switches helps avoid traffic misrouting. Cybersecurity experts recommend renaming the default VLAN(VLAN10 or VLAN100) to prevent VLAN hopping attacks.

- Voice VLAN: A dedicated VLAN for voice-over-IP (VoIP) traffic, prioritizing voice data over regular traffic to maintain high-quality communications. This reduces latency, jitter, and packet loss for critical voice calls in business environments.

- Link Aggregation: A method of combining multiple network connections into one logical link, increasing bandwidth and providing redundancy. This is often used in data centers to prevent network bottlenecks and ensure high-speed connectivity.

- Speed and Duplex Configurations: These settings control data transmission speed (in Mbps or Gbps) and whether data is sent and received simultaneously (full duplex) or alternately (half duplex). Misconfigurations can reduce performance, and auto-negotiation may sometimes select lower-than-optimal speeds, requiring manual adjustments.

## Spanning Tree Protocol (STP)

## Network Access Control (NAC)

## Maximum Transmission Unit (MTU)
