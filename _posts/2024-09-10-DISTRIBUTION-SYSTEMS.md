---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ | Distribution Systems
tags: [network, compTia, fundamentals, systems]
comments: true
author: Lantana Park
---

# Distribution Systems

## Cable Distribution Systems

Cable Distribution System is an organized system to connect the network's backbone in MDF to the Intermediate Distribution Frames (IDF) and to end user's wall jacks.

### Components of cable distribution systems

- **Demarcation Point(DP)** is the location at which the Internet service provider's connection ends and the network infrastructure and cabling begin.

- **Main Distribution Frame(MDF)** serves as the main starting point for all interior cabling that will be distributed throughout this facility. It is like the trunk of a tree. It holds the router and backbone switch to manage external connections and centralize the internal network. 

- **Backbone switch** is where the network connects in MDF. Its main role is to gather, process, and forward data from various parts of the network, such as the edge switches located in each IDF (Intermediate Distribution Frame).

- **Intermediate Distribution Frame(IDF)** is like branches of the tree. It connects smaller sections of the network back to the MDF. These IDFs contain edge switches that connect to the backbone switch in the MDF. Each floor or area usually has its own IDF.

- **Edge switch** connects local devices and users to the backbone switch or router in the MDF.

- **Cable Tray** is the unit or assembly of units that form a rigid structural system to secure the cables and raceways used by the cables as they go across the building.

- **Racks** are designed to hold various devices like switches, routers, patch panels, and servers to facilitate efficient space management and easy access for ongoing network maintenance.

  - 2-post racks for lighter equipment.
  - 4-post racks for heavier equipment like servers.
  - Wall-mounted racks for small spaces.
  - Rack enclosures are fully enclosed with doors for security.

- **Patch Panels** organize cables so I can easily connect devices to the network. They allow I to quickly move or repair cables without messing with the expensive equipment. Patch panels have ports on the front (where cables connect) and punchdown blocks on the back (where I secure cables using a special punchdown tool). There are two types:

  - Copper patch panels (for copper cables).
  - Fiber distribution panels (for fiber optic cables).

- **Wall Jacks** is where I plug my computer or phone into the network. Behind the scenes, this jack connects to a cable that runs through the walls and ceilings to the IDF, where it’s connected to the patch panel and then to a switch.

## Power Distribution Systems

Power Distribution Systems ensure consistent and reliable power delivery for networking equipment, infrastructure, and environments.

- **Uninterruptible Power Supply** (UPS) is an electrical apparatus that provides **emergency power** to a load when the input power source fails. An UPS is great for **short-duration power outages**, depending on the amount of electrical load.

- Power Distribution Unit (PDU) is a specialized device for distributing electric power to various network components and computing equipment. PDU units are only designed to provide power protection from surges, spikes, and brownouts.

- Generators are usually installed outside of a datacenter to provide longer-term power during a power outage in a region.

- Managing power loads is critical in preventing circuit overloads and ensuring efficient power usage inside datacenters.

- Voltage refers to the electric potential difference and is a key factor in power distribution systems. However most devices these days are considered to be dual-voltage and can be configured to operate at either 120 volts or 230 volts.

## Heating, Ventilation, and Air Conditioning (HVAC) Systems

This system is a technology designed for indoor environmental comfort that provides temperature control, humidity management, and airflow regulation.

- Temperature Control is a significant consideration as computer networks and data centers house electronic equipment that generates heat. Most networking equipment has fail-safes designed to power off if it gets too hot to prevent any damage from occurring on that system.

Maintain a steady temperature of 68-77°F or 20-25°C
Maintain a relative humidity level of 40 to 60%

- Airflow Management

In order to properly manage the airflow,

**Port-Side Exhaust** means the back of the equipment (where the exhaust ports are located) should face the aisle where hot air is pushed out. The idea is to have cold air coming in from the front of the equipment, and hot air exiting from the back. This setup helps keep the equipment from overheating.

- Raised floor systems

- Ceiling plenums

## Fire Suppression Systems

- **Wet pipe systems** are **the most basic type of fire suppression system** that involves using a sprinkler system and pipes that always contain water. Avoid using a wet pipe system in an around data centers because it that pipe leaks or that little glass bulb is broken by accident, water will come rushing out and it will damage the servers and network gear that are located inside of the room underneath them.

- **Pre-action systems** help minimize the risk of accidental releases when using a wet pipe system. With a pre-action system, both a detector actuation like a smoke detector and a sprinkler must be tripped prior to water being released.

- **Special suppression systems** utilize **a clean agent** as part of its suppression system. Clean agents, such as FM-200 or Novec 1230, are ideal for data centers as they effectively suppress fires **without harming electronic equipment or leaving a residue**. These agents are safe for the environment and do not displace oxygen, which minimizes risk to personnel. Because they do **not cause environmental damage**, they are preferred over older options like Halon gas, which, although effective, depletes the ozone layer. If a special suppression system is used, data centers should have alarms and backup oxygen available to ensure safety.

## Storage network Technology

1. NAS (Network Attached Storage)

  - File-Level Storage: NAS provides file-level storage, which means data is stored and accessed as files (such as documents or media files). It’s similar to how data is stored on a shared network drive.
  - Function: NAS operates as a dedicated file server, accessible over a network, and is ideal for environments where multiple clients or users need to access shared files.
  - Example Protocols: NAS devices commonly use protocols like NFS (Network File System) or SMB (Server Message Block) for file sharing.

2. SAN (Storage Area Network)

  - Block-Level Storage: Unlike NAS, SAN typically provides block-level storage, where data is divided into blocks and each block is managed separately. This method is closer to how data is managed on a physical hard drive.
  - Function: SANs are generally used in enterprise environments, providing high-speed, low-latency storage over dedicated networks, which makes them ideal for database and application data where quick, efficient access is needed.
  - Example Protocols: Common SAN protocols include iSCSI, Fibre Channel (FC), and Fibre Channel over Ethernet (FCoE).