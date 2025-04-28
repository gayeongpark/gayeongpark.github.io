---
layout: post
title: CyberDefenders - WebStrike Lab
subtitle: Solving network forensics lab in CyberDefenders CTF challenges
tags: [wireShark, pcap, analysis, webStrike, Zui(Brim), easy]
comments: true
author: Lantana Park
---

# WebStrike Lab

## Scenario

"A suspicious file was identifies on a company web server, raising alarms within the intranet. My goal is to uncover how the file appeared and determine the extent of any unauthorized activity"

![pcapFile](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2018.53.38.png)

### Questions

1. Identifying the geographical origin of the attack helps in implementing geo-blocking measures and analyzing threat intelligence. From which city did the attack originate?

   #### Answer : Tianjin

   I decided to view detailed information from all the entire packet entries

   ![maliciousConn1](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2018.56.36.png)

   ![maliciousConn2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2018.56.46.png)

   Since I was able to get the attacker's IP address, I searched for `117.11.88.124` on the VirusTotal.

   ![IdentifyIPaddress1](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2020.57.43.png)

   ![IdentifyIPaddress2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2020.58.04.png)

2. Knowing the attacker's User-Agent assists in creating robust filtering rules. What's the attacker's Full User-Agent?

   #### Answer : Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0

   Since the User-Agent is included in the `http` protocol communication. I went through the `http` path in Zui

   ![httpUser-Agent1](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2019.00.36.png)

   ![httpUser-Agent2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2019.00.44.png)

3. We need to determine if any vulnerabilities were exploited. What is the name of the malicious web shell that was successfully uploaded?

   #### Answer : image.jpg.php

   While reviewing the log entries, I identified that the attacker exploited a web vulnerability—likely a malicious file upload via `http` communication. The attacker uploaded a malicious `.php` file to the review directory, possibly to establish a reverse shell.

   - First attempt from attacker (Failed)
     ![failed](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2021.18.06.png)

   - Second attempt from attacker (Failed)
     ![failed2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2021.18.31.png)

   - Third attempt from attacker (Failed)
     ![failed3](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2021.31.01.png)

   - Fourth attempt from attacker (Success to access `/reviews/uploads/` and load the reverse shell)
     ![success1](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2021.28.42.png)

     ![success2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2021.34.26.png)

4. Identifying the directory where uploaded files are stored is crucial for locating the vulnerable page and removing any malicious files. Which directory is used by the website to store the uploaded files?

   #### Answer : /reviews/uploads/

   The malicious attacker uploaded `image.jpg.php` to the `/reviews/uploads/` directory using the `POST` method.
   ![successfulUpload](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2021.41.16.png)

5. Which port, opened on the attacker's machine, was targeted by the malicious web shell for establishing unauthorized outbound communication?

   #### Answer : 8080

   First I did go through `HTTP` stream, especially `POST` method

   First attempt (failed)

   ![firstHTTPStreamFilter1](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.02.41.png)

   ![firstHTTPStreamFilter2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.01.49.png)

   ![firstHTTPStreamFilter3](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.01.56.png)

   Second attempt (Success)

   ![secondHTTPStreamFilter1](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.02.51.png)

   ![secondHTTPStreamFilter2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.00.42.png)

   ![secondHTTPStreamFilter3](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.00.51.png)

6. Recognizing the significance of compromised data helps prioritize incident response actions. Which file was the attacker attempting to exfiltrate?

   #### Answer : passwd

   Luckily, the server responded with a `501` status code, preventing the attacker's request from being processed. The attacker had attempted to exfiltrate password data to their server.

   ![final1](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.14.15.png)

   ![final2](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.03.14.png)

   ![final3](../assets/img/WebStrike/Screenshot%202025-04-28%20at%2022.03.29.png)
