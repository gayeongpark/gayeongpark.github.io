---
layout: post
title: TCM - Active Directory Lab Building
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through active directory lab build
tags: [ethical hacking, tcm, pjpt, active directory, windows, lab building]
comments: true
author: Lantana Park
---

# Active directory

## Overview

### What is the active directory?

Active Directory (AD) is like a phone book for Windows networks. Approximately 95% of Fortune 1000 companies implement this service in their networks, making it a core component of most enterprise environments since its release in 2000. AD can be exploited not by attacking patchable vulnerabilities but by abusing its features, trusts, and components.

The critical concept of AD is **Centralization** for the creation and management of user accounts. User accounts are stored as objects made up of attributes. A wide variety of objects are stored in the Active Directory database. It utilizes the **Kerberos protocol** for secure authentication, ensuring that users can efficiently and securely access network resources. When users attempt to log on to a network using Active Directory, several processes and components work together to ensure secure and efficient access to resources.

Here are the logon processes:

1. Once a user attempts to log on to a network by typing username and password, the client computer sends this information to the Active Directory server, which is called the Domain Controller.

2. The DC(Domain controller) checks user's name and password. If they are correct, DC creates a special digital pass called a Ticket Granting Ticket (TGT). It is like a temporary ID card. With this ticket, a user can request access to other network resources without needing to re-enter credentials.

3. If a user wants to access a resource, the client computer asks the Domain Controller for a Service Ticket specific to that resource.

4. Once a user accesses the resource they want, the resource checks the Service Ticket and lets the user in if every is correct.

5. Changes for user accounts, security policies, and other directory information are replicated across all domain controllers to ensure consistency.

Since the user password is not sent around the network all the time, the encrypted tickets can provide the enhanced authorization and authentication service.

And it can be convenience because users can access multiple resources without re-entering their passwords.

Finally, admin can easily manage user access and enforce security policies from a central location.

### Physical Active Directory Components

- **Domain Controllers(DCs)** hosts a phone book. It provides authentication and authorization services. And it allows administrative access to manage user accounts and network resources. Once a user modify/create an account information, domain controllers replicate updates to other domain controllers. It handles authentications issuing Kerberos tickets(ticket granting ticket and service ticket). Organizations typically deploy several Domain Controllers (DCs), each of which maintains a copy of the directory for the entire domain.

- **AD DS(Domain Services) Data Store** contains the database files and processes that store and manage directory information for users, services, and applications. It consists of the `Ntds.dit` file. It is stored by default in the `%SystemRoot%\NTDS` folder on all domain controllers. The data store is accessible only through the domain controller processes and protocols.

- **Global Catalog Server** contains the information about Active Directory objects of all domains within a forest, enabling users and applications to find directory information regardless of which domain is it in.

- **Read-Only Domain Controller (RODC)** is a type of domain controller that stores a read-only copy of the Active Directory database.

![physical](../assets/img/AD/Screenshot%202024-07-14%20at%2021.36.00.png)

### Logical Active Directory Components

- **Schema** defines every type of object that can be stored in the directory. It enforces rules regarding object creation and configuration. It serves as a rule-book or blueprint.

  - **Class object** represents the types of objects that can be created in the directory, such as User, Computer, and Printer.
  - **Attribute object** refers to the information that can be attached to an object, such as Display name.

- **Domains** are used to group and manage objects in an organization. (www.google.com)

  - **An administrative boundary** is for applying policies to groups of objects
  - **A replication boundary** is for replicating data between domain controllers
  - **An authentication and authorization boundary** provides a way to limit the scope of access to resources

- **Tree** is a hierarchy of domains in Active Directory Domain Services (AD DS). For example, domains like news.google.com, mail.google.com, and translate.google.com share a contiguous namespace with the parent domain, google.com. By default, a tree creates a two-way transitive trust with other domains within the same forest.

- **Forest** is a collection of one or more domain trees. It shares a common schema, configuration partition, global catalog to enable searching and the enterprise admins and schema admins groups. Furthermore, it enables trusts between all domains in the forest. And compromising a domain admin in a forest does not necessarily mean that that's an enterprise admin. However, it is possible to elevate to an enterprise admin or something like that by crossing the forest with that account.

- **Organizational Units(OUs)** are Active Directory containers that can hold users, groups, computers, and other OUs. OUs represent the organization hierarchically and logically, allowing for consistent management of a collection of objects, delegation of permissions to administer groups of objects, and the application of policies.

  Different types of objects

  - **User**: Enables network resource access for a user.
  - **InetOrgPerson**: Similar to a user account. Uses for compatibility with other directory services.
  - **Contacts**: Uses primarily to assign e-mail addresses to external users. and it does not enable network access.
  - **Groups**: Uses to simplify the administration of access control.
  - **Computers**: Enables authentication and auditing of computer access to resources.
  - **Printers**: Uses to simplify the process of locating and connecting to printers.
  - **Shared folders**: Enables users to search for shared folders based on properties.

![ADlogicalDiagram](../assets/img/AD/AD.jpeg)

- **Trusts** provide a mechanism for users to gain access to resources in another domain. All domains in a forest trust all other domains in the forest. And trusts can extend outside the forest.

  - **Directional trusts** flow from trusting domain to the trusted domain
  - **Transitive trusts** extend the relationship beyond a two-domain trust to include other trusted domains.

  ![adTrustsDiagram](../assets/img/AD/trust%20relationship.jpg)

## Building out AD lab

Requirements

- 1 Windows server 2022 for setting up domain controller / `192.168.64.32`
- 2 Windows 11 enterprise workstations for setting up user machines and policies

  - Computer Name: THEPUNISHER / `192.168.64.33`
    ![computername1](../assets/img/AD/Screenshot%202024-07-16%20at%2018.55.05.png)
  - Computer Name: SPIDERMAN / `192.168.64.34`
    ![computername2](../assets/img/AD/Screenshot%202024-07-16%20at%2018.54.34.png)

  ![filesDownload3](../assets/img/AD/Screenshot%202024-07-16%20at%2009.12.35.png)

  ![settingDC1](../assets/img/AD/Screenshot%202024-07-16%20at%2018.44.37.png)

  ![settingDC2](../assets/img/AD/Screenshot%202024-07-16%20at%2019.08.25.png)

  ![settingDC3](../assets/img/AD/Screenshot%202024-07-16%20at%2019.08.33.png)

  ![settingDC4](../assets/img/AD/Screenshot%202024-07-16%20at%2019.09.31.png)

  To verify Domain connections

  ![connectionWithPunisher](../assets/img/AD/Screenshot%202024-07-16%20at%2018.46.39.png)

  ![connectionWithSpiderMan](../assets/img/AD/Screenshot%202024-07-16%20at%2018.46.57.png)

  To verify DNS connections

  ![connectingCheckFromClient](../assets/img/AD/Screenshot%202024-07-16%20at%2018.51.56.png)

  ![connectingCheckFromClient](../assets/img/AD/Screenshot%202024-07-16%20at%2018.52.33.png)

  ![connectingCheckWithDC](../assets/img/AD/Screenshot%202024-07-16%20at%2019.11.51.png)

Even though I set my victim ad environment manually by following the heath's instructions, It will be great to use this resource if you want to set AD environment without any guidance.

(https://github.com/Dewalt-arch/pimpmyadlab?tab=readme-ov-file)

## Attacking Active Directory: Initial Attack Vectors

1. LLMNR(Link Local Multicast Name Resolution) Poisoning

   It is used to identify hosts when DNS fails to do so in a network. The key flaw is that, when I intercept the traffic in the network, I am able to capture a username and a hash when I respond to this traffic. Now this can be called "a man in the middle attack". It is to utilize weak password. In order to do this attack, I set really weak passwords on the victim machines.

   Here are the attack processes

   Step 1, Run `responder`

   `responder`

   `sudo responder -I tun0 -dw`

2. SMB Relay Attacks

3. SMB Relay Attack Defenses
