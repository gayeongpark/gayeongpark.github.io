---
layout: post
title: TCM - Active Directory Lab Building (Vol2)
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through active directory lab build (Vol2)
tags: [ethical hacking, tcm, pjpt, active directory, windows, lab building]
comments: true
author: Lantana Park
---

# Active directory 2

## Attacking Active Directory: Post-Compromise Attacks

- Pass Attacks

1. Have access via password

CrackMapExec is a post-exploitation tool that helps automate assessing the security of AD network.

I used CrackMapExec to gather essential SMB information.

![stolen1](../assets/img/AD2/Screenshot%202024-07-22%20at%2010.29.24.png)

`SMB 192.168.64.33 445 THEPUNISHER [*] Windows 11 Build 22621 x64 (name:THEPUNISHER) (domain:MARVEL.local) (signing:FALSE) (SMBv1:False)`

`Windows 11 Build 22621 x64` is the operating system information for the target machines being used.

`name:THEPUNISHER` is hostname
`domain:MARVEL.local` is domain name

`SMB 192.168.64.34 445 SPIDERMAN [+] MARVEL.local\fcastle (Pwn3d!)` and `SMB 192.168.64.33 445 THEPUNISHER [+] MARVEL.local\fcastle (Pwn3d!)` indicate that privileged access was obtained.

`SMB 192.168.64.32 445 HYDRA-DC [+] MARVEL.local\fcastle` says that Successful authentication to `HYDRA-DC` with the same credentials, but no privileged access indicated.

The term `Pwn3d!` in the output implies that the account `fcastle` has administrative or privileged access on `THEPUNISHER` and `SPIDERMAN`, but not necessarily on `HYDRA-DC`. This might be because `fcastle` has local administrator rights on these machines(`THEPUNISHER` and `SPIDERMAN`), not Domain Admin and Enterprise Admin rights.

At the moment, I have the access of local admins of the two machines - `THEPUNISHER` and `SPIDERMAN`.

2. Have access via NTLM hashes

![stolenViaHashes1](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.03.23.png)
![stolenViaHashes2](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.00.21.png)

`--local-auth` option indicates that the tool - `CrackMapExec` should perform local authentication. This means it will try to authenticate against the local account database on each target machine, rather than using domain-based authentication.

![stolenViaHashes3](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.04.50.png)

![stolenViaHashes4](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.05.03.png)

### What is the Security Accounts Manager (SAM)?

SAM is a database file in the Microsoft Windows operating system that contains usernames and passwords. The credentials are encrypted. The SAM database file is stored within `C:\Windows\System32\config`. the access is restricted.

`--sam` option tells `crackmapexec` to attempt to dump the Security Account Manager (SAM) database from the target machines, after a successful authentication.

![stolenViaHashes5](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.05.18.png)

`--shares` makes `crackmapexec` to enumerate shared resources (shares) on the target machines after successful authentication.

This is not I am connecting with these shares. Just for enumerating.

`ADMIN$`, `C$`, and `IPC$` are shared in both machines

`ADMIN$` allows remote management and administrative access to the machine. It provides access to the Windows directory on the system(C:\Windows), enabling system administrators to perform tasks remotely.

`C$` provides access to the entire C: drive and is used for broader file management tasks.

`IPC$` is not used for file sharing. Instead, it is utilized for communication between networked processes.

![stolenViaHashes5](../assets/img/AD2/Screenshot%202024-07-22%20at%2013.23.00.png)

![stolenViaHashes6](../assets/img/AD2/Screenshot%202024-07-22%20at%2013.20.49.png)

`--lsa` specifies that the LSA secrets should be dumped. LSA secrets include sensitive data such as passwords and encryption keys stored by the LSA service.

In the result, SMB service was detected.

I can notify that local admin in `SPIDERMAN` and `THEPUNISHER` have same password according to the hashes. And then it is possible to crack the password using `hashcat` and `John the Ripper`.

`aes256-cts-hmac-sha1-96` indicates the encryption algorithms and mode.

`0d4394f7ec3f961f4cc5b81ec667168921c6e5400b490f491d1d0a5d10b18435` is an encryption key used in the SMB protocol.

![stolenViaHashes8](../assets/img/AD2/Screenshot%202024-07-22%20at%2013.06.57.png)

![stolenViaHashes9](../assets/img/AD2/Screenshot%202024-07-22%20at%2013.07.08.png)

`-L` is to list out all of the modules that are available to use with SMB.

![stolenViaHashes10](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.05.55.png)



![stolenViaHashes11](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.06.09.png)

![stolenViaHashes12](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.06.18.png)

`cmedb` allows me to interact with the CME database, displaying information about hosts and credentials collected during my network scanning and penetration testing activities.

`hosts` is to list all the hosts recorded in the database.

`creds` is to list all the credentials.

## Additional Active Directory Attacks

## Attacking Active Directory: Post Exploitation
