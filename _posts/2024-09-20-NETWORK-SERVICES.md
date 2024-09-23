---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - Network Services
tags: [network, compTia, fundamentals, services, types of communication]
comments: true
author: Lantana Park
---

# Network Services

Network Service is a function provided by the network infrastructure to support various types of communications and processes.

## Dynamic Host Configuration Protocol (DHCP)

DHCP provides an IP address to every machine on the network and eliminates configuration errors. Because IP conflicts happens when the same IP gets assigned to multiple machine inside the same network by accident. DHCP operates using the User Datagram Protocol (UDP). To help the data get to where it needs to go, I need to configure what's known as an IP helper address on my router. The IP helper address is used to forward several different kinds of UDP broadcasts across the router and can be used in conjunction with the DHCP relay that we just talked about. So, for DHCP to work across different network segments, I need to configure the client's router with an IP helper address.

- Dynamic Assignment

- Static Assignment (I need to configure statically IP address, subnet mask, default gateway IP and DNS server IP on my device.)

DHCP Reservation lets me exclude some IP addresses from being handed out to devices unless a certain condition is met. The DHCP server automatically configures devices by assigning a static address each time, utilizing this automatic configuration.

DHCP Relay forwards DHCP packets between clients and servers. DHCP relay is used when the client device and the DHCP server are not located on the same subnet or network. instead of installing a DHCP server on every subnet or mini network inside of the network, I can configure one device to act as the DHCP relay, and that way I can save myself a lot of effort. This device will listen for discovery requests, and then forward that request to the DHCP server on the other network on behalf of the client, acting essentially as a middleman.

In the world of cyber security, having devices that are constantly changing their IPs makes it harder for us to track down when bad things happen. So in larger networks, we tend to use a longer lease time.

4 Steps of configuring a device on a network using DHCP,

1. Discover

2. Offer

3. Request

4. Acknowledge

`DORA`

With the information configured, that client can get online, get out of the network, and get onto the internet because it now knows where it is on the network with its IP address, where the router is with that gateway address, and how to convert the domain names to IP addresses using that DNS server's IP.

1. IP address

2. Subnet mask

3. Default gateway IP

4. DNS server IP

Key Features

- Centralized control over IP address assignment.

- Allows both dynamic and static address assignment.

- The lease time for IP addresses can be managed.

- Available for both IPv4 and IPv6 (via DHCPv6).

## Stateless Address Autoconfiguration (SLAAC)

Stateless Address Autoconfiguration (SLAAC) is a integral component of the IPv6 network protocol used to simplify the network configuration process and make assigning IP addresses seamless and easy to complete. SLAAC allows hosts to automatically configure own addresses without the requiring a central server. SLAAC was created to foster self-sufficiency and reduce the administrative overhead of statically assigning IP addresses.

Why SLAAC was created?

- To eliminate the need for manual IP address assignment.
- To reduce reliance on DHCP servers for dynamic IP allocation.
- To support the growing complexity of networks and streamline device integration.

How SLAAC works (5 steps)

1. Device Initiation: The device generates a temporary link-local address to identify itself.
2. Router Solicitation: The device sends a message to the network asking for routers to identify themselves.
3. Router Advertisement: The router responds with information about the network, including the network prefix.
4. Address Configuration: The device combines the network prefix with a unique identifier derived from its hardware address to form a complete IPv6 address.
5. Final Check: The device checks for address conflicts via neighbor solicitation to ensure no other device is using the same IP.

In a smart home, devices like fridges, cameras, and lights automatically connect to the network, finding their unique place without requiring manual IP assignment. Similarly, SLAAC enables devices in IPv6 networks to self-discover and configure their addresses, ensuring efficient communication.

## Domain Name System (DNS)

The Domain Name System (DNS) is a protocol that translates human-readable domain names (e.g., diontraining.com) into numeric IP addresses (e.g., 66.123.45.237) that computers use for communication. It simplifies web navigation, making it easier for users to remember domain names rather than IP addresses.

How DNS Works:

When a user types a domain name into their browser, their device contacts a DNS server to request the IP address associated with that domain.
The DNS server responds with the correct IP address, allowing the device to connect to the web server.

Fully-Qualified Domain Name (FQDN) is a complete domain name, such as `www.diontraining(Domain name).com(Top level domain)`, that specifies the exact location of a resource in the DNS hierarchy.

DNS Hierarchy (5 Levels):

1. Root Level: The highest level of the DNS hierarchy, represented by a dot (.). It answers requests in the root zone. It contains a list of top-level domains (TLDs)

2. Top-Level Domains (TLDs): These include generic TLDs like `.com`, `.edu`, `.net`, or country code TLDs like `.de` or `.us`.

3. Second-Level Domains: Domains directly under the TLD, such as diontraining in `diontraining.com`. This is the registered domain name.

4. Subdomains: An optional part of the domain name that can be added before the second-level domain, like www or mail (e.g., `www.diontraining.com` or `support.diontraining.com`).

5. Host Level: Refers to the individual machine or service in the network, often represented by an A or AAAA record in DNS. It points to a specific IP address where the service (like a web server or mail server) is hosted.

Before DNS, systems used a flat file called the host file to map domain names to IP addresses.
The host file can still be used to override DNS locally. And every time I enter a website's name, my system has to first consult its host file to see if it already knows the IP address for that given domain name.

Attackers can manipulate host files to redirect traffic to malicious sites, highlighting the need for caution when modifying host files.

### DNS Record Types

DNS records are entries in the Domain Name System (DNS) that map domain names to various types of information, primarily IP addresses. These records tell DNS servers how to respond to queries for a domain. Different types of DNS records serve different purposes, and they are essential for routing traffic on the internet.

Zone Transfer is to send DNS records data from the primary nameserver to a secondary nameserver. It used the TCP protocol to transfer data.

DNS Record | Description | Function | Example
A | Address | Links a hostname to an IPv4 address | `www.example.com` -> `192.12.1.1.`
AAAA | Address | Links a hostname to an IPv6 address | `www.diontraining.com` -> `2400:cb00:2024::a29f:1234`
CNAME | Canonical Name | Pints a domain to another domain or subdomain | `support.diontraining.com`
MX | Mail Exchange | Directs email to a mail server, using priorities to set routing preferences. | `mail.diontraining.com`
SOA | Start of Authority | Stories important information about a domain or zone updates and DNS zone transfer
PTR | Pointer | Maps an IP address to a domain name, used for reverse DNS lookups for security purposes
TXT | Text | Stores human-readable or machine-readable text, often used for domain verification or email security.
NS | Nameserver | Specifies the authoritative DNS server for a domain.

### Attack using DNS

DNS snooping : An attacker monitor DNS queries to infer what websites a user is visiting.

### Securing DNS

- DNS Security Extensions (DNSSEC) provides a digital tamper-proof seal for the DNS data to ensure that the information reaching the device is exactly what the server intended to send. However, DNSSEC does not encrypt any of the DNS data.

- DNS over HTTPS (DoH) is used to send the DNS queries through the HTTPS protocol, which is the same protocol that secures the data.

- DNS over TLS (DoT) encapsulates DNS traffic inside of a transport layer security tunnel. DNS over TLS also provides privacy for the DNS data since it is encrypted.

Website owners need to embrace DNSSEC to protect domain names
Internet Service Providers and organizations should consider supporting DoH and DoT.

## Network Time Protocol (NTP)

Network Time Protocol is used to synchronize clocks between systems communicating over a packet-switched, variable-latency data network. It is sent over UDP using port 123.

Synchronization is crucial for security protocols, as mismatches in time can cause login errors or security issues (e.g., if system clocks differ by more than five minutes).

How does NTP work?

Three different components

1. Stratum

   - Stratum 0: Most precise time sources like atomic clocks or GPS.
   - Stratum 1: Primary servers connected to Stratum 0 devices.
   - Stratum 2+: Servers synchronized to higher-level servers (Stratum 1, Stratum 2, etc.), with each level adding slight delays. The limit is Stratum 15.
     NTP can handle a maximum of 15 stratum levels

2. Clients

3. Servers

In enterprise networks, NTP servers synchronize time across systems, with clients (e.g., workstations) syncing their clocks using this service.

#### Newer protocol to coordinate time on the systems

- Precision Time Protocol (PTP) is a protocol used to synchronize clocks throughout a computer network. it is ideal for networks that require precise timekeeping.

- Network Time Security (NTS) is an extension of NTP that was developed to provide cryptographic security for the time synchronization provided by the NTP servers. It ensures time synchronization processes are secure from malicious interference.

## Quality of Service (QoS)

QoS allows networks to prioritize certain types of traffic to ensure proper functionality, especially for time-sensitive applications like VoIP or video streaming.

Voice and video traffic require higher priority due to their sensitivity to latency and jitter, whereas data traffic (e.g., web browsing) can tolerate slight delays.

QoS Categories

- Delay: The time taken for a packet to travel from source to destination, important for live communications like VoIP or video calls.
- Jitter: Uneven arrival of packets, affecting real-time communications and causing distorted audio or video.
- Drops: Packet loss due to congestion, which can severely impact UDP-based applications like VoIP, leading to noticeable communication gaps.

#### Effective Bandwidth

The overall speed of communication is limited by the slowest link in the network path. QoS helps manage this by prioritizing critical traffic within the available bandwidth.

#### Mechanisms I can use to categorize the traffic

1. Best effort - No QoS, Traffic is first in, first out

2. Integrated services (IntServ) - Hard QoS, Traffic has strict bandwidth reservations

3. Differentiated services (DiffServ) - Soft QoS, has differentiation of data types where routers and switches can make decisions based on markings and can fluctuate traffic

Best Effort | Not strict
DiffServ | Less strict (Soft QoS)
IntServ | More strict (Hard QoS)

### QoS mechanisms

1. Classification: Traffic is categorized based on type, such as email (POP3, IMAP, SMTP), VoIP, video, etc. It’s identified through packet headers, ports, and protocols without altering bits in the packet. Switches and routers use this info to implement QoS.

2. Marking: Here, specific bits in the packet are altered to signal how the traffic should be treated. This marking, such as using IP precedence or DSCP (Differentiated Services Code Point), helps network devices prioritize packets.

3. Congestion Management: When devices receive more traffic than they can send, they buffer it. Queuing algorithms like weighted fair queuing, low-latency queuing, and weighted round-robin are used to decide which packets are sent first. Weighted round-robin, for example, allows traffic prioritization by category (e.g., VoIP gets more priority).

4. Congestion Avoidance: Mechanisms like RED (Random Early Detection) help prevent queues from overflowing by selectively dropping low-priority traffic when congestion builds up, especially for TCP traffic, which can retransmit.

5. Policing and Shaping: Policing drops packets that exceed a bandwidth limit (like enforcing a speed limit), leading to retransmissions. Shaping, on the other hand, buffers excess traffic and sends it when bandwidth is available, optimizing network performance.

6. Link Efficiency: Techniques such as compression and LFI (Link Fragmentation and Interleaving) improve bandwidth utilization. Compression reduces packet size, especially for VoIP, while LFI fragments large packets and interleaves smaller ones, reducing latency on slower links
