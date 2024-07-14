---
layout: post
title: TCM - Active Directory Lab Build
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through active directory lab build
tags: [ethical hacking, tcm, pjpt, active directory. windows]
comments: true
author: Lantana Park
---

# Active directory

## Overview

### What is the active directory?

Active Directory (AD) is like a phone book for Windows networks. Approximately 95% of Fortune 1000 companies implement this service in their networks, making it a core component of most enterprise environments since its release in 2000. AD can be exploited not by attacking patchable vulnerabilities but by abusing its features, trusts, and components.

The critical concept of AD is **Centralization** for the creation and management of user accounts. User accounts are stored as objects made up of attributes. A wide variety of objects are stored in the Active Directory database. It utilizes the **Kerberos protocol** for secure authentication, ensuring that users can efficiently and securely access network resources. When users attempt to log on to a network using Active Directory, several processes and components work together to ensure secure and efficient access to resources.

Logon process:

1. Once users attempt to log on to a network by typing username and password, the client computer sends this information to the Active Directory server, which is called the Domain Controller.

2. The DC checks user's name and password. If they are correct, DC creates a special digital pass called a Ticket Granting Ticket (TGT). It is like a temporary ID card. With this ticket, users can request access to other network resources without needing to re-enter credentials.

3. If users want to access a resource, the client computer asks the Domain Controller for a Service Ticket specific to that resource.

4. When users access the resource they want, the resource checks the Service Ticket and lets me if if every is correct.

5. Changes for user accounts, security policies, and other directory information are replicated across all domain controllers to ensure consistency.

Since my password is not sent around the network all the time, just the encrypted tickets, it can provide enhanced authorization and authentication service.

And it can be convenience because I can access multiple resources without re-entering my password

finally, admin can easily manage user access and enforce security policies from a central location.

### Physical Active Directory Components

- **Domain Controllers(DCs)** hosts a phone book. It provides authentication and authorization services. And it allows administrative access to manage user accounts and network resources. Once a user modify/create an account information, domain controllers replicate updates to other domain controllers. It handles authentications using Kerberos tickets. Organizations normally have several Domain Controllers, and each one has a copy of the directory for the entire domain.

- **AD DS(Domain Services) Data Store** contains the database files and processes that store and manage directory information for users, services, and application. It consists of the `Ntds.dit` file. It is stored by default in the `%SystemRoot%\NTDS` folder on all domain controllers. It is accessible only through the domain controller processes and protocols.

### Logical Active Directory Components

- **Schema** defines every type of object that can be stored in the directory. It enforces rules regarding object creation and configuration. It serves as a rule-book or blueprint.

  - **Class object** : Represents the types of objects that can be created in the directory, such as User, Computer, and Printer.
  - **Attribute object** : Refers to the information that can be attached to an object, such as Display name

- **Domains** are used to group and manage objects in an organization. (www.google.com)

  - **An administrative boundary** for applying policies to groups of objects
  - **A replication boundary** for replicating data between domain controllers
  - **An authentication and authorization boundary** that provides a way to limit the scope of access to resources

- **Tree** is a hierarchy of domains in AD DS. (google.com, dev.google.com, google.com.kr) It shared a contiguous namespace with the parent domain. By default, it creates a two-way transitive trust with other domains.

- **Forest** is a collection of one or more domain trees. It shares a common schema, configuration partition, global catalog to enable searching and the enterprise admins and schema admins groups. Finally, it enables trusts between all domains in the forest. compromising a domain admin in a forest does not necessarily mean that that's an enterprise admin. However, I can elevate to an enterprise admin or something like that by crossing the forest with that account.

- **Organizational Units(OUs)** are Active Directory containers that can hold users, groups, computers, and other OUs. OUs represent the organization hierarchically and logically, allowing for consistent management of a collection of objects, delegation of permissions to administer groups of objects, and the application of policies.

  #### Different types of objects

  - **User**: Enables network resource access for a user.
  - **InetOrgPerson**: Similar to a user account. Uses for compatibility with other directory services.
  - **Contacts**: Uses primarily to assign e-mail addresses to external users. and it does not enable network access.
  - **Groups**: Uses to simplify the administration of access control.
  - **Computers**: Enables authentication and auditing of computer access to resources.
  - **Printers**: Uses to simplify the process of locating and connecting to printers.
  - **Shared folders**: Enables users to search for shared folders based on properties.

![AD](../assets/img/AD/AD.jpeg)

- **Trusts** provide a mechanism for users to gain access to resources in another domain. All domains in a forest trust all other domains in the forest. And trusts can extend outside the forest.

  - **Directional trusts** flow from trusting domain to the trusted domain
  - **Transitive trusts** extend the relationship beyond a two-domain trust to include other trusted domains.

  ![adTrusts](../assets/img/AD/trust%20relationship.jpg)

## Building out AD lab
