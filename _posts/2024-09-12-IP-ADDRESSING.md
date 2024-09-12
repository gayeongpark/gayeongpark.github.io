---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - IP address
tags: [network, compTia, fundamentals, ip, subnet]
comments: true
author: Lantana Park
---

# IP Addressing

Internet Protocol (IP) Address is an assigned numerical label that is used to identify Internet communicating devices on a computer network. IP addresses are used at layer 3 of the OSI model. And they are going to be used by routers to send data from one network into another.

## IPv4 Addressing

An IPv4 address is represented by four octets, each containing 8 bits, resulting in a total of 32 bits for the entire addressable space.

`192.168.1.4` -> `11000000.10101000.00000001.00000100`

Each IPv4 address is actually going to be created using two portions

Subnet mask (common subnet masks associated with private IP address ranges)
`255.255.255.0` -> `11111111.11111111.1111111.00000000`

1. Network portion

   `11111111.11111111.1111111`
   `192.168.1`

2. Host portion(Server, Desktop, Laptop, Tablet, Printer)

   `00000000`
   `4`

### IPv4 class

![classRange](../assets/img/networkFundamental/Screenshot%202024-09-12%20at%2015.16.27.png)

Multicast Address is a logical identifier for a group of hosts in a computer network. It is like a group chat.

Subnetting is the process of taking a larger network portion and subdividing it into smaller portions.

- Classful Subnet Mask

It is the default mask for a given class of IP addresses

- Classless Subnet Mask

It is used to borrow some of the host bits from an IPv4 address

CIDR (Classless Inter-Domain Routing) combines the IP address and subnet mask into a single notation. For example, the IP address `192.168.1.4` with a subnet mask `255.255.255.0` is written as `192.168.1.4/24`.

The number after the slash (e.g., /24) represents how many bits are set to "1" in the subnet mask.

For example, 255.255.255.0 has 24 bits set to "1", so it's written as /24.

Classful vs. Classless Subnet Masks:

Classful subnet masks match the default for a class:
Class A: /8 (255.0.0.0)
Class B: /16 (255.255.0.0)
Class C: /24 (255.255.255.0)

Classless subnet masks deviate from the default for a class. For example:
192.168.1.4/26 means 26 bits are used for the network portion, which corresponds to `255.255.255.192` -> `11111111.11111111.11111111.11000000`.

Class Breakdown:

- Class A: Default subnet mask is 255.0.0.0 or /8.
- Class B: Default subnet mask is 255.255.0.0 or /16.
- Class C: Default subnet mask is 255.255.255.0 or /24.

In essence, CIDR notation simplifies IP address and subnet representation by specifying the number of bits dedicated to the network portion of the address.

## IPv4 Address Types

1. Public IPv4 Addresses

   - Also known as routable IPs, these are unique global identifiers for devices to communicate over the internet.
   - Managed by ICANN and its regional bodies (e.g., ARIN, LACNIC).
   - Must be leased or purchased from an ISP.

2. Private IPv4 Addresses

   - Non-internet routable, used within local networks for internal communication.

   - IP ranges:
     Class A | 10.0.0.0 – 10.255.255.255 | 16.7 million (256 x 256 x 256)
     Class B | 172.16.0.0 – 172.31.255.255 | 1.05 million (16 x 256 x 256)
     Class C | 192.168.0.0 – 192.168.255.255 | 65,536 (256 x 256)
   - Use NAT (Network Address Translation) to translate private IPs to public IPs when accessing the internet.

3. Loopback/Localhost Addresses

   - Range: 127.0.0.0/8, typically 127.0.0.1.
   - Used for internal testing and diagnostics, without external communication.

4. APIPA (Automatic Private IP Addressing)

   - Range: 169.254.0.0 – 169.254.255.255.
   - Assigned when DHCP fails, allowing limited local network communication but not internet access.
   - Indicates potential issues with DHCP(for automatically assigning IP addresses) when seen on a device.
   - It is considered private IPs.

## IPv4 Data Flows

- Unicast : Data travels from a single source to **a single destination**. It’s a one-to-one communication, like a phone call between two people.

- Multicast : Data is sent from a single source to **multiple specific destinations**. It’s efficient because the data is sent once and delivered to multiple devices in a multicast group.

- Broadcast : Data is sent from a single source to **all devices on the destination network**. Every device connected to the network receives the broadcast. (radio broadcast)

## Assigning IPv4 Addresses

There are two main ways to assign IP addresses in a network: static (manual) and dynamic (automatic).

1. Static Assignment

   - A technician manually assigns the IP address, subnet mask, default gateway, and DNS server for each device.
   - This method is prone to errors and is impractical for large networks due to the time and complexity of managing multiple devices.

2. Dynamic Assignment

   - The IP address and related information are assigned automatically. This is more efficient for both small and large networks. The four critical pieces of information that are dynamically assigned are the IP address, subnet mask, default gateway, and DNS server.

Methods of Dynamic IP Assignment

1. BOOTP (Bootstrap Protocol):

   - An older protocol from 1985 used for diskless workstations. It assigns IP addresses based on a static MAC address database.

2. DHCP (Dynamic Host Configuration Protocol)

   - Introduced in 1993, it dynamically assigns IP addresses from a pool or scope of addresses. It leases an IP to a client for a set time and automatically renews or reassigns it when necessary.
   - **DHCP provides the IP address, subnet mask, default gateway, DNS server, and optional WINS server information**.
   - DHCP is the modern implementation of BOOTP.

     - WINS is like DNS, but it only works within a Windows domain environment.

3. APIPA (Automatic Private IP Addressing)

   - Used when DHCP is unavailable. APIPA assigns a self-configured IP in the 169.254.x.x range, **allowing local network communication but not internet access**.
   - APIPA allows for a quick configuration of a LAN without the need for a DHCP server.

4. ZeroConf (Zero Configuration)

   - Builds on APIPA, enabling link-local IP address assignment, name resolution without DNS (via mDNS), and service discovery (e.g., finding printers or shared drives). It's used in systems like Apple's Bonjour, Windows' LLMNR(Link-Local Multicast Name Resolution) and Linux' SystemD.

## Computer Mathematics

## Subnetting

## IPv6 Addressing

## IPv6 Data Flow

## IPv4 and IPv6 Compatibility Requirements
