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

## Subnetting

Subnetting is where we can take a large network and we split in up into smaller networks.

Subnet masks modify subnets and create better scoped networks.

Classless Inter-Domain Routing (CIDR) is the shorthand notation used to summarize continuous networks called using route aggregation.

Variable-Length Subnet Mask (VLSM) allows subnets of various sizes to be used and requires a protocol that supports it.

CIDR | Subnets | IPs
/24 | 1 | 256
/25 | 2 | 128
/26 | 4 | 64
/27 | 8 | 32
/28 | 16 | 16
/29 | 32 | 8
/30 | 64 | 4

Easy way to calculate the assignable IP addresses

If the IP address is `172.16.1.0/27`

1. IPs

   = 2<sup>(32-27)</sup> - 2

   = 2<sup>5</sup> - 2

   = 32 (Total IPs) - 2 (Network IP and Broadcast IP - Unassignable)

   = 30(Assignable IPs)

2. Subnets

   = 2<sup>(27-24)</sup>

   = 2<sup>3</sup>

   = 8 (Subnets)

For example, if `171.129.67.168/25` was given

1. Network IP `171.129.67.128`

   - Identify the Subnet Mask

     `/25` means that the first 25 bits are for the network and the remaining 7 bits are for hosts. For finding network ip, I need to set the host part into `0` and network part into `1`

     `11111111.11111111.11111111.10000000`

   - Convert the IP address into Binary

   `171`

   171 / 2 = 85 remainder 1<br/>
   85 / 2 = 42 remainder 1<br/>
   42 / 2 = 21 remainder 0<br/>
   21 / 2 = 10 remainder 1<br/>
   10 / 2 = 5 remainder 0<br/>
   5 / 2 = 2 remainder 1<br/>
   2 / 2 = 1 remainder 0<br/>
   1 / 2 = 1 remainder 1<br/>

   = `1 0 1 0 1 0 1 1`

   `129`

   129 / 2 = 64 remainder 1<br/>
   64 / 2 = 32 remainder 0<br/>
   32 / 2 = 16 remainder 0<br/>
   16 / 2 = 8 remainder 0<br/>
   8 / 2 = 4 remainder 0<br/>
   4 / 2 = 2 remainder 0<br/>
   2 / 2 = 1 remainder 0<br/>
   1 / 2 = 0 remainder 1<br/>

   = `1 0 0 0 0 0 0 1`

   `67`

   67 / 2 = 33 remainder 1<br/>
   33 / 2 = 16 remainder 1<br/>
   16 / 2 = 8 remainder 0<br/>
   8 / 2 = 4 remainder 0<br/>
   4 / 2 = 2 remainder 0<br/>
   2 / 2 = 1 remainder 0<br/>
   1 / 2 = 0 remainder 1<br/>

   = `1 0 0 0 0 1 1` In order to make 8-bit representation, I need to add leading zeros. `0 1 0 0 0 0 1 1`

   `160`

   160 / 2 = 80 remainder 0<br/>
   80 / 2 = 40 remainder 0<br/>
   40 / 2 = 20 remainder 0<br/>
   20 / 2 = 10 remainder 0<br/>
   10 / 2 = 5 remainder 0<br/>
   5 / 2 = 2 remainder 1<br/>
   2 / 2 = 1 remainder 0<br/>
   1 / 2 = 0 remainder 1<br/>

   = `10100000`

   So, `171.129.67.160` in binary is `10101011.10000001.01000011.10100000`

   - Perform a bitwise AND operation

   If both bits are `1`, the result is `1`.
   If either bit is `0`, the result is `0`.

   | IP Address (`171.129.67.160`) | 10101011.10000001.01000011.10100000 | | Subnet Mask (`255.255.255.128`) | 11111111.11111111.11111111.10000000 | | Result (Network Address) | 10101011.10000001.01000011.10000000 |

   In decimal form, `10101011.10000001.01000011.10000000` is :

   `1 0 1 0 1 0 1 1`

   1 + 2 + 8 + 32 + 128 = 171

   `1 0 0 0 0 0 0 1`

   1 + 128 = 129

   `0 1 0 0 0 0 1 1`

   1 + 2 + 64 = 67

   `1 0 0 0 0 0 0 0`

   = 128

   `171.129.67.128`

2. Broadcast IP `171.129.67.255`

   | Network address (`171.129.67.128`) | 10101011.10000001.01000011.10000000 | | Set the host bits (last 7 bits) to 1 | 10101011.10000001.01000011.11111111 |

   `10101011.10000001.01000011.11111111`

   In decimal form, the Broadcast address is `171.129.67.255`

3. Assignable IP range `171.129.67.129` - `171.129.67.254`

## IPv6 Addressing

IPv4 has its limited address space.

IPv6 has larger address space and no broadcast. It is considered to be more secure because there is no packet or datagram fragmentation. It has simplified header. IPv6 address uses **hexadecimal digits** and allows the use of shorthand notation. **IPv6 has 128 bits of addressable space inside of it as opposed to the 32 bits that we has in IPv4.**

Shorthand notation:

`2018 : 0000 : 0000 : 0000 : 0000 : 0000 : 4815 : 54ae` -> `2018 : 0 : 0 : 0 : 0 : 0 : 4815 : 54ae` -> `2018 :: 4815 : 54ae`

Different types of IPv6

A single interface can be assigned to multiple different IPv6 addresses.

`2584:0db8:8583:1234:5678:882e:0370:7334`

- **Unicast addresses** are used to identify a single interface. (`2584`)

  - Globally-routed unicast addresses (`2584:0db8:8583:1234:5678:882e:0370:7334`) are similar to IPv4's unicast class A, B, and C addresses and begins with 2000-3999. SLAAC (Stateless Address Autoconfiguration) facilitates automatic address configuration for devices using RA messages, without needing manual configuration or a DHCP server. This autoconfiguration process discovers the current network that an interface is located on, and select its own host ID based on its MAC address using the EUI-64 process.

    - Extended Unique Identifier (EUI) allows a host to assign itself a unique 64-bit IPv6 interface identifier called EUI-64. EUI-64 process splits the MAC address into two 24-bit parts (Organizationally Unique Identifier and device-specific identifier) and inserts `FF FE` between them to form the 64-bit address.

      `00:21:2F:B5:6E:10` (MAC Address)
      `00:21:2F:FF:FE:B5:6E:10` (64-bit EUI)

    - DHCPv6 Protocol allows DHCP to automatically assign addresses from a DHCPv6 server. DHCPv6 can also be used to assign IPv6 addresses, but SLAAC allows a device to autonomously generate its IP address using NDP and EUI-64, making DHCPv6 optional.

    - Neighbor Discovery Protocol (NDP) is used to determine the Layer 2 addresses that are on a given network. SLAAC uses NDP to discover Layer 2 addresses (MAC addresses) and network neighbors. NDP functions include:

      - Router Solicitation: Clients ask for routers on the network.

      - Router Advertisement: Routers announce their presence and provide network prefix information.

      - Neighbor Solicitation and Advertisement: Hosts discover other nodes on the network and exchange information.

      - Redirection: Routers suggest more efficient routes to a destination.

  - Link-local/Local Use addresses is very much like a private IP inside of IPv4. It can only be used on the local area network and begins with `FE80` as its first segment. Whenever an IPv6 system starts up itself, it is automatically going to create a link-local address for each IP version six interface on that system.

- **Multicast addresses** are used to identify a group of interfaces and begins with `FF`.

- **Anycast addresses** are used to identify a set of interfaces so that a packet can be sent to any member of a set. Data travels from a single source device to the device nearest to multiple (but specific) destination devices. It is really efficient.

## IPv4 and IPv6 Compatibility Requirements

As the transition from IPv4 to IPv6 occurs, both protocols need to coexist on the same network due to the widespread use of IPv4. Here are the main mechanisms used to ensure compatibility:

1. **Dual Stack** allows devices (Routers, Switches, and hosts) to run both IPv4 and IPv6 simultaneously. Devices communicate using IPv6 by default. If IPv6 is unavailable, they fall back to IPv4. DNS queries return both A (IPv4) and AAAA (IPv6) records, and devices choose the appropriate protocol. This method provides a seamless migration path without disrupting services or requiring immediate IPv4 removal.

2. **Tunneling** encapsulates IPv6 packets within IPv4 packets to allow them to traverse an IPv4 network. IPv6 packets are encapsulated in IPv4, sent across the IPv4 network, then decapsulated at the endpoint and delivered to the IPv6 destination. Techniques like 6to4, Teredo, and ISATAP create these tunnels. This method enables IPv6 communication over IPv4 infrastructure.

3. **NAT64** allows IPv6-only devices to communicate with IPv4 services. A NAT64 gateway translates IPv6 addresses into IPv4 and vice versa. The gateway maintains a translation table for seamless interaction between devices across both protocols. This method facilitates communication between IPv6-only devices and legacy IPv4 systems, extending the life of IPv4.

While IPv6 brings new benefits, IPv4 will remain in use for the foreseeable future. These compatibility mechanisms allow the internet and network infrastructure to support both protocols during the lengthy transition period