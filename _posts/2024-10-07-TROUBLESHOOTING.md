---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - troubleshooting (1)
tags: [network, compTia, fundamentals, troubleshooting, first]
comments: true
author: Lantana Park
---

# Troubleshooting Methodology

1. Identify the problem

   - Ask questions to the users for gathering information. Such as, What happened?, What was the status before?, What was the status after?, Is there any change in the system?

2. Establish a theory of probable cause

   - Question the obvious things
   - Look up the problem using external research/documentation (Internet)
   - Look up the problem using Internal research/documentation (System)

3. Test the theory to determine the cause

   - Go back to steps 1 to three if the theory is not correct

4. Establish a plan of action to resolve the problem and identify potential effects

5. Implement the solution or escalate as necessary

6. Verify full system functionality and, if applicable, implement preventative measures

7. Document findings, actions, outcomes, and lesson learned

# Troubleshooting Tools

## Hardware Tools

1. Snips/Cutters : Used to cut cables from a spool, including twisted-pair copper, coaxial, or large cable bundles.

2. Cable Strippers : Removes the outer jacket of the cable to expose wires for connector attachment, like RJ45 for Ethernet or RG6 for coaxial.

3. Cable Crimpers : Attaches connectors (RJ45, RJ11 for Ethernet; RG6, RG59 for coaxial) to cables.

4. Cable Testers : Verifies the continuity and pinout configuration of each wire in the cable to ensure proper connection (e.g., straight-through or crossover cables).

5. Wire Maps : Diagnoses issues in Ethernet cables, such as open, shorted, or cross pairs.

6. Cable Certifiers : Determines the category and data throughput of cables (Cat5, Cat6, etc.) and provides information like cable length and resistance.

7. Multimeters : Measures voltage, resistance, and amperage in cables to check for breaks or test power outlets.

8. Punch Down Tools : Used for terminating cables on punch-down blocks (e.g., 66 or 110 blocks).

9. Tone Generators : Helps identify copper cables run by generating a tone that is detected at the other end, useful for tracing cables.

10. Loopback Adapters : Creates a loop in the network for testing connectivity by connecting transmit and receive pins.

11. Time-Domain Reflectometers (TDR) : Locates breaks in copper cables and measures the distance to the fault.

12. Optical Time-Domain Reflectometers (OTDR) : Similar to TDR, but used for fiber optic cables to detect breaks and measure light loss.

13. Fiber Light Meters : Measures how effectively a fiber cable transmits light, using LEDs for multimode and lasers for single-mode fibers.

14. Fusion Splicers : Joins fiber optic cables by fusing the fibers together.

## Software Tools

1. Wi-Fi analyzer : Used to conduct wireless surveys to ensure proper coverage and to prevent non-desired overlap between wireless access point coverage zones and channels

2. Protocol analyzer and packet capture : Protocol analyzer is used to **capture and analyze signals and data traffic over a communication channel** and Packet Capturing Tool is used to capture packets running over a network connection in real time and save for later analysis

3. Bandwidth speed test : Verifies the real-world throughput from a client device all the way out to the Internet and back

4. Port scanner : Determines which ports are open on a network

5. NetFlow analyzer : Performs monitoring, troubleshooting and in-depth inspection, interpretation, and synthesis of traffic flow data

6. IP scanner : Used to search for and detect IP addresses and other information related to devices on the network

# Troubleshooting Physical

## Cable Signal Issues

1. Attenuation

   - Attenuation is the loss of signal strength over the length of a cable.

   - It occurs in both wired and wireless connections but is emphasized here for wired connections.

   - In copper cables (e.g., twisted pair, coaxial), electrical signals representing binary data weaken as they travel due to resistance.

   - The maximum effective length for twisted pair cables is about 100 meters, while coaxial cables can reach about 500 meters due to better shielding.

   - Other factors affecting attenuation include frequency, environmental noise, and physical surroundings (e.g., temperature, wall construction).

   - Solutions include using appropriate cables for the environment, shortening cable lengths (recommended maximum of 80 meters), and employing amplifiers or repeaters to boost signals over longer distances.

2. Interference

   - Interference occurs when cables operating at the same frequency are in close proximity, which can degrade the signal.

   - To minimize interference, use high-quality twisted pair cables with more twists per inch, and plan cable runs to avoid proximity to high-power cables.

3. Decibel (dB) Loss

   - dB loss measures signal deterioration in copper and fiber cables.

   - For copper cables, it reflects voltage loss, while for fiber, it reflects light loss.

   - High dB loss in copper indicates the need for higher quality cables or additional shielding; for fiber, it may require using higher quality cables or cleaning connectors.

### Tools

| Copper Cable | Fiber Cable
Attenuation | Cable certifier | Fiber light meter
Interference | Spectrum analyzer
Decibel loss | Cable certifier, Cable analyzer | Fiber light meter

## Copper Cable Issues

1. Incorrect Pinouts: If a twisted pair network connection fails, check the pinout at the patch panel, wall jack, or RJ45 connector. Patch panels typically follow TIA-568-B standards, where pins 1-8 have specific color codes (e.g., white/orange, orange, etc.). Inspect the punch down block or use a cable tester to confirm the correct pinout.

2. Bad Ports : Network interface cards (NICs) and switch/router ports may malfunction. Use a loopback plug and specialized software to test ports. If faulty, replace the NIC or switch the connection to another port.

3. Opens and Shorts : An open occurs when there’s no connection or a wire break. Test each part of the cable to locate the break. A short happens when two wires are touching, typically caused by improper wiring. Rewire or replace the cable if needed.

## Fiber Cable Issues

1. **Incorrect Transceivers** : A transceiver is a device that transmits and receives data, often used in routers and switches to convert network connections. Using the wrong transceiver can cause connectivity issues. Transceivers are typically hot-pluggable, meaning they can be replaced without shutting down the device. However, the correct transceiver type must be used to avoid data loss and connectivity problems.

2. **Reversed Transmit/Receive Connections** : Fiber connections usually consist of two cables—one for transmitting data (TX) and one for receiving it (RX). If these cables are reversed, there will be **no valid connection**. This can be easily resolved by swapping the TX and RX cables and checking the LED activity lights to confirm the connection is active. This occurs **mismatch in wavelength specifications**. It is important to ensure compatibility in terms of speed, type, and wavelength by connecting the correct connection and transceivers.

3. **Dirty Optical Cables** : Dust, dirt, or fingerprints on fiber optic cables and connectors can block the optical signal, leading to performance issues or connection problems. Cleaning methods include dry cleaning (using a dry cloth) for dust or dirt, and wet cleaning (with isopropanol alcohol) for oils or fingerprints. Regular cleaning is essential to maintain optimal fiber performance, especially if errors or slowdowns occur, which can be detected with a fiber light meter.

## Ethernet Issues

1. LED Status Indicators: Network interface cards (NICs) have two key LED lights:

   - Activity Light: Shows the status of the network link. If off, there's no connection. A solid orange light indicates an established connection, while a blinking orange light means data is being transmitted.

   - Link Speed Light: Indicates the speed of the connection. A green light shows 1 Gbps, orange shows 100 Mbps, and no light indicates 10 Mbps. These lights are also present on network switches to help monitor the status of each Ethernet port.

2. Duplexing Issues: A duplex mismatch occurs when one device on an Ethernet connection operates in full duplex mode (sending and receiving simultaneously), and the other is in half duplex (sending or receiving, not both). This mismatch can cause high packet loss without significant jitter. To avoid duplex mismatches, it's important to configure both devices for auto-negotiation or manually set them to full or half duplex, depending on the network requirements. Full duplex is preferred when using switches, as each port on a switch is its own collision domain.

## Interface Issues

1. **Cyclic Redundancy Check (CRC) Errors** : These occur when the integrity of data is compromised during transmission, often due to interference, cable damage, or hardware faults. An increasing number of CRC errors signals a physical issue in the network.

   - **Cyclic Redundancy Check (CRC)** is a method used to detect errors in data transmission. It works by performing a mathematical calculation (checksum) on the data packets before they are sent. This checksum is then sent along with the data. The receiving server also calculates the checksum for the received data and compares it with the checksum sent. If they do not match, it indicates that the data has been corrupted during transmission.

2. Runts : These are frames smaller than the minimum size, often caused by collisions or network card malfunctions. Monitoring runts helps maintain network integrity.

3. Giants : Frames larger than the maximum size, typically caused by device misconfigurations, can lead to network congestion. Network devices may drop oversized frames to prevent issues.

4. Drops : Occur when a device’s buffer is full, leading to discarded packets, often caused by bandwidth bottlenecks or overloaded hardware. Persistent drops require traffic management or hardware upgrades.

5. Error Disabled Port Status : Ports may shut down automatically due to policy violations or errors, such as preventing network loops. Manual intervention or specific commands are needed to reactivate the port.

6. Administratively Down Port Status : Indicates a port has been intentionally disabled by an administrator, often for maintenance or upgrades. To reactivate it, a command like no shutdown is used.

7. Suspended Port Status : Happens when there's a violation of protocol, such as a misconfigured ether channel. Resolving the configuration issue is necessary to restore the port’s functionality.

## Power of Ethernet (PoE)

### Two PoE types:

- PoE (IEEE 802.3af) – delivers up to 15.4 watts of power, with a minimum of 12.95 watts guaranteed due to power loss over cables.
- PoE+ (IEEE 802.3at) – provides up to 30 watts, with a minimum of 25.5 watts guaranteed.

### PoE Issues:

1. Power Budget Exceeded : This occurs when the combined power needs of all connected devices surpass the capacity of the PoE switch. Symptoms include devices restarting, not powering on, or malfunctioning. To fix this, check and manage the power requirements of connected devices or upgrade to a switch with a higher power budget.

2. Incorrect Standard : This happens when PoE+ devices requiring 30 watts are connected to older PoE switches that only provide 15.4 watts. The device may not function properly or fail to power up. To resolve this, ensure compatibility between the device and switch, or use PoE injectors or upgrade the switch.

# Wireless Issues

## Wireless Coverage Issues

### Signal Measurement

- RSSI (Received Signal Strength Indicator): Measured in decibels (dB) from the client’s perspective.

- EIRP (Effective Isotropic Radiated Power): Measured in dBi from the access point’s perspective.

Insufficient wireless coverage is one of the most common issues experienced by Wi-Fi users because RSSI decreases whenever the signal has to penetrate through the floor.

Tools: Signal booster, Larger antenna, Wireless repeater, Second access point

## Interference Issues

1. Interference

   - Definition: Occurs when multiple networks use the same channel, leading to signal overlap and slowdowns.
   - 2.4 GHz Spectrum: Use channels 1, 6, and 11 to minimize interference. Avoid overlapping channels (e.g., channels 4 and 6).
   - Placement Strategy: Arrange access points in a sequence (e.g., 1, 6, 11) with 10-15% overlap for coverage. For 5 GHz networks, use a honeycomb pattern.

2. Attenuation

   - Definition: Reduction of signal strength due to distance, obstacles, or poor-quality components.
   - Multi-path Reception: Signals can bounce off walls, causing delays and weaker signals, impacting throughput.
   - Mitigation: Use high-quality cables and antennas to reduce attenuation and improve signal quality.

## Client Disassociation Issues

### Disassociation Causes

1. Idle Timeout: Occurs after 300 seconds (5 minutes) of inactivity, allowing other clients to connect. Keep-alive packets can prevent disassociation.

2. Session Timeout: Happens after 1800 seconds (30 minutes), requiring clients to re-authenticate automatically.

3. Wireless Network Changes: Changes (e.g., passphrase updates) disable and re-enable the network, forcing all clients to reconnect.
4. Manual Deletion: An administrator can manually disconnect a client from the network.

5. Authentication Timeouts: If the authentication process takes too long, the client is disassociated and must re-authenticate.

6. Access Point Radio Resets: Resetting the access point causes disassociation, requiring clients to reconnect.

Continuous de-authentication may indicate a de-authentication attack, where attackers disconnect clients to capture packets and crack the network passphrase.

It's crucial to check wireless gateway and controller logs to identify whether disassociation is due to legitimate reasons or potential security threats.

## Incorrect Wireless Configuration

- Wrong SSID

  SSID (Service Set Identifier) is a natural language name used to identify a wireless network in an 802.11 network.

  Essentially it acts as the name of the network, for example, Cafe_Brew, Library_Guest_WiFi. in public wifi.

  It is crucial to avoid mistyping to prevent an incorrect SSID error.

  If I connect to wrong SSID, it is likely to get malware infection or On-Path attack.

- Incorrect passphrase

  If I connect wireless network using the correct SSID, I need to enter a correct pre-shared key or passphrase.

  Passphrase/pre-Shared Key is used to encrypt and decrypt data sent and received by a wireless network

  Solution: Attempt to reinstall the drivers for the wireless adapter

- Encryption mismatch

  Encryption algorithms

  WEP | RC4
  WPA | TKIP
  WPA2 | AES

  Error message "Network security key mismatch"

  Possible causes

  - Wrong password or passphrase
  - Wrong encryption protocol

  Mitigation

  1.  Manually change protocol type

  2.  Disable third-party antivirus tools

  3.  Reinstall wireless drivers

## Captive Portal Issues

Captive Portal is a web page displayed to newly-connected Wi-Fi users before being granted broader access to network resources.

In general, captive portal is implemented by using an HTTP redirect, ICMP redirect or DNS redirect.

- HTTP Redirect : Redirects all traffic to a web server which then redirects them to a captive portal using a 302 HTTP status code

- ICMP Redirect : Sends error messages and operational information indicating the success or failure of communicating with another IP address

- DNS Redirect : The client is redirected by the onboard DNS server to the captive portal webpage

### Typical issues

1. Open a web browser and try to go to any website : Sometimes the mobile devices do not automatically load up the captive portal page. If that issue occurs, try to go to any website.

2. Determine default gateway for wireless network and enter `http://` and default gateway's IP address, then press enter.

3. Verify DNS server IPs and allow DHCP to autoconfigure the DNS server when connecting to the wireless network

## Wireless Considerations in troubleshooting

1. Antennas

   ### Types

   - Omnidirectional : Radiates signal evenly in all directions. Common in Wi-Fi setups, typically with vertical polarization. Signal strength weakens with distance, measured by RSSI (Received Signal Strength Indicator).
   - Dipole (Bi-Directional) : Focuses signal in two directions, offering stronger RSSI at distance, but not widely used in typical wireless networks.
   - Yagi : Unidirectional antenna used for long-distance, site-to-site connections.
   - Parabolic Grid/Disc : Also unidirectional, used for longer distances than Yagi antennas.

Antennas must be placed strategically, considering obstructions (e.g., trees, snow, rain) for outdoor setups.
Correct polarization (vertical or horizontal) is key for optimal signal strength and RSSI. Most Wi-Fi networks use vertical polarization.

2. Channel Utilization

   - Definition: Measures how much airtime a channel is being used. High channel utilization (over 30%) results in slow wireless performance.
   - Collision Avoidance (CSMA/CA): Devices listen for active transmissions before sending data to avoid collisions. High traffic on a channel increases congestion and wait times for transmissions.
   - Solution: Conduct site surveys to identify underutilized channels or move to a less crowded frequency band (e.g., 5 GHz for 802.11ac).

3. Site Surveys

   - Purpose: Plan wireless network layout to ensure optimal coverage, data rates, and minimize interference. Surveys help identify optimal access point placement and signal strength.
   - Power Levels: Use EIRP (Effective Isotropic Radiated Power) to fine-tune power settings of wireless access points.
   - Frequency Bands: Moving to higher frequencies like 5 GHz provides more non-overlapping channels (24 channels vs. 3 in 2.4 GHz).

4. Wireless Access Point (AP) Association

   - Process: A client connects to an AP through a seven-step process, starting with probe requests and ending with secure association.
   - BSSID Broadcast: Clients send probe requests to discover nearby APs, and APs respond if they support the requested data rates.
