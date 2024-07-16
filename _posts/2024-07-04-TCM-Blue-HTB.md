---
layout: post
title: TCM - practice for blue Lab
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through blue lab from HTB
tags: [ethical hacking, tcm, pjpt, blue, easy-peasy]
comments: true
author: Lantana Park
---

# Blue

I have solved Blue capstone today. Scanning and enumeration were easy though, exploitation from the discovered vulnerability was complicated for me. During solving this capstone, I could learn about window and its vulnerabilities.

Here is my target machine. Since I did not know the passwords of admin and user, I could not test about networking connection of the victim machine. Luckily I could find the target ip address on my kali.

![finding](../assets/img/blue/Screenshot%202024-07-04%20at%2009.20.47.png)

![pingTest](../assets/img/blue/Screenshot%202024-07-04%20at%2009.20.35.png)

## Scanning

1. Scanned the opened ports of the target machine.

   ![nmapScan1](../assets/img/blue/Screenshot%202024-07-04%20at%2021.19.40.png)

   ![nmapScan2](../assets/img/blue/Screenshot%202024-07-04%20at%2021.20.03.png)

Noted information

`Running: Microsoft Windows 7|2008|8.1`
`135/tcp   open  msrpc    	Microsoft Windows RPC`
`139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn`
`445/tcp   open  microsoft-ds Windows 7 Ultimate 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)`

2. I could not get valuable information through this scanning. So I tried to scan this machine more deeply.

   `nmap -T4 -A -sV --script=exploit,vuln 192.168.64.19`

   I added `--script-exploitm,vuln` to specify Nmap Scripting Engine scripts to check for potential vulnerabilities and its exploitation.

   ![detailedscanning1](../assets/img/blue/Screenshot%202024-07-04%20at%2021.50.48.png)

   ![detailedscanning2](../assets/img/blue/Screenshot%202024-07-04%20at%2021.50.57.png)

   Thankfully, I could get fruitful information about its vulnerability and how to exploit it.

Noted information

`Host script results:`

`|_smb-vuln-ms10-061: NT_STATUS_OBJECT_NAME_NOT_FOUND`

`|_smb-vuln-ms10-054: false`

`| smb-vuln-ms17-010:`

`|   VULNERABLE:`

`|   Remote Code Execution vulnerability in Microsoft SMBv1 servers(ms17-010)`

`| 	State: VULNERABLE`

`| 	IDs:  CVE:CVE-2017-0143`

`| 	Risk factor: HIGH`

`|   	A critical remote code execution vulnerability exists in Microsoft SMBv1`

`|    	servers (ms17-010).`

`|`

`| 	Disclosure date: 2017-03-14`

`| 	References:`

`|   	https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/`

`|   	https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143`

`|_  	https://technet.microsoft.com/en-us/library/security/ms17-010.aspx`

Thanks to the information, I search about `ms17-010` - `CVE:CVE-2017-0143`.

- https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_eternalblue/

- https://www.exploit-db.com/exploits/42315

## Enumeration

1. Tried to access the window smb files using `smbclient` without password input. However, it failed...

   ![smbclient1](../assets/img/blue/Screenshot%202024-07-04%20at%2022.18.55.png)

   ![smbclient2](../assets/img/blue/Screenshot%202024-07-04%20at%2022.19.02.png)

   ![smbclient3](../assets/img/blue/Screenshot%202024-07-04%20at%2022.19.08.png)

   ![smbclient4](../assets/img/blue/Screenshot%202024-07-04%20at%2022.19.17.png)

2. Additionally, identified the founded vulnerability by using `metasploit` - `scanner/smb/smb_ms17_010` module.

   ![metasploitEnumeration1](../assets/img/blue/Screenshot%202024-07-04%20at%2022.27.07.png)

   ![metasploitEnumeration2](../assets/img/blue/Screenshot%202024-07-04%20at%2022.27.29.png)

   ![metasploitEnumeration3](../assets/img/blue/Screenshot%202024-07-04%20at%2022.27.42.png)

   ![metasploitEnumeration4](../assets/img/blue/Screenshot%202024-07-04%20at%2022.28.00.png)

   I could ensure that `MS17-010` can be the low hanging fruit (easy to exploit) for now. So I decided to exploit this vulnerability.

## Exploitation

1. When I search about `MS17-010` on google, I could see `MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption` - exploitation method. So, I gave a try to exploit it.

   resourced from (https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_eternalblue/)

   ![exploitation1](../assets/img/blue/Screenshot%202024-07-04%20at%2022.35.19.png)

   ![exploitation2](../assets/img/blue/Screenshot%202024-07-04%20at%2022.35.31.png)

   ![exploitation3](../assets/img/blue/Screenshot%202024-07-04%20at%2022.35.42.png)

   ![exploitation5](../assets/img/blue/Screenshot%202024-07-04%20at%2022.35.49.png)

   ![exploitation6](../assets/img/blue/Screenshot%202024-07-04%20at%2022.35.58.png)

   ![exploitation7](../assets/img/blue/Screenshot%202024-07-04%20at%2022.36.06.png)

   ![exploitation8](../assets/img/blue/Screenshot%202024-07-04%20at%2022.36.15.png)

   Failed... but, I set the target - window 8.1 replacing window 7

   ![exploitation9](../assets/img/blue/Screenshot%202024-07-04%20at%2022.36.35.png)

   ![exploitation10](../assets/img/blue/Screenshot%202024-07-04%20at%2022.36.46.png)

   ![exploitation11](../assets/img/blue/Screenshot%202024-07-04%20at%2022.37.01.png)

   I checked if this shell has system user authentication.

   ![exploitation12](../assets/img/blue/Screenshot%202024-07-04%20at%2022.37.57.png)

   ![exploitation13](../assets/img/blue/Screenshot%202024-07-04%20at%2022.38.22.png)

   I found the hashed passwords of the registered users. So tried to crack these passwords.

   ![exploitation14](../assets/img/blue/Screenshot%202024-07-04%20at%2022.39.24.png)
