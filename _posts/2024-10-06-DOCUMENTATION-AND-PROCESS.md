---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - Documentation and process | disaster recovery
tags: [network, compTia, fundamentals, documentation]
comments: true
author: Lantana Park
---

# Documentation and Process

- Policies define the organization’s security goals and are divided into:

  - Organizational: Provide overall direction and goals.

  - System-specific: Address security for specific technologies.

  - Issue-specific: Tackle specific security concerns (e.g., email privacy).

- Standards are mandatory rules to implement policies.

- Baselines are reference points for system configurations.

- Guidelines are recommended, flexible actions.

- Procedures are step-by-step instructions for implementing policies.

## Common Documentation

Physical Network Diagram shows the actual physical arrangement of the components that make up the network.

Logical Network Diagram illustrates the flow of data across a network and shows how devices communicate with each other.

Wiring Diagram labels which cables are connected to which ports.

Radio Frequency (Wireless) Site Survey is the process of planning and designing a wireless network to deliver the required wireless solution.

Audit and Assessment Reports are delivered after a formal assessment has been conducted. It should contain executive summary, environment and system diagram, scope and objectives, security requirements, assumptions and limitations, findings and recommendations, methods and tool, and audit result.

Baseline Configurations are the most stable versions of a device's configurations. It is the set of specifications for an information system, or a configuration item within a system, that has been formally reviewed and agreed on. Changes will be properly tested and approved to be part of the new baseline.

## Asset Inventory

Asset management refers to the systematic approach of governing and maximizing the value of both tangible and intangible assets throughout their entire lifecycle. This includes tangible assets like computers, servers, and equipment, and intangible assets such as intellectual property and human resources. The primary goal is to develop, operate, maintain, upgrade, and eventually dispose of assets in a cost-effective manner while managing associated risks and performance attributes.

A database system allows for the detailed management and configuration of assets.

### Key components of asset management

1. Inventory Lists and Database Systems : Organizations need to maintain a complete inventory of all assets, which can range from workstations and servers to smaller devices like printers, tablets, and IoT devices. For larger organizations, manual inventory management becomes difficult, so database systems are used to store information like asset type, serial numbers, location, and assigned users. These systems often integrate with configuration management and trouble-ticket systems to automate tracking.

2. Asset Tags and IDs : Each asset must be uniquely identified using asset tags, which can be barcodes or RFID tags. These allow for easy tracking and inventory management, especially during annual inventories.

3. Procurement Lifecycle : The procurement lifecycle includes several stages:

   - Change approval: Requesting and approving asset purchases.
   - Procurement: Budgeting and purchasing from trusted vendors.
   - Deployment: Installing the asset securely.
   - Maintenance/Operation: Monitoring and supporting the asset.
   - Disposal: Sanitizing data and responsibly recycling, selling, or destroying assets at the end of their lifecycle.

4. Warranty and Licensing : Keeping track of asset warranties and software licenses is essential. Each asset's warranty and licensing status should be logged in the asset management database to ensure compliance and proper asset usage.

5. Assigned Users : Asset management also involves assigning assets to specific users. The system should track which user is responsible for each device, making it easier to manage support issues and maintain accurate records.

## IP Address Management

IP Address Management (IPAM) is a methodology and suite of tools used to plan, track, and manage the IP address space in a network infrastructure.

IPAM creates a systematic and error-resistant method of managing IP addresses in network enterprises. These automated systems detect and resolve IP conflicts and ensure two devices are noy assigned to the same IP address.

## Common Agreements

Non-Disclosure Agreement (NDA) defines what data is confidential and cannot be shared outside of a relationship. NDA is an administrative control.

Memorandum of Understanding (MOU) is the non-binding agreement between two or more organizations to detail what common actions they intend to take.

Service-Level Agreement (SLA) documents the quality, availability, and responsibilities agreed upon by a service provider and a client.

## Product Lifecycle

When it comes to Microsoft Windows, there are two types of supports

- Mainstream support : Minimum of five years

- Extended support : Extends up to three to five years

End of life means that product is no longer supported by mainstream or extended support. It can be called Legacy Operating System. That means that product is no longer supported.

Every product, including operating systems, has a defined life cycle. Once that operating system reaches end of life, there will be no more security patches.

## Change Management

Change Management is the orchestrated strategy to transition from an existing state to a more desired future state. Disruption of existing processes by any kind of change will affect its efficiency and effectiveness. However change management ensures seamless integration of changes into existing architecture and processes.

Change Advisory Board (CAB) is a body of representative from various parts of an organization that is responsible for evaluation of any proposed changes.

## Configuration Management

Configuration Management focuses on maintaining up-to-date documentation of a network's configuration.

- Asset Management : Formalized system of tracking network components and managing their lifecycle.

- Create a baseline : Collection of data under normal operating conditions.

- Cable management : Process of documenting the network's existing cable infrastructure.

- Network documentation : Document the network appropriately.

## Patch Management

Patch Management involves planning, testing, implementing, and auditing of software patches. It is to ensure that patches do not create new problems once installed.

- Planning : Tracks available patches and updates and determines how to test and deploy each patch

- Testing : Tests any patch received from a manufacture prior to automating its deployment through the network. It is needed to have a small test network, lab, or machine for testing new patches before deployment

- Implementing : Deploys the patch to all of the workstations and servers that require it

- Auditing : Scans the network and determines if the patch was installed properly and if there are any unexpected failures that may have occurred

# Disaster Recovery

Disaster Recovery enables software, data, or hardware recovery to resume performance of critical business functions after a disaster.

## High Availability Approaches

Network Redundancy is to ensure uninterrupted operations by using multiple connections between devices (servers, switches, routers) and the internet. For instance, servers can have multiple network interface cards (NICs) configured in pairs or groups for load balancing and failover.

- Active-Active Approach : Multiple systems operate simultaneously, sharing the load. If one fails, others continue to function without interruption, maximizing resource utilization.

- Active-Passive Approach : A standby system remains idle until the primary system fails, providing a reliable fallback but not utilizing resources as efficiently as the active-active approach.

- Load balancers : Distribute traffic across multiple servers to prevent any single server from being overloaded. They also monitor server health and reroute traffic when needed.

- Content Delivery Networks : Geographically distributed servers that store cached content closer to end users, reducing latency and improving reliability.

## Designing Redundant Networks

When designing redundant networks, several key considerations need to be made.

1. Types of Redundancy

   - Hardware Redundancy: Multiple power supplies, network interface devices, hard drives, routers, or switches. Knowing when to use redundant hardware is crucial for ensuring network uptime and reliability.

   - Software Redundancy: Virtual switches, virtual routers, and software-based solutions like RAID provide redundancy without requiring additional hardware, reducing costs.

2. Cost-Benefit Analysis

   Understanding how to balance cost, availability, and redundancy is a key part of network design. You must consider how adding redundancy, whether via hardware or software, affects the overall network budget.

3. Environmental Redundancy

   Power, space, and cooling (like air conditioners and UPS systems) are critical for network reliability. For larger server farms, these elements need to be redundant, but for smaller environments, simpler solutions might suffice.

4. Protocols and Performance

   Choosing the right protocol (TCP vs. UDP) based on redundancy needs, as TCP offers packet retransmission while UDP does not.
   Implementing Quality of Service (QoS) profiles to prioritize business-critical applications (e.g., web, email, streaming).

5. Performance Standards and Metrics

   Uptime goals (e.g., 99%, 99.999% availability) help determine the level of redundancy required. Defining and measuring network performance through key metrics ensures the network meets business requirements.

6. Design Trade-offs

   The balance between time, cost, and quality in network design. You need to understand how focusing on one area (e.g., speed) may sacrifice another (e.g., cost).

7. High Availability Best Practices

   Importance of planning redundancy early in the network design phase to avoid higher costs when retrofitting.

## Disaster Recovery Metrics

Disaster Recovery Metrics are the quantifiable standards used to plan and evaluate an organization's ability to recover IT operations following a disruptive event.

### How can I maintain that high level of availability?

- Availability : Being up and operational. is measured by uptime, expressed as a percentage of operational time. Aim for 99.999% uptime (five nines), allowing only five minutes of downtime per year, or 99.9999% uptime (six nines), which translates to 31 seconds of downtime per year.

- Reliability : ensures that the network consistently delivers data without packet loss. Both availability and reliability need to be balanced for effective operations.

### Key metrics

- Mean Time to Repair (MTTR) : Measures the average time it takes to repair a device or service after a failure. A lower MTTR indicates better availability.

- Mean Time Between Failures (MTBF) : Measures the average time between failures. A higher MTBF means greater reliability.

- Maximum Tolerable Downtime (MTD) : The longest time a business or system can be down without causing significant damage to operations. This varies across different organizations and functions.

- Recovery Time Objective (RTO) : The target time to restore normal operations after a disruption. For instance, using backup generators or battery systems can achieve short RTOs, even zero for power recovery.

- Recovery Point Objective (RPO) : The longest period of time that an organization can tolerate lost data being unrecoverable.

## Redundant Site Considerations

Redundant Site is alternative sites for backup in case the primary location encounters a failure or interruption.

- Hot Sites : Continuously operational backup locations, enabling immediate failover with minimal downtime. These sites replicate all essential systems, but are costly due to the need for duplicate resources.

- Warm Sites : Have some infrastructure (e.g., power, desks, network) in place but lack fully operational systems. They can be up and running in a few days, offering a balance between cost and response time.

- Cold Sites : Essentially empty spaces with minimal infrastructure, requiring extensive setup time (1-2 months). They are the cheapest option but offer the longest recovery time.

- Mobile Sites : Portable solutions like tents or trailers, which can be configured as hot, warm, or cold sites. These are useful for remote deployments or disaster zones and provide flexibility in recovery efforts.

- Virtual Sites : Cloud-based setups that can be configured as hot, warm, or cold sites. These offer scalability, cost-efficiency, and flexibility by utilizing cloud resources from providers like AWS, Azure, or Google Cloud.

It is also important to consider to use geographic dispersion because it helps spread out the resources across different locations.

## Training and Exercises

- Tabletop exercises : These exercises involve discussions about simulated emergency scenarios. They're easy to set up but are largely theoretical, lacking practical evidence of how long tasks might take in real situations. A common issue with tabletop exercises is that they can lead to unrealistic expectations for recovery times in actual events.

- Penetration testing : This involves using active tools to simulate attacks, verify vulnerabilities, and test security controls. Penetration tests help identify vulnerabilities and social engineering risks. It's essential to clearly define the scope and resources for these tests. External teams or separate internal red teams are recommended for objective assessments, as system administrators may have biases that impact the results.

- Red/Blue/White exercises

  - Red Team: The attacking team, often third-party, tasked with finding vulnerabilities.

  - Blue Team: The defensive team, composed of system administrators and cybersecurity professionals, tasked with defending systems.

  - White Team: The referees and supervisors who evaluate and manage the exercise, ensuring objectivity and reporting on both teams' performance. They may also set up simulated environments for testing without risking the live network.
