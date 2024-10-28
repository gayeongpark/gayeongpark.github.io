---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - troubleshooting (2)
tags: [network, compTia, fundamentals, troubleshooting, second]
comments: true
author: Lantana Park
---

# Troubleshooting Network Services

## Duplicate Addresses

### Duplicate MAC addresses

Having two or more devices responding to data requests from the same MAC address can cause significant network issues.

To avoid issues, enable port security on the switches.

- Logical Domain Manager : Listen to multicast messages on a network and keeps track of the MAC addresses

### Duplicate IP addresses

It occurs when another computer on the same network has an identical IP to another workstation or server on the same network.

Probable causes

- Static IP address issue

- DHCP server issue

- Rogue DHCP server

To solve this issue, start by checking whether the client is dynamically or statically assigned an IP address.

## DHCP Issues

DHCP (Dynamic Host Configuration Protocol) is a network management protocol that automatically assigns IP addresses and other parameters (subnet mask, default gateway, DNS server) to devices in a network using a client-server architecture.

- Rogue DHCP Servers : A rogue DHCP server is an unauthorized DHCP server in the network, either maliciously installed or accidentally by employees (e.g., connecting a wireless router with a built-in DHCP server). It can cause significant issues, such as:

  - Man-in-the-middle attacks: The rogue server can configure clients to redirect traffic to malicious websites.

  - Duplicate IP addresses: If the rogue server uses the same IP scope as the authorized DHCP server, it can cause network issues by assigning the same IP to multiple devices.

### Solutions

- DHCP snooping: A security feature that blocks unauthorized DHCP traffic.
- Port security: Preventing rogue devices from connecting to network ports.
- Intrusion detection systems (IDS): Identifying rogue DHCP servers and allowing administrators to remove them.

- DHCP Scope Exhaustion: This occurs when a DHCP server runs out of available IP addresses in its scope, meaning it can no longer assign IPs to new devices.

  - For example, a network with 254 IPs may face exhaustion if there are more devices than available addresses.

  - Long lease times (e.g., 7 or 30 days) can exacerbate the problem in environments with many transient users, as IP addresses are reserved for longer than necessary.

### Solutions

- Reducing lease time: Setting shorter lease times (e.g., 24 hours) to free up IPs more frequently.
- Increasing scope size: Expanding the IP range to accommodate more devices (e.g., switching from a /24 to a /22 network).
- Limiting device access: Using port security or network access control (NAC) to prevent unauthorized devices from consuming IP addresses.

## Routing Issues

1. Multicast Flooding

   - Multicast communication sends messages to multiple hosts at once.
   - Flooding occurs when the switch's CAM table doesn't associate any host with the multicast MAC address, causing multicast traffic to flood the entire LAN or VLAN, wasting resources.
   - Solution: Block unknown multicast packets on switches.

2. Asymmetrical Routing

   - This occurs when packets leave via one path and return via another, often in high availability clusters or load-balanced environments.
   - Problematic for security devices like stateful firewalls, as they need to see the entire packet flow for proper inspection.
   - Solution: Adjust firewall placement and internal routing so that traffic flows consistently through the same firewall in both directions.

3. Missing Routes

   - Missing routes in a router's routing table prevent it from reaching certain destinations.
   - Common with manual/static routes if misconfigured, or in dynamic routing protocols like OSPF or BGP if routers fail to establish neighbor states.
   - Solution: Check the routing table using show ip route or route print, and verify dynamic routing protocols are enabled and neighbors are communicating. Add routes manually if necessary.

## Switching and Routing Loops

- Switching Loop occurs whenever there is more than one path between the source and destination devices. Switching loops are usually an issue with how STP is configured.

- Routing Loop is formed when an error occurs in the operation of the routing algorithm and creates a circular route amongst a group of network devices. Routing loops are caused by logical Layer 3 circular connections that may exist in a routing table.

  ### Solutions

  - Split Horizon : Routing configuration that stops a route from being advertised back in the direction from which it came
  - Route Poisoning : Increasing a router's metric to an infinitely high number after detecting one of its connected routes has failed
  - Hold-Down Timer : Prevents bad routes from being restored and passed to other routers by accident

## Firewall Issues

### Common scenarios for firewall-related network issues

1. Access to protected resources from unprotected networks isn't working.

2. Access to unprotected resources from protected networks isn't working.

3. Access to the firewall and its configuration isn't functioning.

### Ways to troubleshoot

Go through OSI model from first to seventh. Especially, always check ACLs to ensure they are in the right sequence.

1. Ensure there are no typos in the ACL rules

2. Verify the protocol and port numbers referenced by the rule are correct

3. Verify the source and destination addresses are referenced by the rule

4. Verify the order of the rules is applied correctly

And in the Windows firewalls, it is important to look not just at the IP addresses and ports that are being blocked.

## VLAN Issues

Devices in different VLANs (e.g., IT and HR) cannot communicate directly, even if they're physically connected to the same switches, until routing is configured between the VLANs.

Devices in the same VLAN must be on the same subnet. For example, all IT clients in VLAN 100 could use the 192.168.1.0/24 subnet, while HR clients in VLAN 200 might use 192.168.2.0/24.

Another common mistake is not using VLANs, leaving all devices in the default VLAN (VLAN 1), which creates a large broadcast domain. This can slow down the network due to excessive broadcasts. Separating traffic into VLANs improves performance, especially for critical devices like servers.

Finally, if the new VLAN is not allowed on the trunk link, traffic from that VLAN cannot traverse the network to reach the router for internet access. Ensuring the trunk link is configured to allow the new VLAN resolves the issue. Incorrect subnet masks would affect local communication, not specifically internet access. If the DHCP server ran out of IP addresses, users would not receive any IP configuration. While the firewall could block internet access, it's less likely if the issue is isolated to a newly created VLAN.

## DNS and NTP Issues

### DNS Issues

DNS matches domain names (like `example.com`) to their corresponding IP addresses.

1. Client-Side DNS Issue

   - TCP/IP Settings: Use ipconfig, ifconfig, or ip commands to verify the DNS server IP.
   - Connection Troubleshooting: If no connectivity between client and DNS server, troubleshoot layers of the OSI model (Layer 1, Layer 2, Layer 3).
   - Flush DNS Cache: Command `ipconfig /flushdns` (Windows) or `sudo systemd-resolve --flush-caches` (Linux) to clear the DNS cache.
   - Change DNS Server: Use a reliable DNS like Google's DNS (8.8.8.8, 8.8.4.4) if the issue persists.

2. DNS Server-Side Issues

   - A Records: Ensure the domain name is correct and points to the right IP address.
   - CNAME Records: Verify the source and destination domain names.
   - TTL (Time to Live): Avoid setting TTL too high (e.g., 86,400 seconds). A lower TTL (~300 seconds) allows quicker DNS record updates.
   - Latency: Use DNS servers geographically closer to users to reduce DNS latency.

3. Tools for DNS Troubleshooting

   - nslookup: Use to verify A and CNAME records.
   - ping: Test connectivity to the DNS server.

### NTP Troubleshooting

NTP synchronizes system clocks across devices in a hierarchical time source system.

1. Common NTP Issues

   NTP Packets Not Received:

   - Check physical connection (Layer 1).
   - Verify MAC address communication (Layer 2) if on LAN.
   - Ensure proper IP communication (Layer 3) if outside the LAN.
   - DNS Dependency: Verify NTP server domain name resolution if using a domain name instead of an IP.

   NTP Packets Not Processed:

   - Ensure the NTP service is running on the client and server.
   - Check if NTP packets are being read and acted on properly.

   Errors or Packet Loss:

   - Causes: Network saturation, high dispersion/delay values, link saturation, buffering.
   - Consequence: Loss of synchronization between client and server.
   - Troubleshooting: Look for network congestion, packet loss, or excessive delays that impact synchronization.

# Troubleshooting Performance Issues

## Troubleshooting Performance Issues

## Collisions and Broadcast Storms

Collision occurs when two hosts on the network transmit at the same time which causes the signals to combine on the network medium. It can occur in both wired and wireless networks.

To prevent collisions, design the networks with smaller collision domains. To break apart collision domains, we need to use any Layer 2 devices, such as switch.

To check if there are collision, input `show interface ethernet 0`, `show controller ethernet 0`.

To overcome this issue, we need to turn off auto-negotiation for the speed, hardcode to lower speed setting, change to half-duplex

Broadcast storm occurs when a network system is overwhelmed by continuous multicast or broadcast traffic. A broadcast storm significantly decreases network performance. It can happen in Layer 2 and 3. It will show like `FF:FF:FF:FF:FF:FF` in Layer 2, `255.255.255.255` in Layer 3.

Broadcast Domain is a logical division of a computer network where all nodes can reach each other by broadcast at the data link layer. A switch and a Layer 2 device will not break up broadcast domains because they bridge these things together. Instead, I have to reach a router or a Layer 3 switch to break up the broadcast domain into smaller broadcast domains.

### Main causes of broadcast storm

1. Too large singular broadcast domain. Instead I need to use a router to break up subnets into separate broadcast domains.

2. Large volume of DCHP requests

3. Loops are created in the switching environment

### Mitigation of broadcast storm

1. Enable Bridge Protocol Data Units (BPDU) - loop prevention on managed switches

2. Enforce a maximum number of MAC addresses per port

3. Break up large broadcast domains into smaller domains using routers and Layer 3 switches

### Identification of broadcast storm

1. Look at the packet counters. A rapid increase beyond the normal baseline may indicate a broadcast storm

2. Look at the network monitoring tools and determine the packet loss on the network. During a broadcast storm, network devices struggle to process the flood of packets using Wireshark and TCPdump

## VoIP Issues

Voice Over Internet Protocol is a set of protocols that are used to send streaming voice and video in real time. Being able to have a very low latency and a very high quality of service is imperative to having a good voice connection or video connection when using real-time protocols such as VoIP.

- Latency : Time it takes for a signal to reach the intended client. It is about the travel time of each packet. For providing stable service, I need to keep latency under 50 to 100 milliseconds. Latency is the delay between the sending and receiving of data packets, it doesn't directly cause intermittent disruptions.

- Jitter : Measurement of the variation in delay over time. When latency increases by up to 30-50 milliseconds, it starts to have jitter. Jitter is a variation in the delay of received packets, with irregular arrival times causing intermittent disruptions such as freezes and delays.

### Solutions of latency and jitter

1. Increase network performance

2. Implement Quality of Service

## Packet Loss

Packet Loss occurs when data packets traveling across a network fail to reach their intended destination.

Due to packet loss, unexplained network slowdowns, jitter during VoIP calls, abrupt disconnections in streaming media playback will occur.

### Main causes of packet loss

1. Network congestion : Occurs when too much data is sent through a network that exceeds the network's handling capacity.

2. Faulty router configurations : occurs when routers are set up incorrectly and lead to data being misdirected or not prioritized properly by the systems.

3. Bad cables : Physically damaged or deteriorating wires that will disrupt the network's data transmissions.

4. Hardware failures : Occurs when network devices like switches, routers, or modems malfunction.

### Identification of packet loss

- `Ping` shows that packets are not getting through

- `Traceroute` for packet loss

- Cable Analyzer measures dB loss in copper cables

It is important to implement proactive measures to help prevent packet loss

## Network Performance Issues

- High CPU Usage : Network devices like routers, switches, and firewalls have CPUs. When over-utilized, the network slows down, causing increased latency, jitter, and packet loss. To resolve this, upgrade devices or reduce the processing load (e.g., simplifying access lists).

- High Bandwidth Utilization : High bandwidth usage causes delays and dropped packets, especially with TCP retransmissions, which further increases traffic. Solutions include increasing bandwidth or conducting network flow analysis to limit non-essential traffic, such as social media use.

- Poor Physical Connectivity : Damaged cables lead to errors and retransmissions, slowing down the network. Use a cable tester or fiber light meter to identify faulty connections, and test from the demarcation point to pinpoint the issue.

- Network malfunction : Misconfigurations, hardware failures, or outdated software can degrade performance. Troubleshoot using the seven-step method to identify and fix device issues.

- DNS Problems : High DNS latency affects user experience by delaying domain name resolution. Address DNS issues to improve overall network performance.

## Other Performance Issues

- Low Optical Link Budgets : Optical link budgets involve calculating anticipated losses in a fiber optic connection due to factors like distance, cable imperfections, and splicing. If losses exceed certain levels, transmission issues arise. Tools like Optical Time-Domain Reflectometers (OTDR) help measure these losses.

- Certificate Issues : Digital certificates verify identity during network transactions. Problems like expired certificates or certificates not signed by trusted authorities can disrupt secure communications over HTTPS. In internal networks, certificates are often used for authentication in protocols like 802.1X.

- License Feature Issues : Network devices may have limited functionality based on the license purchased. Mismatches between expected and purchased features can lead to errors, requiring troubleshooting and potentially purchasing upgraded licenses.

- BYOD Challenges : Supporting a Bring-Your-Own-Device (BYOD) policy creates complexities as network administrators must manage diverse devices with different configurations. This increases operational expenses and troubleshooting challenges, particularly in identifying whether issues stem from the network or the device.

- Hardware failures : Can occurs all over the network. To troubleshoot, I need to pinpoint which component on the device has failed. To solve this issue, replace the failed component, replace the entire device, and then return to the manufacture for require or properly dispose.
