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
(https://www.bowneconsultingcontent.com/pub/EH/proj/D7.htm)

And, I got many helps from TCM discord.

## Attacking Active Directory: Initial Attack Vectors

1.  LLMNR(Link Local Multicast Name Resolution) Poisoning attack

    - LLMNR (Link-Local Multicast Name Resolution): A protocol used for name resolution on local networks when DNS is unavailable. It allows devices to query each other directly for name resolution.

    - NBT-NS (NetBIOS Name Service): A legacy protocol for name resolution over IP networks, primarily used in Windows environments.

    Both protocols can be exploited by attackers through poisoning attacks, where malicious actors respond to legitimate queries with fake data to intercept or redirect traffic.

    Here are the attack processes

    Step 1, Run `responder`

    `responder` is a tool to capture credentials, for example, once a target sends out an LLMNR request by inputting attacker's ip address (`\\192.168.64.11`) on the File explorer, the `responder` will send a response to the server directing all traffic to the attacker.

    `sudo responder -I eth0 -dwv`

    `-I eth0` is to specify the network interface to use.

    `-d` is to run the responder in diagnostic mode.

    `-w` is to capture WPAD requests and serve malicious responses.

    `-v`is to get detailed information about the what responder is doing.

    Waiting for the response.

    ![waitingResponse1](../assets/img/AD/Screenshot%202024-07-17%20at%2010.18.05.png)

    ![waitingResponse2](../assets/img/AD/Screenshot%202024-07-17%20at%2010.38.30.png)

    Step 2, Input attacker's ip address on the victim's (THEPUNISHER(Computer Name) - fcastle(User Name)) and Get the response from it.

    ![connectingToAttacker1](../assets/img/AD/Screenshot%202024-07-17%20at%2010.45.53.png)

    ![connectingToAttacker2](../assets/img/AD/Screenshot%202024-07-17%20at%2010.17.46.png)

    ![connectingToAttacker3](../assets/img/AD/Screenshot%202024-07-17%20at%2010.48.48.png)

    ### What is NTLM?

    It is a suit of Microsoft security protocols for providing authentication, integrity, and confidentiality to users. It is a different with Kerberos protocol.

    One of the characteristics is that the hash used by NTML is not as strong as the encryption method used by Kerberos protocol.

    Here is the authentication process of NTML protocol

    ![ntlmProtocol](../assets/img/AD/server-during-ntlm-authentication.png)

    Step 3, Save one of the hashes and crack the hash

    ![saveHashes1](../assets/img/AD/Screenshot%202024-07-17%20at%2010.52.36.png)

    ![saveHashes2](../assets/img/AD/Screenshot%202024-07-17%20at%2010.52.50.png)

    Need to set a proper module to crack the password

    Since the smb response was `NTMLv2`, I considered to set `5600`. However I visited `hashcat` wiki to check the hash format that I want to crack.

    ![crackPassword1](../assets/img/AD/Screenshot%202024-07-17%20at%2010.53.38.png)

    ![crackPassword2](../assets/img/AD/Screenshot%202024-07-17%20at%2010.53.27.png)

    Attempt to crack the hashed password with the module and wordlists

    ![crackPassword3](../assets/img/AD/Screenshot%202024-07-17%20at%2010.54.02.png)

    ![crackPassword4](../assets/img/AD/Screenshot%202024-07-17%20at%2010.54.17.png)

    ![crackPassword5](../assets/img/AD/Screenshot%202024-07-17%20at%2010.54.27.png)

    Cracked password is `Password1`

2.  LLMNR(Link Local Multicast Name Resolution) Poisoning Defenses (Mitigation)

    To disable `LLMNR`, just select "Turn OFF multicast name resolution".

    In the DC server,

    ![server](../assets/img/AD/Screenshot%202024-07-17%20at%2012.22.59.png)

    Go to Group Policy Management

    Click `Computer Configuration` > `Administrative Templates` > `Network` > `DNS Client` > `Turn off the multicast name resolution`

    ![groupPolicyManagement](../assets/img/AD/Screenshot%202024-07-17%20at%2012.25.59.png)

    Hit the `Enabled` > `Apply` > `OK`

    ![groupPolicyManagement](../assets/img/AD/Screenshot%202024-07-17%20at%2012.26.14.png)

    To disable `NBT-NS`, just select "Disable NetBIOS over TCP/IP".

    Go to `Network Connections` > `Network Adapter Properties` > `TCP/IPv4 Properties` > `Advanced tab` > `WINS tab` > `Disable NetBIOS over TCP/IP`

    ![disableNBT1](../assets/img/AD/Screenshot%202024-07-17%20at%2012.50.25.png)

    ![disableNBT2](../assets/img/AD/Screenshot%202024-07-17%20at%2012.50.59.png)

    ![disableNBT3](../assets/img/AD/Screenshot%202024-07-17%20at%2012.51.15.png)

    ![disableNBT4](../assets/img/AD/Screenshot%202024-07-17%20at%2012.51.39.png)

    If a company must use or cannot disable LLMNR/NBT-NS, the best course of action is to require **strong password** and **Network Access Control** for ensuring only authorized devices connections to the network.

3.  SMB Relay Attacks

    SMB is a protocol for a network file sharing.

    Instead of capturing a hash with the responder tool, this SMB Relay Attack occurs when an attacker captures authentication requests (like password hashes) and then relays them to another machine to gain unauthorized access.

    The relayed user credentials need to have administrative privileges on the target machine to provide significant access. This is why targeting admin accounts is crucial. And I cannot relay the credentials to the same machine the credentials were captured from.

    At the moment, Frank Castle (username) from the MARVEL.local domain is admin privileged on two machines (THEPUNISHER and SPIDERMAN)

    1. Identify the workstations without SMB singing enforced(set as default)

    `nmap --script=smb2-security-mode.nse -p445 192.168.64.0/24`

    ![defaultSetting1](../assets/img/AD/Screenshot%202024-07-17%20at%2015.15.22.png)

    ![defaultSetting2](../assets/img/AD/Screenshot%202024-07-17%20at%2015.15.32.png)

    The result says "Message signing enabled but not required". That means this is a default setting for all Windows workstations. Attackers can exploit this weak validation for gaining shell access.

    2. Set up Responder.conf (SMB = Off, HTTP = Off)

    ![offSetting1](../assets/img/AD/Screenshot%202024-07-17%20at%2015.18.38.png)

    Yes, I used mousepad for the quick revision.

    ![offSetting2](../assets/img/AD/Screenshot%202024-07-17%20at%2015.18.33.png)

    The reason behind this is that I will utilize `Responder` and `ntlmrelayx` for this attack.

    To be specific, if the responder is listening for SMB or HTTP requests, it may respond to the captured authentication requests instead of allowing them to be relays. Moreover, by disabling SMB and HTTP in Responder, it can be ensured that only desired traffic (LLMNR or NBT-NS) should be captured and then forwarded to `ntlmrelayx`.

    Launch the responder

    ![launching1](../assets/img/AD/Screenshot%202024-07-17%20at%2015.37.49.png)

    ![launching2](../assets/img/AD/Screenshot%202024-07-17%20at%2015.37.56.png)

    ![launching3](../assets/img/AD/Screenshot%202024-07-17%20at%2015.38.08.png)

    Finally, start `ntlmrelayx` and wait for an event to occur

    ![launching4](../assets/img/AD/Screenshot%202024-07-17%20at%2015.44.27.png)

    Ready to go!

4.  Input the attack ip address on the victim machine (THEPUNISHER) for occurring an event

    The responder captures this event and then passes it to `ntlmrelayx`.

    In `Responder`,

    ![responderResult](../assets/img/AD/Screenshot%202024-07-17%20at%2016.04.12.png)

    In `ntlmrelayx`, local SAM hashed are dumped. These hashes can be cracked.

    ![credentials](../assets/img/AD/Screenshot%202024-07-17%20at%2016.07.21.png)

    Other kinds of relay attack

    I can gain a shell access by SMB client.

    Here are the processes.

    `ntlmrelayx.py –tf targets.txt –smb2support -i`

    ![accessingShell1](../assets/img/AD/Screenshot%202024-07-17%20at%2016.13.34.png)

    ![accessingShell2](../assets/img/AD/Screenshot%202024-07-17%20at%2016.13.44.png)

    It says "Started interactive SMB client shell via TCP on 127.0.0.1:11000", let's begin to connect this SMB Client shell!

    ![gainAccess1](../assets/img/AD/Screenshot%202024-07-17%20at%2016.14.00.png)

    ![gainAccess2](../assets/img/AD/Screenshot%202024-07-17%20at%2016.14.07.png)

5.  SMB Relay Attack Defenses (Mitigation)

    - Enabling SMB signing on all devices can completely stop the attack, but it can cause performance issues with file copies and legacy devices using SMBv1

    `Computer Configuration` > `Policies` > `Windows Settings` > `Security Settings` > `Local Policies` > `Security Options`

    Enabled:

    Microsoft network client: Digitally sign communications (always)
    Microsoft network client: Digitally sign communications (if server agrees)
    Microsoft network server: Digitally sign communications (always)
    Microsoft network server: Digitally sign communications (if client agrees)

    - Disabling NTLM authentication on network can completely stops the attack. However, if Kerberos stops working, Windows defaults back to NTML

    - Account tiering limits domain admins to specific tasks, for example only log onto servers with need for DA. But it can enforce the policy difficult

    - Local admin restriction can prevent a lot of lateral movement. Nevertheless, but it can also increase the workload for the service desk because Service desk staff might need to frequently grant temporary administrative rights or perform administrative tasks on behalf of users.

6.  IPv6 Attacks

7.  IPv6 Attack Defenses

8.  Passback Attacks

9.  Other attacks
