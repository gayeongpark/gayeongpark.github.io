---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - wireless networks
tags: [network, compTia, fundamentals, wireless]
comments: true
author: Lantana Park
---

# Wireless network

## Wireless network types

- **Ad Hoc** / **Independent Basic Service Set** (IBSS) are networks where devices connect directly to each other rather than through a central access point. Ad Hoc network does not typically provide Internet access. Ad Hoc or peer-to-peer configuration allows sharing and collaboration, as long as the devices are within range.

When might I want to use ad hoc wireless network?

If I need to deploy two devices to share files wirelessly between them, ad hoc will be a great way to do it. Because I do not have to set up and configure an entire wireless network for that purpose.

- **Infrastructure Wireless Networks** are a more organized setup in which devices like laptops and smartphones are going to be connected to a network through a wireless access point that will then bridge my wireless clients onto the wired local area network.

Each wireless access point is going to have a unique identifier known as a Basic Service Set Identifier (BSSID), which is set to the MAC address of the wireless access point.

**Service Set Identifier (SSID)** is a common alphanumeric network name that end users can search for to connect to the wireless network.

**Extended Service Set (ESS)** creates a **larger network** that shares the name SSID to allow for seamless connectivity across a building.

- **Point-to-point Wireless Networks** are designed to connect two distinct locations over long distances using high-gain antennas. It is highly efficient and offer dedicated bandwidth between two points.

- **Wireless Mesh Mesh Networks** are versatile and resilient form of wireless networking. It has self-healing capability and can reconfigure themselves around broken or blocked pathways. Mesh networks are also great for large scale deployments when I cannot lay cables.

Different types of mesh networks

1. It uses ESS configuration in a wireless network that operates in infrastructure mode.

2. It involves multiple different types of wireless networks all operating together to provide services to end users.

Inherent redundancy in a mesh network ensures that data can be rerouted through alternate paths maintaining vital communications.

- **Autonomous Access Point** is a standalone device that contains all of the intelligence to handle wireless networking functions independently.

- **Lightweight Access Point** is multiple access points connecting back to a centralized controller.

## Wireless Antennas

Wireless antennas are simply devices that are designed to send and receive radio frequency signals.

- **Omnidirectional antennas** are designed to transmit and receive wireless signals **in all directions equally**. It is great for covering a broad area with a relatively uniform signal strength.

Mobile hot spot, wireless public networks.

- **Unidirectional Antennas** focuses on a single direction to provide a more concentrated signal beam. Unidirectional antennas are suitable for **long and narrow coverage areas or a strong signal in one particular direction**.

- **Yagi antenna** is a specific type of directional/unidirectional antenna that can provide high signal gains and uses a narrow beam-width. A yagi antenna is best when capturing or sending signals over **long distances to or form a specific, fixed location**.

## Understanding Antennas

1. Omnidirectional Antenna

   - Found in most wireless access points and mobile devices.
   - Radiates signals equally in all directions (360 degrees).
   - Ideal for environments where devices move around (e.g., smartphones connecting to Wi-Fi or cellular networks).

2. Unidirectional Antennas:

   - Focuses signals in one direction for longer distances.
   - Used in specific scenarios, like wireless penetration testing, to target a single direction for more power.

3. Parabolic Antennas:

   - A type of unidirectional antenna with a curved dish design, used for focused signal transmission (e.g., satellite TV).
   - Maximizes signal strength by directing the transmission in one direction.

4. Yagi Antennas:

   - Another form of unidirectional antenna, typically used for long-range wireless communication between buildings.
   - Common in business parks or campus settings to connect multiple buildings.

## Wireless Frequencies

Wireless frequencies are the different frequency bands that are used to transmit and receive the radio waves used by the wireless networks to send data.

- **2.4 GHz**(2.400 GHz to 2.495 GHz) - One of the most widely used frequencies for wireless networking and is known for its long-range and better penetration through solid objects. It has the slowest data transfer speeds due to having smaller channel widths and fewer nonoverlapping channels. Which can lead to interference and retransmission of the data.

- **5 GHz**(5.725 GHz to 5.875 GHz) - There are 24 non-overlapping channels of 20 MHz per channel when working in a 5 GHz-based 802.11 wireless network. It has less interference and higher levels of performance. It has a shorter range then the 2.4 GHz band. (Video streaming and gaming). It has faster data transfer speed.

  - Channel Bonding creates a wider channel by merging two or more neighboring channels into a single wider channel. Up to 8 channels together can be bonded to create a virtual channel that is 160 MHz in width. It increases the speed and is susceptible to interference.

- **6 GHz**(5.925 GHz to 7.125 GHz) -It is a relatively new spectrum opened up for Wi-Fi use that offers even more channels and bandwidth to allow for faster connections and less congestion. It does provide the shortest distances for its coverage, and offer the least amount of solid object penetration for the use cases.

## 802.11 Standards

The IEEE 802.11 standards define the technology for Wi-Fi and have evolved to meet growing demands for speed and reliability.

1. 802.11a (Wireless A):

   - Frequency: 5 GHz
   - Speed: Up to 54 Mbps
   - Range: ~35 meters
   - Higher cost made it primarily used by businesses.

2. 802.11b (Wireless B):

   - Frequency: 2.4 GHz
   - Speed: Up to 11 Mbps
   - Range: ~140 meters
   - Lower cost made it widely adopted in homes and schools. (Security cameras, Walkie talkies, baby monitors, microwaves)

3. 802.11g (Wireless G):

   - Frequency: 2.4 GHz
   - Speed: Up to 54 Mbps
   - Range: ~140 meters
   - Combined Wireless A’s speed with Wireless B’s affordability.

4. 802.11n (Wireless N / Wi-Fi 4):

   - Frequency: 2.4 GHz & 5 GHz
   - Speed: Up to 600 Mbps
   - Range: ~70 meters (2.4 GHz) and ~35 meters (5 GHz)
   - Introduced MIMO (multiple-input, multiple-output) for faster data transfer.

5. 802.11ac (Wireless AC / Wi-Fi 5):

   - Frequency: 5 GHz
   - Speed: Up to 6.9 Gbps
   - Range: ~35 meters
   - Introduced MU-MIMO (multi-user MIMO) for simultaneous connections by multiple users. High speed and reliability.

6. 802.11ax (Wireless AX / Wi-Fi 6):

   - Frequency: 2.4 GHz, 5 GHz, and optionally 6 GHz (Wi-Fi 6E)
   - Speed: Up to 9.6 Gbps
   - Range: Varies by band
   - Supports all previous wireless standards and enhances performance with MU-MIMO and OFDMA (Orthogonal Frequency Division Multiple Access).

- Wireless B, G, N, and AX support 2.4 GHz.
- Wireless A, N, AC, and AX support 5 GHz.
- Wi-Fi 6E (AX) supports 6 GHz.
- Higher speeds often come with reduced coverage distances for a single access point.

## Wireless Security

## Understanding Wireless Security

## When Wireless Security Fails

## Captive Portals
