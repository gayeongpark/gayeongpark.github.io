---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - orchestration and automation
tags: [network, compTia, fundamentals, orchestration, automation]
comments: true
author: Lantana Park
---

# Orchestration and Automation

Orchestration is the process of arranging or coordinating the installation and configuration of multiple systems. The primary purpose of orchestration in network is to automate network device configurations.

## Infrastructure as Code (IaC)

Infrastructure as Code enables managing and provisioning of infrastructure through code instead of through manual processes.

Infrastructure as Code is the basis of everything in horizontal scaling or scaling out within cloud environments.

### Areas for implementation of automation

1. Scripting let the user perform a series of actions in a particular order or sequence

2. Security Templates and Policies contain a series of configuration files that are applied to the different devices being deployed in the environment

- Snowflake System is any system that is different from the standard configuration template used within the organization's IaC architecture. The lack of consistency in a special snowflake system will result in numerous issues.

## When to Automate and Orchestrate

Automation and orchestration are vital in modern IT and cybersecurity environments

Because, it streamlines complex processes, enhances security measures and improves operational efficiency.

### Consideration things before implementing automation and orchestration

- Complexity : The initial step involves assessing the complexity and resource commitment needed for the process

- Cost : Requires a large upfront initial investment to hire a service provider or a team of developers for implementation

- Single points of failure : Identify during automation or orchestration implementation in the network and ensure that the automations and orchestrations are appropriately designed to be maintained

- Technical debt : Can accumulate if not regularly maintained or updated. It is the cost and complexity of poorly implemented software needing future adjustments

- Ongoing supportability : Long-term supportability is crucial for adapting automation to evolving technology

Automation and orchestration excel in handling repeatable and stable tasks. And it is required to conduct continuous monitoring and adaptation of the automation and orchestration systems

## Benefits of Automation and Orchestration

1. Increasing efficiency and time savings : Automating tasks frees up employee time

2. Enforcing baselines : Streamlined security and compliance through automation

3. Implementing standard infrastructure configurations : Standardized configurations for security and stability

4. Scaling in a secure manner : Dynamic resource scaling with security compliance

5. Increasing employee retention : Automating tasks unlocks job fulfillment

6. Increasing reaction times : Respond more quickly to security incidents and anomalies through automation

7. Being a workforce multiplier : Amplifying staff capabilities with automation

## Playbooks

The playbook is a checklist of actions to be performed to detect and respond to a specific type of incident.

- Playbooks in networking are used to define a set of tasks or actions to be executed in an automated manner, typically using tools like Ansible, providing a structured approach to automate network configurations. 
- Templates are predefined configurations or patterns that can be reused to automate the deployment of network devices or services. While both playbooks and templates are used for automation, they serve different purposes. 

Great Resource for playbook

- playbook gallery

- Microsoft Incident Response playbook

Security center often implements SOAR (Security Orchestration, Automation, and Response). It facilitates incident response, threat hunting, and security configurations without any human assistance.

Runbook is an automated version of a playbook which leaves clearly defined interaction points for human analysis.

## Upgrades and Compliance

Automation simplifies network upgrades like security patches and firmware updates by scheduling them during off-peak hours, minimizing downtime, and ensuring version control across all devices. Automated testing tools help verify the network’s performance after upgrades.

Automation ensures that networks adhere to compliance standards (e.g., PCIDSS) by continuously monitoring configurations and policies, automatically enforcing them, and flagging non-compliant systems. It also helps gather logs for audits and assists in policy enforcement by deploying policies across all devices.

- Automated Patch Management : Automation is essential for managing patches in large networks, ensuring systems are secure and minimizing vulnerabilities.

- Continuous Compliance Monitoring : Automation tools can provide 24/7 monitoring of network configurations, automatically correcting deviations, and offering real-time compliance reports.

## Automating Network Inventories / Dynamic inventories

Automating network inventories is crucial in modern networks, especially with the increasing use of virtual machines and cloud services. Traditional manual inventory methods are ineffective for virtual environments, which require real-time tracking of dynamic assets such as devices, software, and licenses. Automating this process ensures more accurate and up-to-date information, supporting both logistical and strategic needs.

### Key Benefits of Automated Inventories

1. Real-Time Updates : Devices are automatically tracked as they connect or disconnect from the network, providing immediate visibility into network assets and reducing risk.

2. Integration with Management Tools : Tools like Ansible, Chef, and Puppet can be integrated with dynamic inventories to automate device configuration and streamline network operations.

3. Reduction of Human Error : Automating the inventory process eliminates the mistakes that come with manual counts, improving accuracy and saving time.

### Methods for Network Inventory Automation

- Nmap : A tool that conducts IP and port scans to identify devices and services on the network, enabling network administrators to detect vulnerabilities, such as open ports.

- Visualization Tools : Tools like Zenmap, SolarWinds Network Topology Mapper, and Intermapper help visualize network layouts and identify single points of failure.

Automated inventories also support compliance with standards like PCI DSS by ensuring that unauthorized devices don’t connect to sensitive subnets, providing real-time alerts and protecting critical assets.

## Integration and APIs

Integration is the process of combining different subsystems or components into one comprehensive system to ensure proper functioning together.

API (Application Programming Interface) is a set of rules and protocols that are used for building and integrating application software. And APIs allow for integration between different services.

Integrations and APIs are used to create interconnections between different services.

### Types of APIs

- REST API (Representational State Transfer) is an architectural style that uses standard HTTP methods and status codes, uniform resource identifiers, and MIME types. REST is more straightforward and adaptable to utilize.

- SOAP (Simple Object Access Protocol) is the protocol that defines a strict standard with a set structure for the message, usually in XML format. SOAP provides higher level of security and transactional integrity.

