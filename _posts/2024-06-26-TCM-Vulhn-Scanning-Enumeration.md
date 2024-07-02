---
layout: post
title: TCM - practice for Kioptrix Lab
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through Kioptrix lab - level1
tags: [ethical hacking, tcm, pjpt, kioptrix, utm, level1]
comments: true
author: Lantana Park
---

# Kioptrix Lab (Level 1)

## Preparation

As a UTM user, it was really hard to install kioptrix lab in my utm machine. Thankfully, TCM provided `.7z` converted file for the UTM users. I could just follow the given instruction from TCM discord.

1. Downloaded `Kioptrix_utm.7z`

   ![download](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.25.03.png)

2. Extracted the contents of this compressed file. `7zz x Kioptrix_utm.7z`

   ![decompressed1](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.16.56.png)

   ![decompressed2](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.17.12.png)

3. Installed the decompressed file on my UTM machine

   ![install](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.29.38.png)

4. Run this machine and then test the network connection using `ping 8.8.8.8` (google dns ip address)

   ![test](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.52.38.png)

5. While running up on the Kioptrix lab, I found the lab's ip address on my kali machine and then ready to scan/enumerate the target machine.

   discovering lab's networking status

   `netdiscover -r 192.168.64.0/24`

   ![labnetworking](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.52.55.png)

   Scanning my lab machine from Kali

   `nmap -T4 -p- -A 192.168.64.15`

   ![scanning1](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.53.07.png)

   ![scanning2](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.53.18.png)

## Scanning/Enumeration

### trivial tip from class!

What makes me set apart from other people is my ability to information gathering and to enumerate the target. In my opinion, in order to collect the juicy information, it is required for me to learn more about the natures of each protocol and its vulnerabilities.

1. First, I visited the opened websites under `http`/`https` based on the outcomes of the `nmap` scan. (Scanning with `nmap`)

   ![website1](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.27.48.png)

   ![website2](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.27.59.png)

   ![website3](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2009.24.38.png)

Noted information
`80(http)/443(https) - 192.168.64.15`
`80/tcp    open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4`
`443/tcp   open  ssl/https   Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4`
`Default webpage - Apache Web Server/1.3.20 (Unix) - PHP`
`Document - https://192.168.64.15/manual/index.html Not Found`

Potential vulnerabilities

Apache httpd 1.3.20 - Root directory access

- https://www.exploit-db.com/exploits/19975
- https://httpd.apache.org/security/vulnerabilities_13.html
- https://www.cvedetails.com/vulnerability-list/vendor_id-45/product_id-66/version_id-371592/Apache-Http-Server-1.3.20.html?page=1&cvssscoremin=8&order=1&trc=8&sha=6d26d89b3754eda3acf4098d3cc8bf718f8405f6

2. Since I noticed there are websites running under `http` and `https`. I scanned the vulnerability of these services. I could not scan the `https` service, but scanned potential vulnerabilities `http` service. (Enumeration HTTP and HTTPS)

   `nikto -h http://192.168.64.15`

   `nikto` is to examine a web server to find potential problems and security vulnerabilities.

   `-h` option is to specify the host `http://192.168.64.15`.

   ![vulnerability](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.42.24.png)

   ![vulnerability2](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.42.46.png)

Noted information
`mod_ssl/2.8.4 - mod_ssl 2.8.7 and lower are vulnerable to a remote buffer overflow which may allow a remote shell.`

### What is mod_ssl?

It is an Apache HTTP Server module that provided support for SSL and TLS encryption for secure communication over HTTP and HTTPS. Since 2.8.7 is really older version of `mod_ssl`, I found common vulnerabilities by googling this web server version.

Potential vulnerabilities

(80/443) - `mod_ssl/2.8.4` - OpenLuck (remote buffer overflow for remote shell - CVE-2002-0082)

- https://www.exploit-db.com/exploits/47080
- https://github.com/heltonWernik/OpenLuck

Again, I searched potential vulnerabilities with `searchsploit`

![searchsploit](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2012.48.15.png)

### What is the buffer overflow attack?

In computer science, a data buffer temporarily holds data as it moves between locations, like from an input to an output device, and helps manage varying processing rates, typically using RAM for its quick access speed. Buffers often use queue algorithms (First In First Out) to balance timing, writing data at one speed and reading it at another.

Attackers can exploit the buffer overflows to corrupt a web application's execution stack, taking advantage of user's input, if the data storage space is fixed. There are two types of the buffer overflow attack: **stack-based buffer overflow** and **heap-based buffer overflow**.

3. I scanned hidden directories of this service with using `dirbuster`. (Enumeration HTTP and HTTPS)

   ![dirbcommand](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.54.34.png)

   ![dirbcommand2](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.54.44.png)

   ![dirb1](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.12.35.png)

   ![dirb2](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.13.04.png)

   And visited some found directories

   ![visited2](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.13.26.png)

   ![visited1](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.46.39.png)

   ![visited3](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.43.29.png)

   ![chart1](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2012.12.56.png)

   ![chart2](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.41.47.png)

   ![chart3](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.42.05.png)

   Noted information
   `192.168.64.15/usage/usage_202406.html - Generated by Webalizer Version 2.01`

   ### What is webalizer?

   It is **a web log analysis software tool**. It has multiple cross-site scripting vulnerabilities that could allow malicious HTML tags to be injected in the reports.

   Potential vulnerabilities
   `192.168.64.15/usage/usage_202406.html` - multi cross-site scripting vulnerabilities or remote buffer overflow

   - https://www.tenable.com/plugins/nessus/10816 (cross-site scripting)
   - https://www.cvedetails.com/cve/CVE-2002-0180/ (remote buffer overflow)
   - https://cve.mitre.org/cgi-bin/cvename.cgi?name=2002-0180 (remote buffer overflow)

4. I scanned the target address for enumerating SMB protocol.

   I used `matasploit` to identify the version of SMB protocol

   Entering to `metasploit` took kit

   ![msfconsole](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2009.42.39.png)

   ![msfconsole2](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2009.42.45.png)

   Searching auxiliaries of SMB for scanning its version

   ![search](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.26.03.png)

   ![outcomes](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.26.03.png)

   Getting info to use this auxiliary for scanning the target smb protocol

   ![info1](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.24.28.png)

   ![info2](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.24.41.png)

   Setting RHOST(the target ip) to exploit

   ![rhost](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.24.59.png)

   Furthermore, I use `smbclient` to check out the shared resources on a server that uses the smb protocol.

   ![smbclient](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2018.16.11.png)

   I found that, `IPC$` can be accessible without the password input.

   ![smbclient2](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2010.01.09.png)

   Noted information

   `139 / tcp  open  netbios-ssn Samba smbd (workgroup: MYGROUP)`

   `Host script results:`
   `|_smb2-time: Protocol negotiation failed (SMB2)`
   `|_clock-skew: -3d05h31m10s`
   `|_nbstat: NetBIOS name: KIOPTRIX, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)`

   `Unix (Samba 2.2.1.a)`

   `IPC$ is accessible using smbclient with no password input`

   ### What is **SMB**(139 or 445 ports)?

   It is for providing shared access to files, printers, and serial ports between nodes on a network. And this protocol allows applications on a computer to read and write to files and to request services from server programs in a computer network. The popular vulnerability using this protocol is **EternalBlue**.

   I just scanned this target machine's protocol to identify the version of SMB in this enumeration process.

   Potential vulnerabilities

   (139)`Samba 2.2.1a` - Remote Buffer Overflow (tran2open)

   - https://www.rapid7.com/db/modules/exploit/linux/samba/trans2open/
   - https://www.exploit-db.com/exploits/22468

5. I just made some tries to login the target ssh without login.

   ### What is SSH(Secure Shell) protocol?

   It is to access a computer over unsecure network. It provides strong password authentication and public authentication, as well as encrypted data communication between two computers. It is widely used for managing servers and network devices securely.

   ![ssh1](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2018.26.08.png)

   **Key exchange algorithms** in `SSH` is to enable the secure negotiation and derivation of a shared session key. This session key, in turn, are used to encrypt data, ensuring confidentiality and integrity throughout the SSH session.

   **Host key algorithms** is to tell the SSH client to accept these specific types of host key algorithms from server. In short, it is to verify the authenticity of the SSH server they are connecting to.

   **ciphers** is used to encrypt and decrypt data transmitted between the client and server. Once the session keys are derived, the keys are used by the symmetric encryption ciphers (like AES) to encrypt data transmitted between the client and server. Each SSH session uses its own session keys for encrypting and decrypting the data exchanged during that session

   Noted information

   `22/tcp    open  ssh         OpenSSH 2.9p2 (protocol 1.99)`
   `Still not accessible`

   Potential vulnerabilities

   `OpenSSH 2.9p2` - Token Buffer Overflow

   - https://www.exploit-db.com/exploits/21402

   ![potential](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2018.30.05.png)

## Scanning with Nessus

There is a tool to comprehensively scan the vulnerabilities of the target machine, which is called `Nessus`.

Here is the steps to use this service.

1. Downloaded/installed the file.

   I selected `aarch64`, instead of `amd`, because I am using M1 mac os.

   ![failed](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.59.04.png)

   ![aarch64Selection](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2012.03.14.png)

   ![successDownload](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.59.15.png)

   ![successDownload2](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.59.29.png)

2. Selected Basic scan and set the scanning configuration

   ![setting1](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.05.30.png)

   ![setting2](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.06.54.png)

   ![setting3](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.07.32.png)

   ![setting4](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.08.06.png)

   ![setting5](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2011.12.20.png)

3. From now on, I am going to use this scanned potential vulnerabilities in the process of exploitation.

   ![setting6](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2012.12.50.png)

   ![setting7](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2012.12.20.png)

## Exploitation
