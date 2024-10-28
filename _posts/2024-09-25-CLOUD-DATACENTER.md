---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ | Cloud and the datacenter
tags: [network, compTia, fundamentals, cloud, datacenter]
comments: true
author: Lantana Park
---

# Cloud and the Datacenter

## Cloud Computing

Cloud computing benefits or characteristics

1. High Availability - Services experience very little downtime when using the cloud. The cloud should only have 5 minutes and 15 seconds of downtime in a year.

2. Scalability - Ability to increase the number of items in a system at a linear rate or less than a linear rate.

   - Vertical Scaling (Scaling up) - Increasing the power of the existing resources in the working environment

   - Horizontal Scaling (Scaling out) - Adding additional resources to help handle the extra load being experienced

3. Elasticity - Ability to quickly scale up or down and handle changes to demand in real time

4. Metered utilization - Being charged for a service on a pay-per-use basis. The cloud service is done on a metered basis

   - Metered Services - Paying for a certain amount of quantity upfront

   - Measured Services - Paying for the exact amount used

5. Shared resources - Ability to minimize the costs by putting VMs on other servers. Dividing an expensive server into virtual machines for shared use is more efficient

6. File synchronization - Ability to store data which can then spread to other places depending on configuration

## Cloud Service Models

On-premise solutions offer strong security but come with high costs. Once it is decided to use the on-premise solution, it is needed to procure all the hardware, software, and personnel necessary to run the organization's cloud.

Many organization instead decide to use a hosted solution. With the hosted solution, a third-party service provider (Amazon, Microsoft, Google) that provides all the hardware and facilities needed to maintain a cloud solution.

### Concerns of using the service hosting provider

1. It is important to understand their authentication and authorization mechanisms.

2. I should require redundancy and fault tolerance measures.

3. I should know storage location and location-based laws.

### Cloud service models

1. **Software as a Service (SaaS)** : The service provider is going to give the client organization a complete solution, including Application, Data, Runtime, Middleware, O/S, Virtualization, Servers, Storage, and Networking. (Turbo Tax, QuickBooks Online, Office 365). It provides remote access to software applications based on a subscription fee. SaaS is much closer to the end user than either PaaS or IaaS.

   - **Multitenancy** is a software architecture in which a single instance of an application serves multiple customers (tenants), with each tenant's data and environment isolated from others. It allows multiple users or organizations to share the same application while maintaining privacy and security. This is commonly used in cloud services and SaaS (Software as a Service) platforms. Each tenant may have customized settings, but they all use the same infrastructure and application instance.

2. **Platform as a Service (PaaS)** : Offers hardware, operating systems, and middleware, while organizations manage their custom applications. **PaaS is ideal for developing web applications**. with PaaS, the operating system and infrastructure software are included as part of the service.

3. **Infrastructure as a Service (IaaS)** : Provides virtualized hardware like servers, storage, and networking, allowing organizations to configure operating systems and software themselves. IaaS is focused on the hardware only.

#### Reliability of Cloud Service

`SaaS` > `PaaS` > `IaaS`

## Cloud Deployment Models

Cloud Architectures

- Public Cloud : Offered by providers like Google, Microsoft, and Amazon, public clouds are cost-effective and efficient, but they involve security risks since resources are shared over the internet.

- Private Cloud : Managed internally, private clouds offer higher security and control, but come at a higher cost. An example is the U.S. government’s GovCloud.

- Hybrid Cloud : Combines public and private cloud resources, allowing sensitive data to stay on private clouds while utilizing public resources for less critical operations.

- Community Cloud : Shares resources among organizations with similar needs, reducing costs, but introducing security risks from interconnected networks.

- Multi-Tenancy Cloud : Multiple organizations share the same physical resources, improving efficiency but raising concerns about potential security breaches or collateral damage during attacks.

- Single-Tenancy Cloud : A single organization uses dedicated resources, providing greater security but at a higher cost and lower efficiency.

## Cloud Connectivity

When connecting enterprise networks to cloud service providers (CSPs), two main connectivity options are commonly used: **Virtual Private Networks (VPNs)** and **Private-Direct Connections (PDCs)**.

### VPN (Virtual Private Network)

- Establishes a secure, encrypted connection between an on-premise network, remote offices, or client devices and the cloud provider’s network.
- Typically uses an **IPSec VPN** to create an encrypted tunnel over the public internet.
- Extends the network securely without requiring a direct connection.
- Works well for most organizations but may have limitations in speed and redundancy.
- Example: AWS-managed VPN supports speeds up to 4 Gbps.
- Cost: Relatively cheaper (e.g., 9 cents per gigabyte of data transfer).

### Private-Direct Connection

- **Provides a dedicated, secure connection between an on-premise network and a cloud provider's network**.
- Bypasses the internet, using a dedicated leased line or WAN connection.
- Supports faster speeds and greater redundancy compared to VPNs.
- Example: AWS Direct Connect supports speeds up to 40 Gbps and allows multiple connections to different virtual private clouds (VPCs).
- Cost: More expensive (e.g., 20-30 cents per gigabyte of data transfer) but offers better performance and reliability.

VPNs are more affordable but have speed limitations, while Private-Direct Connections offer higher speeds and redundancy at a higher cost.

## Cloud Security

Cloud security is comprised of several different components within a virtual private cloud.

**Virtual Private Cloud (VPC) is a logically isolated network area hosted within a public cloud environment**. VPCs provide flexibility, scalability, and control compared to traditional hardware networks.

VPCs are integral to IaC (Infrastructure as Code), where the deployment of resources is automated via scripts and orchestration. IaC enhances cloud architecture management by enabling scripted network configuration and resource deployment.

### VPC (Virtual Private Cloud) Components

- **Subnets** : Logical subdivisions of a VPC. Public subnets allow internet access, while private subnets restrict external access.

- Route Tables : Contain rules to direct network traffic within the VPC, associated with subnets.

- **Internet Gateways** : Allows instances within a cloud environment to send and receive unencrypted traffic to and from the Internet.

- **NAT (Network Address Translation) Gateways** : Enables instances within a VPC to access external networks. Translates private IP addresses to a public IP address. Restricts inbound connections from external networks.

- **Network Access Control/Security Lists (NSL)** : Are stateless and operate at the subnet level, requiring separate inbound and outbound rules. And used for controlling inbound and outbound traffic in cloud computing environments.

- **Network Security Groups (NSG)** : are stateful, provide more granular control, and can be applied at the instance (or specific virtual NICs) level, automatically managing connection states. And used for controlling inbound and outbound traffic in cloud computing environments.

- **VPC (Virtual Private Cloud) Peering** : Allows direct network connections between two VPCs without using the public internet.

- **VPC Endpoints** : Enable private connections to cloud services within the same cloud provider’s network, improving security and performance.

- **VPN Connections** : Establish a secure, encrypted Internet connection between an on-premises network and cloud resources.

### Advantages

- Flexibility & Scalability : VPCs offer flexible network configurations and allows mixing products from different vendors.
- Automation : VPCs integrate with IAC for automated and high speed deployments.
- Security : Multi-layered security options like ACLs and security groups enhance protection.

### Challenges

- Potential Single Point of Failure : Loss of VPC connectivity can affect the entire network.
- Security : Proper configuration and regular audits of ACLs and security groups are essential to prevent misconfigurations.

## Network Function Virtualization (NFV)

**Network Function Virtualization** is a transformative concept that is reshaping the telecommunications industry by introducing agility and flexibility to hardware-dependent networks.

It provides network flexibility and the ability to respond to the needs of cloud services and virtualization technologies

### Three main components to work

1. **NFV Infrastructure** includes the hardware and virtual resources necessary for deploying, managing, and executing VNFs.

2. **Management and Network Orchestration (MANO)** oversees the lifecycle management of the VNFs, and orchestrates the resources across the NFVI.

3. **Virtual Network Functions (VNFs)** are the software implementations of network functions that were traditionally bound to hardware appliances.

By using virtualization technology, the network functions can be installed and configured just like software applications instead of relying on dedicated pieces of hardware appliances. And this can increase our scalability while also decreasing our capital expenditures and reducing our overall cost.

## Software Defined Network (SDN)

Software-Defined Networking (SDN) is transforming network architectures, especially in cloud environments, by enabling software-based control over traditional network hardware. It allows for increased scalability, flexibility, and security through the use of software controllers and APIs, optimizing performance and resource utilization.

SDN separates network control from the hardware, using APIs to communicate with and manage hardware resources.

SDN is essential for automating network provisioning and management through scripted orchestration.

### Planes of SDN

- Control Plane: Decides how traffic is routed, prioritized, and secured. (Decides where data goes)
- Data Plane: Carries user traffic and enforces security measures. (Moves the data)
- Management Plane: Administers network devices, monitors traffic, and enforces policies. (monitoring and managing)

To set up an SDN, the organization will use an SDN application to define the policy decisions.

#### Advantages

- Vendor Flexibility: Mix-and-match devices using common APIs.
- Automation: Automates network provisioning and scaling, critical for cloud and disaster recovery.
- Security: Centralized control allows easier monitoring and detection of abnormal traffic patterns.

SDNs are critical when dealing with high-velocity or high-availability architectures in the disaster recovery space.

#### Disadvantages

- Single Point of Failure: If the SDN controller fails, network control is lost.
- Security Risk: SDN controllers become prime targets for attacks.

### Types of SDN

- Open SDN: Uses open-source technologies (e.g., OpenFlow, OpenStack).
- Hybrid SDN: Combines traditional and open SDN technologies.
- SDN Overlay: Adds abstraction layers to virtualize multiple network layers over physical devices, enhancing security.

## Software-Defined Wide Area Network (SD-WAN)

It is a virtualized approach to managing and optimizing WAN connections to efficiently route traffic between remote sites, data centers, and cloud environments.

SD-WAN allows enterprises to leverage any combination of transport services to securely connect users to applications.

To create an SD-WAN, use a centralized control function to securely and intelligently redirect the traffic across the WAN.

## Virtual Extensible Local Area Network (VXLAN)

**Virtual Extensible Local Area Network (VXLAN)** is a network virtualization technology that addresses the limitations posed by traditional network infrastructure.

**VXLAN encapsulates Layer 2 Ethernet frames within Layer 3 UDP packets**.

## SASE and SSE

SASE (Secure Access Secure Edge) and SSE (Security Service Edge) are modern network security frameworks designed to address the evolving needs of distributed, cloud-centric businesses. These blend traditional network services with comprehensive security functions.

### Secure Access Secure Edge (SASE)

- SASE combines wide area networking (WAN) and security services into a cloud-native platform, providing secure, reliable access to applications and services across various locations (branch offices, remote workers, cloud environments).

- It leverages SDN (Software Defined Networking) to offer networking and security services from the cloud rather than traditional hardware, improving flexibility, scalability, and cost-efficiency.

#### Core components include

  - Firewalls
  - VPNs
  - Zero Trust Network Access (ZTNA)
  - Cloud Access Security Brokers (CASB)

- SASE is key for securing modern distributed networks with mobile users and cloud-based services.

- SASE provides a secure and efficient way of connecting users and their devices.

### Security Service Edge (SSE)

- SSE is a subset of SASE, focusing exclusively on security services that safeguard interactions between users, devices, and cloud resources.

- SSE is a cloud-based security model designed to address the needs of today’s distributed and mobile workforce, unlike traditional network security architectures that rely on physical hardware at the network perimeter.

- SSE leverages cloud-based security services to protect distributed users and devices.

- SSE aims to provide comprehensive security coverage for users accessing applications and data from various locations, including remote offices, branch offices, and mobile devices.

- SSE includes

  - Secure Web Gateways (SWG): Filters malware and monitors web traffic.

  - Cloud Access Security Brokers (CASB): Manages and enforces cloud-based security policies.

  - Zero Trust Network Access (ZTNA): Ensures only authorized users can access applications and services, reducing the risk of internal threats.

#### Key Benefits

##### SASE

- Provides secure, seamless access across distributed networks.
- Uses cloud-native solutions for WAN and security, improving efficiency.
- Supports global scalability through flexible, cloud-integrated services like AWS VPC, Azure Virtual WAN, and Google Cloud Interconnect.

##### SSE

- Focuses on security controls for cloud environments.
- Implements robust threat protection for data access and user activities.
- Applies Zero Trust principles, securing all connections regardless of the user's location or device.
