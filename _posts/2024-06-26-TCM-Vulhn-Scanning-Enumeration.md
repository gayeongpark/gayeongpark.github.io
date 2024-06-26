---
layout: post
title: TCM - practice for Kioptrix Lab
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through Kioptrix lab (level1)
tags: [ethical hacking, tcm, pjpt, kiotrix, utm, level1]
comments: true
author: Lantana Park
---

# Kioptrix Lab

As the UTM user, it was really hard to install kioptrix lab in my utm machine. Thankfully, TCM provided `.7z` converted file for the UTM users. I could just follow the given instruction from TCM discord.

1. Downloaded `Kioptrix_utm.7z`

   ![download](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.25.03.png)

2. Extracted the contents of this compressed file. `7zz x Kioptrix_utm.7z`

   ![decompressed](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.17.12.png)

3. Installed the decompressed file on my UTM machine

   ![install](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.29.38.png)

4. Run this machine and then test the network connection using `ping 8.8.8.8` (google dns ip address)

   ![test](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.52.38.png)

5. While running up on the Kioptrix lab, I found the lab's ip address on my kali machine and then ready to attack with port scanning.

   discovering lab's networking

   `netdiscover -r 192.168.64.0/24`

   ![labnetworking](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.52.55.png)

   Scanning my lab machine from Kali

   `nmap -T4 -p- -A 192.168.64.15`

   ![scanning1](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.53.07.png)

   ![scanning2](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2022.53.18.png)

   ![scanning3](../assets/img/kioptrix/Screenshot%202024-06-26%20at%2023.16.56.png)
