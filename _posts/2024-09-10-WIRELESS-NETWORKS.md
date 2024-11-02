---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ | Wireless Networks
tags: [network, compTia, fundamentals, wireless]
comments: true
author: Lantana Park
---

# Wireless network

## Wireless Network Types

1. **Ad Hoc** / **Independent Basic Service Set** (IBSS) are networks where devices **connect directly to each other** rather than through a central access point. Ad Hoc network does not typically provide Internet access. Ad Hoc or peer-to-peer configuration allows sharing and collaboration, as long as the devices are within range.

   ### When might I want to use ad hoc wireless network?

   **Quick file sharing between two devices without setting up a full network**.

2. **Infrastructure Wireless Networks** are a more organized setup in which devices like laptops and smartphones are going to be **connected to a network through a wireless access point** that will then bridge my wireless clients onto the wired local area network.

   ### Components

   **Basic Service Set Identifier (BSSID)** is the **unique identifier** for each AP. It has a set to the MAC address of the wireless access point.

   **Service Set Identifier (SSID)** is a common alphanumeric network name that end users can search for to connect to the wireless network. It is something like `TP-Link_015040`, `netgear37`, or `Linksys00042`

   **Extended Service Set (ESS)** creates a **larger network** that shares the name SSID to allow for seamless connectivity across a building.

3. **Point-to-point Wireless Networks** are designed to **connect two distinct locations** over long distances using high-gain antennas. It is highly efficient and offer dedicated bandwidth between two points.

4. **Wireless Mesh Mesh Networks** are versatile and resilient form of wireless networking. It has **self-healing capability with multiple APs** and can reconfigure themselves around broken or blocked pathways. Mesh networks are also **great for large scale deployments** when I cannot lay cables. **It routes data through alternative paths if one fails**.

5. **Autonomous Access Point** is **a standalone device that contains all of the intelligence to handle wireless networking functions independently**.

6. **Lightweight Access Point** is **multiple access points connecting back to a centralized controller**.

## Wireless Antennas

Wireless antennas are simply devices that are designed to send and receive radio frequency signals.

- **Omnidirectional antennas** are designed to transmit and receive wireless signals **in all directions equally**. It is great for covering a broad area with a relatively uniform signal strength.

Mobile hot spot, wireless public networks.

- **Unidirectional Antennas** focuses on a single direction to provide a more concentrated signal beam. Unidirectional antennas are suitable for **long and narrow coverage areas or a strong signal in one particular direction**.

- **Yagi antenna** is a specific type of directional/unidirectional antenna that can provide high signal gains and uses a narrow beam-width. A yagi antenna is best when capturing or sending signals over **long distances to or form a specific, fixed location**.

## Wireless Antennas

1. Omnidirectional Antenna

   - Found in most wireless access points and mobile devices.
   - Transmit and receive signals in all directions. (360 degrees)
   - Ideal for environments where devices move around because it covers broad areas. (e.g., smartphones connecting to Wi-Fi or cellular networks)

2. Unidirectional Antennas

   - Focuses signals in one direction for longer distances.
   - Used in specific scenarios, like wireless penetration testing, to target a single direction for more power.

3. Parabolic Antennas

   - A type of unidirectional antenna with a curved dish design, used for focused signal transmission (e.g., satellite TV).
   - Maximizes signal strength by directing the transmission in one direction.

4. Yagi Antennas

   - Another form of unidirectional antenna, typically used for long-range wireless communication between fixed buildings/locations.
   - Common in business parks or campus settings to connect multiple buildings.

## Wireless Frequencies

Wireless frequencies are the different frequency bands that are used to transmit and receive the radio waves used by the wireless networks to send data.

- **2.4 GHz**(2.400 GHz to 2.495 GHz) - One of the most widely used frequencies for wireless networking and is known for **its long-range and better penetration through solid objects**. It has **the slowest data transfer speeds** due to having smaller channel widths and fewer non-overlapping channels. Which can lead to **interference and retransmission of the data**.

- **5 GHz**(5.725 GHz to 5.875 GHz) - There are **more non-overlapping channels** of 20 MHz per channel when working in a 5 GHz-based 802.11 wireless network. It has **less interference and higher levels of performance**. It has **a shorter range** than the 2.4 GHz band. (Video streaming and gaming). It has **faster data transfer speed**.

- **6 GHz**(5.925 GHz to 7.125 GHz) - It is a relatively new spectrum opened up for Wi-Fi use that offers even **more channels and bandwidth to allow for faster connections and less congestion**. It does provide the **shortest distances for its coverage**, and offer the least amount of solid object penetration for the use cases.

**Band steering** directs devices to connect to the less congested frequency band, optimizing the performance of the wireless network by balancing the load between the 2.4 GHz and 5 GHz bands.

**Beamforming** focuses wireless signals in specific directions to **improve signal strength**.

**Channel bonding** combines multiple channels to increase bandwidth.

## 802.11 Standards

The 802.11 standards are a set of protocols developed by the Institute of Electrical and Electronics Engineers (IEEE) for implementing wireless local area network (WLAN) communications. These standards define how wireless devices like laptops, smartphones, and routers communicate over radio waves. Each version of 802.11 improves performance, speed, and range, and supports different frequency bands.

1. **802.11a** (Wireless A)

   - Frequency: 5 GHz
   - Speed: 54 Mbps
   - Range: 35 meters
   - Higher cost made it primarily used by businesses

2. **802.11b** (Wireless B)

   - Frequency: 2.4 GHz
   - Speed: 11 Mbps
   - Range: 140 meters
   - Lower cost made it widely adopted in homes and schools. (Security cameras, Walkie talkies, baby monitors, microwaves)

3. **802.11g** (Wireless G)

   - Frequency: 2.4 GHz
   - Speed: 54 Mbps
   - Range: 140 meters
   - Combined Wireless A’s speed with Wireless B’s affordability

4. **802.11n** (Wireless N / Wi-Fi 4)

   - Frequency: 2.4 GHz & 5 GHz
   - Speed: 600 Mbps
   - Range: 70 meters (2.4 GHz) and 35 meters (5 GHz)
   - Introduced **MIMO (multiple-input, multiple-output) for faster data transfer**. MIMO technology allows an access point to use multiple antennas to send and receive data at faster speeds

5. **802.11ac** (Wireless AC / Wi-Fi 5)

   - Frequency: 5 GHz
   - Speed: 6.9 Gbps
   - Range: 35 meters
   - Introduced **MU-MIMO (multi-user MIMO)** for simultaneous connections by multiple users. **High speed and reliability**

6. **802.11ax** (Wireless AX / Wi-Fi 6)

   - Frequency: 2.4 GHz, 5 GHz, and optionally 6 GHz (Wi-Fi 6E)
   - Speed: 9.6 Gbps
   - Range: Varies by band
   - Supports all previous wireless standards and enhances performance with **MU-MIMO and OFDMA** (Orthogonal Frequency Division Multiple Access).

- Wireless B, G, N, and AX support 2.4 GHz.
- Wireless A, N, AC, and AX support 5 GHz.
- Wi-Fi 6E supports 6 GHz.
- Higher speeds often come with reduced coverage distances for a single access point

## Wireless Security

Two mechanisms to authentication in the wireless networks,

- Pre-Shared Key (PSK) is a mode of security authentication where the **same password or key is being used on both the wireless access point and any connecting client devices** trying to gain access to the network. It is a string and password string that I use to connect the wifi access.

  Problems,

  - **Unscalable** because everyone knows this key string.
  - There is **no individual user accountability** because every user is using the exact same key.

  **Using a pre-shared key in a large office environment is not practical or effective most of the time**.

  - Enterprise authentication system offers the ability to use individual user credentials and more robust security protocols. To do this, 802.1X can be used for enterprise-grade authentication method.

- **Wired Equivalent Privacy (WEP)** was the original wireless security standard the very first version of Wi-Fi networks. It is **not secure** because WEP relies on a pre-shared key and a weak encryption mechanism know as Rivest Cipher 4 (RC4). Additionally it has the **initialization vector** vulnerability. Using `Aircrack-ng`, **attackers can crack a WEP network pre-shared key**.

- **Wi-Fi Protected Access** (WPA) was designed as a replacement for WEP and uses the **Temporal Key Integrity Protocol (TKIP)**. TKIP is **still has vulnerabilities by today's standard because WPA uses Rivest Cipher 4 (RC4)** for encryption with Message Integrity Check (MIC). MIC relies on hashing the data before it's sent over the network.

- **Wi-Fi Protected Access 2 (WPA2)** is still heavily used today. It was created as part of the IEEE 802.11i standard and was first implemented with wireless g and then used again with wireless n, wireless a, and wireless ac networks. Instead of using Message Integrity Check, WPA2 relies on Countermode with Cipher Blockchaining Message Authentication Code Protocol(CCMP). Instead of using RC4, it uses the **Advanced Encryption Standard (AES)**. **AES provides more data security and confidentiality**. Therefore, WPA2-CCMP is the most secure and provides the high level of confidentiality

**In personal Mode, WPA2/WPA uses the pre-shared key**

In enterprise Mode, WPA2 uses the centralized authentication. For example, RADIUS authentication server is used with individual usernames and passwords for each client.

- **Wi-Fi Protected Access (WPA3)** uses the **Simultaneous Authentication of Equals (SAE)**. SAE is a security protocol that was designed to enhance the handshake process used in Wi-Fi authentication. It does not use the pre-shared key model. Instead **SAE established a secure initial key exchange between the client and the access point**.

- **Wi-Fi Protected Setup (WPS)** is not an encryption or integrity protocol. Instead it is a network security standard aimed at **simplifying the setup of a secure Wi-Fi connection**. WPS allows users to connect to a network using a **PIN that can can hard coded into the user devices**. WPS was designed to make it easier for non-technical users to set up secure networks. WPS is vulnerable to brute-force attacks and really easy to crack.

In these days, WEP, WPA and WPS are not used due to insecurity.

- Open networks are networks with no security, no protection, and no password.

- WEP is associated with the term Initialization Vector(IV).

- WPA is associated with the terms TKIP and RC4.

- WPA2 is associated with the terms CCMP and AES. WPA2-CCMP is the most secure and provides the required level of confidentiality

- WPA3 is associated with the term SAE.

- Pre-shared key is associated with a password used in a personal mode of a wireless network.

- Enterprise mode is associated with using an individual username and password for each user.

## Best Practices for Wireless Security

- Enable MAC filtering.

- Enable Wireless isolation to keep those channels and frequencies isolated from each other.

- Disable SSID broadcast to make it harder for someone to find the the wireless network.

- Use WPA2 with a good, long, strong pre-shared key.

- Disable WPS setting because it is vulnerable to brute-force.

Lightweight Access Point Protocol (LWAPP) is the name of a protocol that can control multiple Wi-Fi wireless access points at once. 

## Captive Portals

Captive portals are the webpages displayed to users upon connecting to a network, providing access controls and enhancing user experience. It is common in public and guest networks for legal compliance and marketing.
