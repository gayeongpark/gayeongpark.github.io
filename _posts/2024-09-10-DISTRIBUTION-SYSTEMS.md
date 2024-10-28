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

Cable Distribution System is an organized system to connect the network's backbone in MDF to the Intermediate Distribution Frames(IDF) and to end user's wall jacks.

### Components of cable distribution systems

- **Demarcation Point** is the location at which the Internet service provider's connection ends and the network infrastructure and cabling begin.

- **Main Distribution Frame** serves as the main starting point for all interior cabling that will be distributed throughout this facility. It is like the trunk of a tree.

- **Intermediate Distribution Frame** is like branches of the tree. It connects smaller sections of the network back to the MDF. These IDFs contain edge switches that connect to the backbone switch in the MDF. Each floor or area usually has its own IDF.

- **Backbone switch** is where the network connects in MDF.

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

- **Special suppression systems** utilize **a clean agent** as part of its suppression system. There is a danger with using a special suppression system because it uses either a halocarbon agent or inert gas. When releases, the agents will displace the oxygen in the room with the inert gas and suffocates the fire.

So the data center with special suppression system must be equipped with an alarm and has supplemental oxygen available.


