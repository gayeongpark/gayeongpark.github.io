---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - Wide Area Networks (WANs)
tags: [network, compTia, fundamentals, wan]
comments: true
author: Lantana Park
---

# Wide Area Networks

## Fiber Optic Connections

Fiber optic connections provide high-speed internet using light transmitted through thin fibers of glass or plastic. Here's a breakdown of common fiber deployment methods:

FTTH - Fiber to the Home | Fiber optic cables are brought directly to individual homes. This provides the fastest speeds, as the fiber connection goes directly into the residence without any copper cable involvement.

FTTC - Fiber to the Curb/Cabinet | Fiber is extended to a curbside or cabinet near the home, and from there, traditional copper cables are used to connect individual homes or businesses. This setup offers high speeds, but the use of copper can slightly reduce performance compared to FTTH.

FTTN - Fiber to the Node/Neighborhood | Fiber optic cables are run to a node or central point within a neighborhood. From the node, copper cables (like DSL) are used to connect individual homes. Due to the longer distances copper cables must cover, this method is slower compared to FTTH and FTTC.

FTTB - Fiber to the Building/Basement | Fiber optic cables are brought to the communication room or basement of a multi-unit building. From there, copper cables distribute the connection to individual units within the building, making this setup slower than FTTH, but it may still offer decent speeds depending on the copper wiring.

## Cable (DOCSIS) Connections

DOCSIS (Data Over Cable Service Interface Specification) is a standard that allows high-speed internet delivery using the same lines as cable TV. It defines how data is transmitted over a Hybrid Fiber-Coaxial (HFC) network.

HFC (Hybrid Fiber-Coaxial)is a network infrastructure combining fiber optic cables for long-distance data transmission and coaxial cables for the final delivery to homes or offices. Fiber provides high-speed connections to a distribution point, where coaxial cables take over.

DOCSIS designates frequency ranges for data transmission.

- Upstream (upload) uses 5-42 MHz.
- Downstream (download) uses 50-860 MHz, offering far greater bandwidth, which leads to faster downloads compared to uploads.

Cable connections offer higher download speeds (e.g., 1 Gbps) and much slower upload speeds (e.g., 30-40 Mbps) due to the bandwidth differences between downstream and upstream channels.

DOCSIS leverages existing cable TV infrastructure, making it more cost-effective and quicker to deploy than fiber-optic alternatives.

## Digital Subscriber Line (DSL) Connections

DSL (Digital Subscriber Line) is a technology that provides internet access by transmitting digital data over local telephone networks. It was popular in the late 1990s and early 2000s for its affordability.

### Types of DSL

- ADSL (Asymmetric DSL): Provides higher download speeds (up to 8 Mbps) than upload speeds (around 1.5 Mbps), making it ideal for users who download more than they upload. This type of DSL was widely used in homes.

- SDSL (Symmetric DSL): Offers equal upload and download speeds, but at lower overall speeds. This was often used for businesses needing consistent bandwidth for both directions.

- VDSL (Very High Bitrate DSL): Offers much faster speeds, with downloads reaching 50 Mbps and uploads around 10 Mbps. However, it only works well if the user is within 4,000 feet of the telephone company's distribution point (DSLAM).

DSL performance decreases with distance. VDSL requires proximity to the DSLAM, while ADSL can work up to 18,000 feet away, but with reduced speeds.

As cable modems and fiber-optic connections became more prevalent, DSL, particularly ADSL and VDSL, became less common. Today, it's mainly found in rural or older areas where fiber or cable hasn't been deployed.

## Satellite Connections

Satellite Internet connects users to the internet via communication satellites in space. It's primarily used in remote areas where cable, cellular, or fiber isn't available, but can be accessed almost anywhere with a clear line of sight to the satellite.

Remote home users, using services like Hughesnet or Starlink.
Mobile users, such as those in RVs, trucks, or aboard airplanes and cruise ships.

- Higher costs compared to cable or fiber connections.
- Satellites tend to be used in remote or mobile environments such as planes, trains, cars, and ships.
- Latency issues due to the distance satellites are from Earth. So something that uses the low earth orbit will give much lower latency and hight speeds

## Cellular Connections

Cellular technology provides internet access through smartphones, tablets, modems, hotspots, and fixed services. The evolution of cellular generations (G) improves speed and capabilities, with 2G starting digital services, 3G enhancing speed, and 4G bringing high-speed connections. The latest, 5G, offers three frequency bands:

- Low Band: Long range but slower speeds (30-250 Mbps).
- Mid Band: Good balance of range and speed (100-900 Mbps).
- High Band: Short range but extremely fast speeds (up to 10 Gbps).

Global System for Mobile Communications (GSM) is a cellular technology that takes the voice during a call and then converts it to digital data.

Code-Division Multiple Access (CDMA) is a cellular technology that uses code division to split up the channel

GSM and CDMA are the two underlying technologies. GSM, used by most of the world, relies on SIM cards, making it preferable for international travelers. CDMA is more common in places like the US, Japan, and South Korea. Modern phones now often support E-SIMs, allowing users to switch carriers digitally.

## Microwave Connections

A microwave link is a communication system that uses a beam of radio waves in the microwave frequency range to transmit information between two fixed locations.

Microwaves can provide a very fast connection point using point-to-point connections between two places.

## Leased Line Connections

A leased line is a dedicated, always-on connection between two locations, usually provided by a telecom provider over fiber or copper. It's often used for WAN connectivity between offices or data centers.

Leased lines provide fixed, symmetric bandwidth (equal upload and download speeds), unlike standard broadband which shares bandwidth with other users. This makes leased lines highly reliable.

Leased lines are ideal for businesses needing high performance, security, and reliability, such as for video conferencing, large file uploads, or secure data transfer.

Because leased lines provide a direct connection, they offer higher security with reduced exposure to public internet traffic. They are also highly reliable, often guaranteed by service level agreements (SLAs) ensuring minimal downtime.

Leased lines are more expensive than shared services (DSL, cable) and are typically used by larger businesses that prioritize reliability and speed.

## MPLS Connections

MPLS is a technique used by service providers to improve the efficiency, speed, and flexibility of networks. It is not a networking protocol but an approach to streamline data traffic flow by using label switching instead of traditional IP routing.

Instead of relying on complex IP routing tables, MPLS uses short, fixed-length labels to make forwarding decisions. Routers (called label switch routers) use these labels to quickly forward packets across the network, speeding up the process.

### MPLS Process

1. Label Assignment: When a packet enters the MPLS network, an ingress router assigns a label.
2. Label Switching: Core routers forward the packet based on the label, avoiding complex routing lookups.
3. Label Removal: The egress router removes the label, and the packet is forwarded based on its original IP header.

## WAN Connections

- Cable Modem: One of the most common WAN technologies. It provides internet connectivity through coaxial cable. The modem connects to a router, distributing the connection throughout a local area network (LAN).

- Fiber Optic Modem: Used in fiber optic networks, such as Verizon Fios. A fiber optic connection is converted to copper (e.g., Cat6) using a media converter, which then connects to the building's networking equipment (router, switch).

- Satellite Modem: Typically used in remote areas without access to cable, fiber, or DSL. It uses coaxial cable to connect to a satellite dish, sending signals to and from satellites in space. The modem outputs a Cat6 connection for local devices.

- Cellular Modem: Mobile phones and dedicated devices can use cellular networks to connect to the internet. These can also function as hotspots, creating a local wireless network using the cellular WAN connection.