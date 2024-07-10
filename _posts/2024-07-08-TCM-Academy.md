---
layout: post
title: TCM - practice for academy
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through academy lab from TCM
tags: [ethical hacking, tcm, pjpt, academy, privilege escalation]
comments: true
author: Lantana Park
---

# Academy

This lab was really difficult to solve, however I have learned a lot from this lab. Here is the steps I took in this lab.

## Scanning / Enumeration

1. Scanned the target machine. There are three main services that is running on the machine.

   `21/tcp open  ftp 	vsftpd 3.0.3`
   `22/tcp open  ssh 	OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)`
   `80/tcp open  http	Apache httpd 2.4.38 ((Debian))`

   ![nmapScanning1](../assets/img/academy/Screenshot%202024-07-08%20at%2021.18.27.png)

   ![nmapScanning2](../assets/img/academy/Screenshot%202024-07-08%20at%2021.18.39.png)

First, there was ftp server was running on the port 21. `ftp` is the protocol for transferring files. It only allows user to upload (`PUT`) files to the server from the client and download ('GET`) files from the server on the client device.

Second, there was openssh server was running on the port 22. `ssh` provides secured remote networking connection between client and server for remote login.

Third, there is http web service running on the port 80. First, there was an FTP server running on port 21. FTP is the protocol used for transferring files. It allows users to upload (PUT) files to the server from the client and download (GET) files from the server to the client device.

Second, there was an OpenSSH server running on port 22. SSH provides a secure remote networking connection between the client and server for remote login.

Third, there is an HTTP web service running on port 80. I thought it would be great to scan the hidden directories of this service.

2. Checked the hidden directories using `gobuster` and `dirbuster`.

   I found there is `/phpmyadmin` page. However I could get any username and password information for authentication..

   ![directory1](../assets/img/academy/)

   ![directory2](../assets/img/academy/Screenshot%202024-07-08%20at%2021.37.52.png)

   So tried to use `dirbuster`using large wordlist file.

   Beside `/phpmyadin`, I found `/academy` page of the http server.

   ![academy1](../assets/img/academy/Screenshot%202024-07-08%20at%2021.49.37.png)

   ![academy2](../assets/img/academy/Screenshot%202024-07-08%20at%2021.51.13.png)

   I checked out the source code of the page, unfortunately, could not get any invaluable information to login.

   So I went through the vulnerabilities of FTP server. According to googling the vulnerability of the `vsftpd 3.0.3`, I found there is anonymous login that I can exploit easily. 

   I referred to this blog. 

   (https://www.linkedin.com/pulse/pentesting-exploiting-ftp-servers-kubotor)

3. Inputted `anonymous` for username, and then no input the password. 

    ![ftpLogin1](../assets/img/academy/Screenshot%202024-07-08%20at%2021.59.10.png)

    Downloaded the `note.txt` file in order to identify what this file is. 

    ![ftpLogin2](../assets/img/academy/Screenshot%202024-07-08%20at%2021.59.28.png)

    Based on the file, grimmie had setup a test website for the new academy. I could notice that this is the information for login `/academy`  

    I used online password cracking tool, and then got the cracked passwd `student`

    ![password](../assets/img/academy/Screenshot%202024-07-08%20at%2013.49.21.png)





