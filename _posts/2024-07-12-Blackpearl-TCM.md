---
layout: post
title: TCM - practice for blackPearl capstone
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through blackPearl lab from TCM
tags: [ethical hacking, tcm, pjpt, blackPearl, privilege escalation, dns, easy]
comments: true
author: Lantana Park
---

# BlackPearl

## Scanning / Enumeration

1. As usual, I started to scan the nmap of the target machine for a comprehensive scanning.

   `nmap -T4 -p- -A 192.168.64.25`

   ![nmapScan1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2017.23.18.png)

   ![nmapScan2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2017.23.28.png)

   Noted information

   `22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)`

   `53/tcp open  domain  ISC BIND 9.11.5-P4-5.1+deb10u5 (Debian Linux)`

   `80/tcp open  http    nginx 1.14.2`

   There were only three services running on the target machine.

   ### What is DNS(53) protocol?

   ISC BIND (Berkeley Internet Name Domain) is a software suite for managing Domain Name System (DNS) services on the internet. It is maintained by the Internet Systems Consortium (ISC). For example, when we visit google.com, DNS resolves the domain name into an IP address. BIND9 provides the mechanisms needed for translating human-readable domain names(google.com) into IP addresses(2607:f8b0:4005:813::200e - IPv6) and vice versa.

   In this command:

   - `9.11.5` is the version of BIND.
   - `P4` is the patch level for BIND.
   - `5.1` is the Debian-specific revision of the BIND package.
   - `+deb10u5` is the package is built for Debian 10 and has had 5 additional updates since the initial release.

   ![dnsResolution](../assets/img/blackpearl/solarwinds-bind-01.png)

2. I attempted to find uncovered directories on the server by using `gobuster`

   ![gobusting](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2018.26.54.png)

   I found `/secret` page. Once I visited this page, it made me download a secret file.

   ![secretPage](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2018.29.10.png)

   Hm... It said `Directory busting won't give anything`. Is that true? um...

   ![homePage](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2018.32.11.png)

   ![usingHydraforBrute-forcing](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2018.54.29.png)

   Failed to find the password for accessing openssh(22).....

   At that moment, I was really confused because there were no interesting clues such as cms version, file upload page, login page, robots.txt, or directory pages.

   So that I opened the inspection page for this website.

   ![openingInspection1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2018.31.16.png)

   ![openingInspection2](../assets/img/blackpearl/Screenshot%202024-07-13%20at%2009.27.53.png)

   ![openingInspection3](../assets/img/blackpearl/Screenshot%202024-07-13%20at%2009.19.32.png)

   There was a comment line mentioning `alek@blackpearl.tcm`. And it appeared that `blackpearl.tcm` might be another hostname accessible in firefox. The reason I thought in this way was that I have some previous experiences of adding a hostname and ip for fixing dns issues. In those instances, resolving DNS issues by adding a hostname and IP address to my local `/etc/hosts` file often resolved the problem of accessing web services. This approach was effective especially when dealing with non-publicly resolved hostnames, which could otherwise result in a blank page with no content.

   To gather more information for enumerating this HTTP service, I added the hostname and IP address to the `/etc/hosts` file.

   ![addinghost1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.02.39.png)

   ![addinghost2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.03.15.png)

   And then attempted to find hidden directories.

   ![finding1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.06.02.png)

   ![finding2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.05.48.png)

   ![finding3](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.05.31.png)

   First, `/`, `index.php`

   ![indexPage1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.07.25.png)

   Second, `/crossdomain.xml`

   ![foundedPage2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.09.56.png)

   Final, `/navigate`

   ![foundedPage3](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.10.53.png)

   ![foundedPage4](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.11.27.png)

   `/navigate` page used `Navigate CMS v2.8`.

   I thought it would be great to utilize this cms vulnerability to get a shell at first.

   By googling navigate cms v2.8, I found a really attractive resource, which is the exploitation of Unauthenticated Remote Code Execution vulnerability.

   resourced from (https://www.rapid7.com/db/modules/exploit/multi/http/navigate_cms_rce/)

   ![foundedVuln1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.15.29.png)

   ![foundedVuln2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.15.59.png)

   ![foundedVuln3](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2019.16.08.png)

## Exploitation

1. I used `metasploit` to exploit this vulnerability as follows.

![exploitation1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2022.55.35.png)

![exploitation2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2022.55.46.png)

![exploitation3](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2022.56.05.png)

![exploitation4](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2022.56.16.png)

Set rhosts(target IP address) and then ran the payload

![exploitation5](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2022.56.27.png)

![exploitation6](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2023.28.00.png)

![exploitation7](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2023.49.07.png)

I used `shell` command to convert meterpreter session into a standard shell and then `python -c` to spawn an interactive shell.

And then I attempted to list all files with the SUID bit set.

`find / -perm /4000 -exec ls -al {} \; 2>/dev/null`

- `find /`: Starts searching from the root directory.
- `perm /4000`: Finds files with the SUID bit set.
- `exec ls -al {} \;`: Executes `ls -al` on each found file. `{}` is a placeholder for the found file, and `\;` indicates the end of the `-exec` command.
- `2>/dev/null`: Redirects error messages to `/dev/null` to keep the output clean.

![suidFile](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2023.33.41.png)

`php7.3` was somewhat different from what I checked out different target machines before.

So I made a decision to use `gfobins` in order to exploit `php` for suid. Fortunately, I found the way to exploit it for privilege escalation.

![gfobins](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2023.59.49.png)

![gfobins2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2023.59.58.png)

Let's begin to exploit it for getting root.

![successExploitation1](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2022.59.50.png)

Success!

![successExploitation2](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2023.00.35.png)

I could read the final `flag.txt`

### What is virtual host routing?

This concept is to embrace more than one web site on one system or web server. For example, `www.example1.com` and `www.example2.com` can both be hosted on the same server.

![successExploitation3](../assets/img/blackpearl/Screenshot%202024-07-12%20at%2023.01.37.png)
