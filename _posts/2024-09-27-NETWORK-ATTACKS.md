---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ | network attacks
tags: [network, compTia, fundamentals, attacks, important]
comments: true
author: Lantana Park
---

# Network Attacks

## DoS and DDoS Attacks

- Denial of Service (DoS) attack occurs when one machine is continually flooding a victim with requests for services. It is really old version of attack. (Resource exhaustion)

flooding is a communication method where data packets are sent to all connected devices, even if they are not the intended recipients of the data.

To Achieve a denial of service attack with a single machine, attackers need to use TCP SYN Flood and Smurf Attack (ICMP Flood).

- TCP SYN Flood is a specific type of DoS attack that occurs when an attacker initiates multiple TCP sessions, but never complete those sessions.

- Smurf Attack (ICMP Flood) occurs when an attacker pings to a subnet broadcast with a spoofed source IP, making the victimized server appear as the source.

- Distributed Denial of Service (DDoS) Attack occurs when an attacker uses many computers all at the same time, asking for access to a single server. DDoS attacks should be prevented even when using cloud-based resources.

  - Botnet is the collection of compromised computers

  - Zombie is any one of the individually compromised computers

## MAC flooding

- MAC Flooding is a network attack technique that attempts to compromise the security of a network switch by attempting to overflow the switch's MAC table. During a MAC flooding attack, fake MAC addresses flood the switch, triggering a fail-safe mode where it behaves like a hub.

### Three main reasons an attacker want to do this attack

- Data Snooping occurs when an attacker **captures sensitive data** by forcing the switch to broadcast traffic. It enables the attackers to eavesdrop in promiscuous mode during a MAC flooding attack.

- **Disrupting Service** arises from MAC flooding, causing a DoS attack by overwhelming the network with unnecessary traffic.

- MAC flooding can **bypass security measures** like MAC address filtering. Switches may fail to enforce such restrictions, potentially allowing unauthorized devices to connect to the network.

### To secure network, I should

1. Use anomaly-based Intrusion Detection System (IDS)

2. Employ network monitoring tools

3. Configure port security to limit the number of MAC addresses on a single port

4. Set MAC address limits from each switch port

5. Implement VLANs to segregate traffic

## Address Resolution Protocol (ARP) Attacks

Address Resolution Protocol (ARP) is a fundamental concept in IP networking that is used to map an IP address to MAC addresses on a local area network.

Since ARP is really old protocol, there are many vulnerabilities on it.

1. ARP Spoofing is an attack wherein an attacker **sends falsified ARP messages over a LAN**. Attacker aims to associate their MAC address with a target IP address. ARP spoofing can be used to initiate an on-path attack inside of a Layer 2 network. (Attackers conduct a more targeted attack)

2. ARP Poisoning is a form of attack that **corrupts the ARP cache*** (ARP table) in the network. It allows an attacker to alter the network traffic flow, and enable data interception, session hijacking, or DoS attack. (Attackers target all devices in a LAN)

### How to perform ARP attack

1. Scanning for IP-MAC pairs and sending fake ARP responses

2. Conducting an ARP poisoning by conducting an ARP flood

### Detection & Prevention

- Detection : ARP monitoring tools and Intrusion Detection Systems (IDS) can track unusual traffic patterns.

- Prevention

  - Static ARP entries: Manually set IP-MAC mappings, though impractical for large networks.

  - Dynamic ARP Inspection (DAI): Modern switches inspect ARP packets and drop untrusted ones.

  - Network segmentation: Use VLANs to limit ARP attack scope.

  - Encryption: VPNs and encryption prevent data modification or interception, even if ARP attacks succeed.

## VLAN Hopping

Virtual Local Area Network (VLAN) is used to partition any broadcast domain and isolate it from the rest of the network at the data link layer (Layer 2) of the OSI model.

A VLAN creates separate logical networks on the same physical switch. Devices on different VLANs can’t communicate directly unless you configure special routing (just like needing a door between rooms).

When devices on different VLANs need to communicate, Layer 3 (using IP addresses) is needed for inter-VLAN routing.

As a network penetration tester, breaking out of a VLAN from a user's workstation is necessary to access sensitive network areas. It can be needed to attempt to bypass VLAN segmentation in order to gain unauthorized access to other parts of the network that are supposed to be isolated.

- VLAN Hopping is a technique that exploits a misconfiguration to direct traffic to a different VLAN without proper authorization.

### VLAN Hopping can be accomplished using

1. Double Tagging : A method where the attacker tries to reach a different VLAN using vulnerabilities in the trunk port configuration. Attackers add two VLAN tags to the frame — one outer tag(Native VLAN) and one inner tag(True destination). The switch strips the outer tag, and the inner tag tricks the network into forwarding the frame to a different VLAN. This allows the attacker to send traffic to another VLAN without authorization. Double tagging is a one-way attack since responses are not sent back to the attacker.

   - Double Tagging Attack prevention : Change default native VLAN (VLAN ID 1) to another identifier, Avoid adding user device to the native VLAN

2. Switch Spoofing : An attack technique that exploits the Dynamic Trunking Protocol (DTP) to make a victim’s switch think that the attacker's device is another switch. By doing this, the attacker can establish a trunk connection, gaining unauthorized access to multiple VLANs on the network.

   - Switch Spoofing prevention : Always configure switch ports to have dynamic switch port modes disabled by default.

3. MAC Table Overflow Attack : Allows VLANs to no longer be enforced. The attacker floods the switch with fake MAC addresses, causing the switch’s CAM table to overflow. Once overloaded, the switch operates like a hub, broadcasting traffic to all ports. This enables the attacker to sniff traffic from other VLANs.

   - MAC Table Overflow Attack prevention : Implement port security to prevent MAC table overflows.

## Domain Name System (DNS) Attacks

Domain Name System (DNS) is a fundamental component of the Internet that is responsible for translating human-friendly domain names into IP addresses.

- DNS Cache Poisoning (DNS Spoofing) : Involves corrupting DNS resolver cache with false information to redirect traffic

  - Prevention : Utilize Domain Name System Security Extensions (DNSSEC), Implement secure network configurations and firewalls

- DNS Amplification Attacks : Attackers exploit the DNS resolution process to overwhelm a target system with DNS response traffic

  - Prevention : Limit the size of DNS responses or rate limit any DNS response traffic to mitigate the impact of DNS amplification attack

- DNS Tunneling : Involves using the DNS protocol to encapsulate non-DNS traffic to attempt to bypass the organization's firewall rules

  - Prevention : Regularly monitoring DNS logs is important to analyze any signs of unusual patterns of behavior that could indicate DNS tunneling

- Domain Hijacking (Domain Theft) : Involves changing the registration of a domain name without the permission of the original registration

  - Prevention : Conduct regular updates, Ensure that account registration information is secure, Use domain registry lock services

- DNS Zone Transfer Attacks : An attack in which the attacker tries to get a copy of the entire DNS zone data by pretending to be an authorized system

  - Prevention : Restrict zone transfers to authorized DNS servers, Disable Zone transfer for public DNS zones

## On-path Attack

On-path Attack is the attack where the attacker or pentester places their workstation between two hosts to capture, monitor, and relay communications

- ARP Poisoning

- DNS Poisoning

- Rogue Wireless Access Point

- Rogue Hub/Switch

Once an on-path or interception attack has begun, attackers have to decide either to use a replay or relay type of attack.

- Replay Attack occurs when an attacker captures valid data and repeats it either immediately or with a delay

- Relay Attack occurs when the attacker is able to insert themselves between two hosts and become part of the conversation. In a relay attack, the attacker breaches both confidentiality and integrity by viewing and modifying the transaction details.

Replay | Data is captured and directly passed on
Relay | Data is intercepted, modified, and then passed on

To overcome the encryption scheme like TLS 1.3, SSL Stripping was created by attackers. Because a lot of websites used SSL and TLS as a way to encrypt data between the client and the server, the attackers might attempt to trick the encryption application into presenting the user with an HTTP connection instead of an HTTPS connection.

If SSL stripping is not possible, Downgrade Attack can be the alternative. It is an attack in which the attacker attempts to have a client or server abandon its higher security mode in favor of a lower security mode. By doing so, the attacker may allow the encryption to occur at a lower level, so it is much easier to crack in real time.

## Rogue Device and Attacks

Network devices are identified using the hardware interface MAC address and their IP address.

IPSec and HTTPS will make sure that only devices I authorize will get onto my network.

Rogue devices are unauthorized devices connected to a network, presenting a serious security risk. These devices can include unauthorized wireless access points (WAPs), servers, network taps, personal laptops, virtual machines, smart appliances, and even unauthorized software. Key concerns are that rogue devices can provide access to adversaries, capture sensitive data, or introduce malware into the network.

### Common Types of Rogue Devices

1. Network Taps: Devices attached to cabling that record network packets.

2. Wireless Access Points (WAPs): Rogue WAPs can extend physical networks to unauthorized users or be used as "evil twins" to trick users into connecting. A Wi-Fi Pineapple can be used to easily create a rogue access point.

3. Servers: Rogue servers may be set up by adversaries to steal credentials or mislead traffic using ARP poisoning.

4. Wired/Wireless Clients: Unauthorized personal devices like laptops or smartphones.

5. Software: Unauthorized software installations that can function as rogue DNS/DHCP servers or malware.

6. Virtual Machines: Spun-up VMs creating unauthorized servers and services.

7. Smart Appliances: Devices like smart TVs, webcams, and printers connected to the network, often vulnerable due to poor security patching.

### Detection Mechanisms

- Physical Inspection: Regular inspections of physical devices in ports and switches to detect unauthorized additions.

- Network Mapping & Host Discovery: Scanners to identify and map hosts via banner grabbing and fingerprinting.

- Wireless Monitoring: Scanning for unknown SSIDs or unexpected access points.

- Packet Sniffing: Identifying unusual traffic patterns or unauthorized protocols.

- NAC and Intrusion Detection: Tools that enforce authentication and detect anomalies in network traffic.

## Social Engineering Attacks

Social engineering is any attempt to manipulate users to reveal confidential information or perform actions detrimental to a system's security. Because, in most networks, the weakest link is end users and employees.

- Phishing : Sending an email to capture the most people and does not really target any particular person or group

  - Spear phishing : More targeted form of phishing

  - Whaling : Focused on key executives within an organization

- Tailgating : Entering a secure portion of the organization's building by following an authorization person into the area without their knowledge or consent

- Piggybacking : Similar to tailgating, but occurs with the employee's knowledge or consent

- Shoulder surfing : Coming up behind an employee and trying to use direct observation to obtain information

- Eavesdropping

- Dumpster diving : Scavenging for personal or confidential information in garbage or recycling containers

## Malware Attacks

Malware is malicious software designed to infiltrate computer systems and cause damage without the user's consent or knowledge.

- Viruses : Malicious code that requires user interaction to spread. It infects a computer when a user runs an infected file or program (e.g., through a downloaded game). Once executed, the virus replicates and spreads across the network.

- Worms : Similar to viruses but do not require user interaction. Worms exploit security vulnerabilities in operating systems or applications, allowing them to self-replicate and spread across networks, consuming system resources and potentially crashing systems. Notable examples include the Nimda and Conficker worms.

- Trojan Horses : Disguised as legitimate software, these malicious programs deceive users into installing them. While performing the advertised function, they secretly perform malicious tasks, like creating backdoors for remote access. Remote Access Trojans (RATs) are a common example.

- Ransomware : A type of malware that locks users out of their systems or encrypts their files, demanding payment (often in cryptocurrency) to restore access. High-profile ransomware attacks have affected governments and corporations, such as the Samsam ransomware attack on the City of Atlanta.

- Spyware : Software that secretly gathers user information, such as browsing habits or personal data, without consent. A subtype, adware, collects information to display targeted ads, while keyloggers capture keystrokes and sensitive information like passwords.

- Rootkits : Malware designed to gain undetected administrative-level control of a system. Rootkits are difficult to detect because they operate at a low level, often hiding within system firmware, and may require scanning from an external boot device to identify.
