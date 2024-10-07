---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - network monitoring
tags: [network, compTia, fundamentals, monitoring]
comments: true
author: Lantana Park
---

# Network Monitoring

Network monitoring is used to ensure that the network's operational integrity and optimal performance can detect and report on issues.

## Intrusion Detection and Protocol Systems (IDS/IPS)

An IDS is a passive device that monitors network traffic, logs suspicious activity, and alerts administrators but does not block or stop attacks.

An IPS is an active device placed in-line with network traffic, monitoring and blocking malicious activity to prevent attacks in real time. It can be installed between the firewall and the switch/router.

IPS systems can cause issues by blocking legitimate traffic if not properly configured, leading to a higher preference for IDS in some organizations.

Snort : Is a widely-used, open-source IDS/IPS that can detect attacks and, in the case of IPS, block them.

### Detection Mechanisms of IDS/IPS

- Signature-based: Matches patterns of known threats (malware signatures).

- Policy-based: Triggers alerts based on violations of predefined policies (e.g., blocking telnet traffic).

- Anomaly-based: Detects deviations from normal traffic patterns, either statistically (based on traffic data) or manually set thresholds (e.g., flagging large downloads).

### Host-based vs. Network-based systems

- Network-based IDS/IPS protects the entire network and monitors traffic between devices.

- Host-based IDS/IPS is installed on individual devices (like PCs, servers) to protect them from unauthorized software or actions.

Network and host-based systems can work together for more protection.

## Simple Network Management Protocol (SNMP)

SNMP is an internet protocol used to collect and organize information about managed devices on IP networks, and to modify that information to change device behavior. Include routers, switches, firewalls, printers, servers, and client devices. These devices communicate with an SNMP manager.

### SNMP Architecture

- Manager: Central machine (usually a server) running SNMP to collect and process data from network devices (agents).

- Agents: Network devices running SNMP services that send information to the manager either at regular intervals or upon request.

### Message Types

- Set: Manager requests changes to a variable on an agent.
- Get: Manager requests information from an agent.
- Trap: Agents send notifications to the manager about significant events without manager requests (asynchronous).

### Trap messages Encoding

- Granular Traps: Sends a unique object identifier (OID) to identify specific messages, reducing redundant data.
- Verbose Traps: Sends detailed information in a payload, consuming more bandwidth and resources.

### SNMP Versions

- SNMPv1 & v2: Uses insecure community strings (in plain text) for access, making them vulnerable.

- SNMPv3: Introduced integrity (hashing), authentication (message source validation), and confidentiality (encryption using DES, 3DES, or AES). Offers improved security through message integrity(message hashing), authentication(source validation), and confidentiality(data encryption). Supports grouping of components for granular access control (read, write, or read-write permissions).

## Network Sensors

Network sensors (routers, switches, and firewalls) monitor the performance of network devices, including temperature, CPU usage and memory.

1. Temperature Sensors can be used to measure the air temperature inside the intake outlet and the air temperature at the exhaust outlet.

   - Minor Threshold is used to set off an alarm when a rising temperature is detected.

   - Major Threshold is used to set off an alarm when a temperature reaches dangerous conditions.

   Devices can start to load shed by turning off different functions to reduce temperature.

2. CPU Utilization: Under normal conditions, devices use 5-40% CPU. High utilization indicates potential issues such as misconfiguration or an attack, possibly leading to packet drops or connection failures.

3. Memory Utilization: Typically around 40% under normal conditions, it can rise to 60-80% during peak times. Constantly high memory usage may indicate the need for more powerful devices or potential network attacks.

## Packet Captures

Packet Capture is used to capture all the data going to or from a given network device.

1. port scan packet

2. DoS attack packet capture

3. DDoS attack packet capture

## Network Flow Data

In order to best monitor traffic in the network, full packet capture and netFlow data can be used. It takes up so much space.

- Full Packet Capture captures the entire packet including the header and the payload.

- NetFlow Data is used in most businesses and organizations. It conducts flow analysis. It highlights trends and patterns, and records metadata and statistics about network traffic, instead of every single packet, using a flow collector. NetFlow and Flow Analysis provide detailed metadata on network traffic, excluding full packet content.

### Tools for traffic flow analysis

1. NetFlow : A Cisco-developed means of reporting network flow information to a structured database. It defines traffic flow based on different packets that share the same characteristics.

   - Source/destination IP addresses

   - Source/destination port

   - Network protocol interface

   - IP service type

   - IP version/type

2. Zeek : A hybrid tool that passively monitors networks like a sniffer. It logs the entire packet when it detects something of interest based on configured parameters and rules. It performs normalization of data and stores it in tab-delimited or JSON text file.

3. MRTG (Multi Router Traffic Grapher) : Used to create graphs to show network traffic flows going through network interfaces on different routers and switches.

   - In normal case spike, it may indicates an off-site backup, sending all data to a cloud service provider

   - In malicious case spike, it may indicates data exfiltration, sending data to the bad actors

## Log Aggregation with Syslog

All of the network devices generates logs based on Information, Events, Warnings, Alerts and other data that they generate.

Instead of checking log of each device manually, I can use System Logging protocol (Syslog). It sends system log or event messages to a central server, called a syslog server.

It can be called Security Information Management (SIM), Security Event Management (SEM), or Security Information and Event Management (SIEM).

When I configure my syslog server, there are two primary components I have to have,

- Client : Device sending the log information to the syslog server. This can be a router, switch, firewall, web server. It sends the data over port 514 using UDP.

- Server : Receives and stores the logs from all of the clients

### Different severity levels

Level | Condition | Indication
0 | Emergency | The system has become unstable
1 | Alert | A condition should be corrected immediately
2 | Critical | A failure in the system's primary application requires immediate attention
3 | Error | Something is preventing proper system function
4 | Warning | An error will occur if action is not taken soon
5 | Notice | The events are unusual
6 | Information | Normal operational message that requires no action
7 | Debugging | Useful information for developers

I can review these inside the syslog server as well as looking at the traffic logs and audit logs.

- Traffic logs contains information about the traffic flow on the network. Traffic logs allow for investigation of any abnormalities.

- Audit logs contains a sequence of events for a particular activity.

In Windows, There are three main different types of logs

- Application logs contain information about software/application running on a client or server. It has three security level, information, warning, and error.

- Security logs contains information about the security of a client or server.

- System logs contain information about the operating system itself. There are three security warning level as application log, information, warning, and error.

## Security Information and Event Management (SIEM)

Security Information and Event Management (SIEM) provides real-time or near-real-time analysis of security alerts generated by network hardware and applications. It gathers logs and data from all sorts of different systems. Conducting log reviews should be something that's done regularly and routinely. SIEM takes data using the Syslog protocol, typically through UDP port 514 or TCP port 1468.

### Key Functions of SIEM

1. Log Collection: Collects event records from all network devices (via Syslog, usually on UDP port 514 or TCP port 1468), providing forensic tools and aiding compliance reporting.

2. Normalization: Converts log messages from different formats into a common model, making it easier to analyze related events across diverse systems.

3. Correlation: Links events from different systems, speeding up threat detection and response.

4. Aggregation: Reduces event volume by consolidating duplicates, improving data clarity.

5. Reporting: Provides real-time dashboards for analysts and summary reports for management, ensuring quick decision-making and historical analysis.

SIEM systems can be implemented as software, hardware appliances, or outsourced services. Proper configuration ensures continuous data flow, enhancing security and compliance through efficient log management and threat detection.

### Considerations for SIEM Deployment

- Log relevant events, filter out irrelevant data.
- Define scope and establish use cases to identify threats.
- Plan incident responses for different scenarios.
- Implement a ticketing system to track flagged events.
- Schedule regular threat-hunting activities to catch undetected threats.
- Provide auditors with an evidence trail via the centralized data repository.

## Network Performance Metrics

Network Performance Monitoring focuses on the end user's experience by monitoring the performance from the user's workstation to the destination, unlike traditional monitoring, which focuses on point-to-point performance.

### Three Key Metrics

1. Latency: Measures the time it takes for data to reach its destination and return, measured as round-trip time in milliseconds.

2. Bandwidth/Throughput: Bandwidth refers to the theoretical maximum data transfer rate, while throughput measures the actual transfer rate in practice.

3. Jitter: The variation in delay between data packets, which can cause issues in real-time applications like VoIP or video conferencing.

Ensuring low latency, sufficient bandwidth, and minimal jitter is essential for maintaining network performance.

## Interface Statistics

Interface statistics are critical for monitoring and troubleshooting the performance of network devices like routers, switches, and firewalls. Interface statistics are collected directly from network devices, such as switches and routers, and show real-time performance metrics (like traffic load, errors, and link status) for specific network interfaces.

1. Interface Definition: Interfaces are physical or logical ports on network devices. Each interface generates its own statistics to provide performance data.

2. Link State: Indicates whether the interface is physically connected and operational. For example, "up" means the interface is active and transmitting data.

3. Speed and Duplex Status: Shows the speed of the connection (e.g., 100 Mbps) and whether it operates in full or half duplex mode. Full duplex allows simultaneous sending and receiving, while half duplex reduces performance.

4. MTU (Maximum Transmission Unit): Commonly set to 1500 bytes for Ethernet, this defines the largest packet size the interface can handle.

5. Reliability: Measures the stability of the connection, with values like 255/255 indicating no errors.

6. Transmit (TX) and Receive (RX) Load: Reflects how busy the interface is with sending and receiving traffic, respectively.

7. Error Statistics:

   - CRC (Cyclic Redundancy Check) Errors: Indicates data frame errors due to data corruption. And physical layer issues such as faulty cables.

   - Runts and Giants: Frames that are too small (under 64 bytes) or too large (over 1518 bytes). Packets that are too large (giants) or too small (runts) compared to standard sizes, which can indicate configuration issues or problems on the network.

   - Overruns and Ignored Packets: Indicate hardware buffer issues or packet overload.

   - Collisions: Occur in half duplex or poor configurations, leading to retransmissions.

8. Output Queue & Packet Drops: Shows the number of packets waiting to be transmitted. Dropped packets can indicate congestion or mismatched speeds.

9. Encapsulation Types: Ethernet typically uses ARPA (Advanced Research Projects Agency) as the encapsulation method for transmitting frames.

10. Queueing Strategy: The default is FIFO (First In, First Out), affecting how packets are handled during traffic surges.

11. Troubleshooting Insight: Interface statistics can help diagnose issues like slow network performance due to half duplex configurations or congestion from mismatched speeds (e.g., 100 Mbps vs. 20 Mbps).
