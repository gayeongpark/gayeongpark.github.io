---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - network segmentation
tags: [network, compTia, fundamentals, segmentation]
comments: true
author: Lantana Park
---

# Network Segmentation

## Firewalls

Firewalls uses a set of rules defining the types of traffic permitted or denied through the device. It operates based on IP address or port

- Packet-Filtering Firewall : Permits or denies traffic based on packet header and rule set

- Stateful Firewall : Inspects traffic as part of a session and recognizes where the traffic originated. It is possible ACLs and permit and deny statements of a packet-filtering firewall with stateful firewall capabilities for security

- NextGen Firewall (NGFW) : Conducts deep packet inspection and packet filtering

Unified Threat Management (UTM) Device : Combines firewall, router, intrusion detection/prevention system, anti-malware, and other features (VPN, Content filtering, Spam filtering) into a single device.

## Access Control List (ACL)

Access Control List (ACL) is a set of rules applied to router interfaces that permit or deny certain traffic.

### Key Criteria for ACLs

- Source IP Address
- Destination IP Address
- Source Port
- Destination Port

ACLs typically do not operate based on MAC addresses. MAC filtering is done at Layer 2 (Data Link Layer), while ACLs typically work at Layer 3 (Network Layer) or Layer 4 (Transport Layer).

### Block-able things using ACL

1. Block requests from internal or private loopback addresses (e.g., 127.0.0.0/8) and multicast IP ranges (e.g., 224.0.0.0/4).

2. Block incoming requests for protocols that should only be used locally (e.g., certain administrative or control protocols).

3. Block or allow specific types of traffic, such as:

   - IPv6 traffic: You can block all IPv6 traffic or restrict it to authorized hosts and ports.

### Types of Deny Rules in ACLs

- Explicit Deny : Blocks matching traffic

`deny ip 8.8.8.8 0.0.0.0 any any`

That means that it is going to block all ports and all protocols going to the IP address of 8.8.8.8. The 0.0.0.0 wildcard mask is used to match only the source IP of 8.8.8.8.

- Implicit Deny : Blocks traffic to anything not explicitly specified.

### Role-Based Access for ACL Management

ACLs are often managed by administrators with specific role-based access controls (RBAC). This defines the privileges and responsibilities of users, ensuring only authorized personnel can modify firewall rules and ACLs.

## Segmentation Zones

### Types of zones

1. Trusted Zone (Inside Zone)

   - This is your internal network, often a Local Area Network (LAN) or intranet.
   - It is the most trusted zone, where internal users and resources reside.
   - Traffic is generally allowed between internal devices.

2. Untrusted Zone (Outside Zone)

   - This includes the internet or other external networks that are not under your control.
   - Considered unsafe, traffic from this zone is generally blocked unless specifically requested by users inside the trusted zone.
   - Requests from the internal zone (like browsing a website) temporarily open a port in the firewall, allowing return traffic.

3. Screened Subnet (Semi-Trusted Zone or DMZ)

   - This zone acts as a buffer/semi-trusted zone between the trusted(inside) and untrusted zones(outside).
   - Hosts public-facing servers, like web servers and email servers, which need limited access from both the internet and the internal network.
   - It is partially trusted and is used to isolate these publicly accessible resources from the more sensitive internal network.

I can place firewalls, Intrusion Detection Systems (IDS), Intrusion Prevention Systems (IPS), and Unified Threat Management (UTM) devices in the screened subnet (also called the DMZ or semi-trusted zone) to enhance security.

## JumpBox

Internet-facing hosts are any servers that accept connections from the internet, such as a web or email server in the screened subnet.

Traffic to internet-facing hosts flows through the screened subnet, ensuring the internal network remains protected. For example, external users can connect to the web server but cannot access internal PCs.

Screened subnet hosts include web, email, communication, and proxy servers, which should be hardened due to their vulnerability to attacks.

Intrusion detection systems (IDS) are useful in this zone to monitor for potential threats. Attackers often try to compromise a host in the screened subnet and pivot into the internal network.

bastion hosts are servers in the screened subnet that do not run internal services, limiting their exposure.

Jumpboxes are used to securely manage and configure devices in the screened subnet. Administrators connect to the jumpbox, which then connects to servers in the subnet. Jumpboxes must be highly secured and can be either physical machines or virtual machines.

## ACL on the firewalls

Firewalls play a critical role in securing networks by controlling the flow of traffic through Access Control Lists (ACLs). ACLs are sets of rules applied to firewalls (and sometimes routers) that dictate whether traffic is permitted or denied based on criteria like port numbers, IP addresses, and protocol types.

ACLs filter traffic by using specific rules based on the source IP address, destination IP address, type of traffic (e.g., TCP/UDP), and port numbers. The rules are processed in a top-down manner, meaning traffic is evaluated against the rules starting from the top of the list.

It's common to place specific permit/deny rules at the top of the list and generic rules (like "deny all") at the bottom. Some devices have an implied deny rule for unmatched traffic, but it's a best practice to explicitly add a "deny all" rule at the end of an ACL.

Firewalls can be configured through web-based interfaces or command-line interfaces (CLI). Depending on the device, you can create rules to block or allow traffic based on port numbers, protocols (TCP/UDP), and IP addresses. Logging traffic and actions (e.g., blocked or permitted traffic) is also crucial for monitoring and auditing purposes.

### Example Configurations

- Hardware Firewall: Using a device like a NETGEAR wireless router, you can create ACLs to block or allow services (e.g., block Telnet on port 23 or restrict game access on port 666). Rules can be applied to specific IP ranges, blocking or allowing traffic based on predefined schedules or conditions.

- Windows Defender Firewall: You can configure inbound/outbound rules using the Windows Defender Firewall with Advanced Security tool. For example, you can allow SSH traffic over port 22 or block unsecure Telnet connections. Additionally, rules can be created for specific networks (private, public, domain), and the configurations can be exported for future use.

- macOS Firewall: On macOS, firewall settings can be accessed via Security & Privacy settings. You can block all incoming connections or allow specific applications (e.g., Skype, Google Drive) to bypass the firewall.

### Best Practices

- Ensure the most specific rules are placed at the top of the ACL, followed by more general rules.

- Always include a deny all rule at the end of the ACL to block any traffic that is not explicitly allowed.

- Log ACL actions for monitoring purposes, including both permitted and denied traffic.

## Content Filtering

Content Filtering is a network management practice that involves restricting access to certain content, websites, or applications based on specific criteria. It prevents exposure to inappropriate content, conserves network bandwidth, and comply with legal or organizational policies.

This can be achieved by:

- URL filtering : Method that can block access to specific websites based on URLs. This can be implemented through browser settings, proxy servers, firewall rules, or dedicated filtering software

- Keyword filtering : Involves scanning a requested webpage for specific keywords, then blocking it from being displayed if any of the blocked keywords are detected

- Protocol/Port filtering : Types of network traffic can be blocked based on the protocol or port used

Proxy Servers play a key role in content filtering and act as intermediaries between user devices and the internet

Different types of proxy servers:

- Web Proxy: Retrieves web pages from the internet and can also be used to bypass or enforce content filters.
- Reverse Proxy: Manages incoming traffic, improving security, load balancing, and caching resources.
- Transparent Proxy: Monitors and filters internet traffic, blocks specific content, and logs user activities without requiring user configuration.

Benefits of Proxy Servers:

- Improved Security: Filters out malicious traffic and prevents unauthorized access.
- Anonymity: Hides a user’s IP address to maintain privacy online.
- Content Blocking: Enforces company policies by restricting access to inappropriate content.
- Performance: Caches frequently accessed resources to improve load times.

## Internet of Thing (IoT)

Internet of Things (IoT) is the global network of appliances and personal devices that have been equipped with sensors, software, and network connectivity to report state and configuration data. These devices should be separated and segmented off from the business network. Because segregation of IoT devices is important for the business network's security.

### Examples of IoT devices

- Building and home automation systems (managing lighting, HVAC, water, security)
- HVAC controllers
- IP video systems (video conferencing, live streaming)
- Physical access control systems (proximity readers, biometric systems, security cameras)
- Scientific and industrial equipment (hospitals, factories, laboratories)

### IoT Device Types

- Hub and control systems : Central communication points for devices that rely on protocols like Z-Wave, Zigbee.

- Smart devices : Endpoint devices like smart thermostats, light bulbs, doorbells.

- Wearables : Devices like smartwatches, fitness trackers.

- Sensors : Devices that measure variables such as temperature, motion, light, humidity.

### Best Practices for IoT Network Security

- Understand endpoints : Each IoT device brings potential vulnerabilities.

- Track and manage devices : Avoid connecting unauthorized devices to the network.

- Patch vulnerabilities : Regularly patch IoT devices to fix security issues.

- Test and evaluate : Use penetration testing techniques before deploying IoT devices.

- Change default credentials : Always replace default usernames and passwords on devices.

- Use encryption : Apply encryption protocols to secure data transmission.

- Segment IoT devices : Place IoT devices in separate VLANs or subnets to avoid interference and enhance security.

## SCADA and ICS

Information Technology (IT) focuses on data and business networks, while Operational Technology (OT) deals with controlling physical systems (e.g., opening valves, generating power). OT is common in industries like manufacturing and power generation.

### Two main types of OT systems

- ICS (Industrial Control System)

  - Provides the mechanisms for workflow and process automation by controlling machinery using embedded devices.
  - Multiple ICSs can create a distributed control system (DCS).
  - ICS prioritizes availability and integrity over confidentiality since (CIA triad) the main goal is to maintain continuous operations.

  In order to interconnect all these industrial control systems, ICS uses a communication technology,

  - Fieldbus : Digital serial data communication protocol used in OT networks to link different PLCs

    - Programmable Logic Controller (PLC) : Type of digital computer used in industrial settings that enables automation and assembly lines, autonomous field operations, robotics, and other applications. To program this PLCs, HMI or Human-Machine Interface can be used. HMI can be a local control panel or software that runs on a computer

- SCADA (Supervisory Control and Data Acquisition) : Type of ICS used to manage large scale multi-site devices and equipment in a geographic region from a host computer

ICS - Single plant/system
DCS - Small connection of the ICS system in a single area
SCADA - Different ICS and DCS plants in a wide area network

## Bring Your Own Device

BYOD Policy allows employees to use their personal devices (laptops, phones, etc.) on the organization's network.

### Pros of BYOD

- Cost savings for the organization (no need to purchase devices).

- Employees use familiar devices.

### Cons of BYOD

- Security Risks: Personal devices could introduce vulnerabilities (e.g., malware from home use).

- Data Ownership: Unclear distinction between personal and company data.

### Ways to secure data for BYOD

1. Data Segmentation: Organizations use storage segmentation to separate personal and business data, either through technical or procedural solutions (e.g., separate apps for work and personal email).

2. Mobile Device Management (MDM): Companies may struggle to enforce security updates and policies on personal devices if employees refuse MDM installations. MDM is a centralized software solution for remote administration and configuration of mobile devices. It prevents certain applications from being installed on the device.

### Alternative Model - Choose Your Own Device (CYOD)

- Employees choose from a set of approved devices.

- The company controls the device through MDM, ensuring security (e.g., blocking apps, enforcing data loss prevention).

## Zero-trust Architecture

Devices and data are no longer confined to a secure perimeter(traditional cybersecurity strategies), necessitating new strategies.

Zero-Trust assumes that no user or device is inherently trusted, whether inside or outside the network. The principle is "trust nothing and verify everything" rather than the old approach of "trust but verify." Zero-Trust addresses threats from both external and internal sources by requiring continuous verification for every user, device, and transaction.

### Two different plan for Zero-trust Architecture

- Control Plane : Layout of the policies and procedures. Key elements include:

  - Adaptive Identity : Continual real-time validation of users' behaviors, devices, and locations.

  - Threat Scope Reduction : Limiting access to only what's necessary to reduce the attack surface.

  - Policy-Driven Access Control : Ensures users access only data relevant to their roles.

  - Secured Zones : Isolated environments for sensitive data, accessible only by authorized users.

- Data Plane: Execution of the policies and procedures

### four basic steps to verify and validate

1. Subject System : The user, device, or application requesting access.

2. Policy Engine : Verifies access requests against predefined policies.

3. Policy Administrator : Establishes and manages the access policies.

4. Policy Enforcement Point : The final gatekeeper that grants or denies access based on the policy engine's decision.

## Virtual Private Network (VPN)

VPN is used to extend a private network across a public network and enables sending and receiving data across shared or public networks.

### Types of VPNs

- Site-to-Site VPN: Connects two offices over a public network, serving as a cost-effective alternative to leased lines.

- Client-to-Site VPN: Allows individual remote users to connect to a corporate network.

- Clientless VPN: Establishes a secure connection through a web browser without requiring additional software, typically using SSL/TLS protocols.

### Tunnel Configurations

- Full Tunnel: Routes all traffic through the VPN, offering more security but reducing local network access and performance.

- Split Tunnel: Separates traffic, sending only necessary data through the VPN and the rest through the regular internet, improving performance but with reduced security.

### VPN Protocols

- Datagram Transport Layer Security (DTLS) : UDP-based version of the TLS protocol which operates a bit faster due to having less overhead.

- IPSec: Commonly used for authentication and encryption in VPNs.

- Older protocols: L2TP(Layer 2 tunneling protocol), L2F(Layer 2 forwarding), PPTP(Point-to-Point tunneling protocol), and SSTP(Secure Socket tunneling protocol), while still in use, lack native security features and are typically supplemented with encryption for secure communication.

## Remote Access Management

### various remote access methods to manage and configure servers, routers, switches, and firewalls

- Telnet (Port 23) : Sends text-based commands to remote devices but is insecure as it transmits data in plain text. It should not be used for sensitive configurations or to connect to secure devices.

- SSH (Secure Shell) (Port 22) : A secure alternative to Telnet, encrypting the connection and ensuring the security of commands and data during remote access.

- RDP (Remote Desktop Protocol) (Port 3389) : A Microsoft proprietary protocol that provides a graphical user interface (GUI) for remotely accessing and controlling Windows servers or clients.

- RDG (Remote Desktop Gateway) : Secures RDP connections by creating encrypted tunnels using SSL or TLS protocols, eliminating the need for VPNs.

- VNC (Virtual Network Computing) (Port 5900) : Similar to RDP but cross-platform, enabling remote access to Linux, macOS, or Windows systems with graphical control.

- VDI (Virtual Desktop Infrastructure) : Virtualizes desktop environments on centralized servers, often used in thin client setups or via a web browser. It is also referred to as Desktop as a Service (DaaS).

In-Band vs. Out-of-Band Management:

- In-Band Management uses the same network being managed (e.g., SSH or Telnet).
- Out-of-Band Management uses a separate network or a direct console connection for secure management, providing an additional layer of security. It prevents a regular user's machine from connecting to the management interfaces of devices.

- APIs (Application Programming Interfaces): Allow automated management, provisioning, and integration between different systems and services. Common API protocols include REST and SOAP.
