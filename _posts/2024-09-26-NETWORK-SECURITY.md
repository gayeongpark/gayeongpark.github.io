---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - network security fundamentals
tags: [network, compTia, fundamentals, security]
comments: true
author: Lantana Park
---

# Network Security Fundamental

## The CIA Triad

- Confidentiality : Concerned with keeping data safe and private. To do this, I can use either symmetric encryption and asymmetric encryption.

  - Symmetric encryption : Both the sender and receiver use the exact same key to encrypt/decrypt the message. Even though it is faster than the asymmetric encryption, symmetric encryption faces a key distribution challenge, requiring secure sharing of the key among users that need it.

  - Asymmetric encryption : Two different keys are used to give confidentiality, one for the sender, and one for the receiver. RSA is by far the most popular implementation of this. It has public key and private key. Receiver generates a key pair: a public key and a private key. Receiver shares their public key with others (like the sender). Sender encrypts the message using the receiver’s public key. Only the receiver can decrypt the message with their private key (which is kept secret). It is really slow.

    - Public Key infrastructure (PKI) encrypts information and facilitates key exchange using asymmetric encryption like RSA.

- Integrity : Ensures that the data was not modified in storage or in transit verifying the original source. This will help us prevent forms of spoofing like IP spoofing, ARP spoofing, or Mac spoofing. To ensure the integrity, hashing can be commonly used. Matching of the hash sent and the hash received means there was integrity in the transmission.

- Availability : Measures data accessibility. Availability could be compromised by different things: crashing the router by sending improperly formatted data (Ping of Death attack), Flooding the network (DoS and DDoS attacks), Having power outages, or using old routers and switches that may dies of old age.

## Threats and Vulnerabilities

A threat is a person or an event that has the potential for impacting a valuable resource in a negative manner. Hacker can be a threat.

A vulnerability is a quality or characteristic within a given resource or environment that might allow the threat to be realized.

### Threats come in two basic varieties

- Internal threat : Any threat that originates within the organization itself

- External threat : Any threat that could be people like a hacker, or it can be an event or environmental condition

### Types of vulnerabilities

- Environmental vulnerabilities : Undesirable conditions or weaknesses that are in the general area surrounding the building where a network is run

- Physical Vulnerabilities : Undesirable conditions or weaknesses in the buildings where a network is run

- Operational Vulnerabilities : Focuses on how the network and its systems are run from the perspective of an organization's policies and procedures

- Technical Vulnerabilities : System-specific conditions that create security weaknesses

  - CVE (Common Vulnerabilities and Exposure) is a list of publicly disclosed computer security weaknesses

  - Zero-day vulnerabilities is any weakness in the system design, implementation, software code, or a lack of preventive mechanisms within a network that is unknown at the time of publication

## Risk Management

Risk Management is the identification, evaluation, and prioritization of risks to minimize, monitor, and control the vulnerability exploited by a threat.

Risk Assessment is the process that identifies potential hazards and analyzes what could happen if a hazard occurs.

- Security Risk Assessment : Used to identify, assess, and implement key security controls within an application, system, or network.

- Threat Assessment : Focused on the identification of the different threats to attack or cause harm to the systems or network. (MITRE attack framework)

- Vulnerability Assessment : Focused on identifying, quantifying, and prioritizing the risks and vulnerabilities in a system or network. (vulnerability scanners - Nessus, QualysGuard, OpenVAS)

- Penetration Test : Evaluates the security of an IT infrastructure by safely trying to exploit vulnerabilities within the systems or network

- Posture Assessment : Used to assess the organization's attack surface. Define mission-critical components, identify strengths, weaknesses, and security issues, strengthen position and stay in control

- Business Risk Assessment : Used to identify, understand, and evaluate potential hazards in the workplace

  - Process Assessment : Disciplined examination of the processes used by the organization against a set of criteria

  - Vendor Assessment : Assessment of a prospective vendor to determine if they can effectively meet the obligations and the needs of the business

## Audits and Compliance

Organizations are now required to follow new and different standards and regulations based on the locality of your data.

Data locality refers to the geographic location where data is stored and processed.

- Payment Card Industry Data Security Standard (PCI DSS) is a set of security standards designed to ensure that all companies that accept, process, store, or transmit credit card information maintain a secure environment. When designing an enterprise network, ensure that it is designed to segment and protect cardholder data environments.

- General Data Protection Regulation (GDPR) is a regulation or law created by the EU that is focused on data protection and privacy in the EU/EEA.

Auditing and compliance is not a one-time activity, it is rather an ongoing process.

- Monitoring and auditing program
- Regular audits
- Employee training
- Policies and procedures

## Device Hardening

Device Hardening refers to securing devices by reducing their attack surface, which involves:

- Disabling unnecessary applications, services, and ports.
- Running only necessary services to minimize potential vulnerabilities.
- Installing monitoring software for malware protection and intrusion detection.
- Establishing regular maintenance schedules for patching and updates.

Endpoints (servers, mobile devices, network infrastructure) can all be hardened to reduce the risk of attack.

Key practices include:

1. Security Software: Install endpoint security software like anti-malware, host-based firewalls, and log collection agents.
2. Specialized Hardware: Use hardware security features like UEFI, TPM, and HSM.
3. Software & Port Management:
   - Patch all software regularly.
   - Disable unnecessary services, ports, and accounts.
   - Restrict external devices and rename default accounts.
4. Standardization: Implement standardized security baselines and apply group policies.
5. Network Interfaces: Disable any unused network interfaces.
6. Port Monitoring: Close unused ports and use host-based firewalls. Some servers may run services on non-standard ports.
7. Disk Encryption: Enable full-disk encryption to protect stored data.
8. Account Review: Regularly review and disable/delete unnecessary accounts.
9. Lifecycle Considerations: Track End of Life (EOL) and End of Support (EOS) dates for software, hardware, and operating systems to ensure they receive security updates and patches.

## Physical Security

Physical security is crucial for network security. If an attacker gains physical access to your networking equipment (routers, switches, firewalls), they can alter configurations or bypass controls.

### Detection Mechanisms

Detection mechanisms identify and log potential security breaches after they occur but do not prevent them. Examples include:

- Cameras: Monitored or recorded, placed at entrances/exits of data centers, closets, and parking lots. Cameras can be wired or wireless (potential for signal interference).
- Infrared Cameras: Detect heat signatures to track intruders or identify overheating equipment.
- Ultrasonic Cameras: Use sound to detect movements, such as in "Mission Impossible" movies.
- Motion Detectors, Asset Tags, Tamper Detection: Help monitor equipment and environments for unauthorized access or movement.

### Prevention Mechanisms

Prevention mechanisms stop security breaches before they happen. These include:

- Access Control Hardware: Badge readers (magnetic strips, chip cards, RFID) and biometric readers (fingerprint, retina scan) often combined with a PIN for two-factor authentication.
- Access Control Vestibules: Secure areas between doors where individuals are authenticated before access is granted.
- Smart Lockers: Secure storage for personal electronic devices (phones, laptops) to prevent unauthorized data capture.
- Locking Racks/Cabinets: Protect equipment in data centers by physically restricting access.
- Employee Training: The most valuable prevention tool, focusing on cybersecurity awareness to reduce user and administrator errors, phishing prevention, and enforcing security policies.

## Honeypots and Active Defense

Honeypots are systems set up to lure attackers away from valuable assets, allowing defenders to observe their methods and learn from them. Honeynets are larger networks used for similar purposes, often employed by security researchers to study attackers' techniques and gain insights for attribution.

In addition to honeypots and honeynets, active defense can include strategies like obfuscation (e.g., fake DNS entries or web server with decoy directories, port triggering and spoofing) to waste attackers' time. Another concept discussed is hack back, where defenders counterattack an adversary. However, hack back is legally complex and not recommended for most organizations due to potential legal ramifications.
