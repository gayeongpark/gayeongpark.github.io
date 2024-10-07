---
layout: post
title: CompTia network+ certification
subtitle: Preparing for CompTia network+ - logical security
tags: [network, compTia, fundamentals, attacks, logical security]
comments: true
author: Lantana Park
---

# Logical Security

Logical Security refers to the non-physical measures implemented to protect digital data, restrict unauthorized access, and ensure data integrity and confidentiality.

## Identity and Access Management (IAM)

Identity and Access Management (IAM) is a security process that provides identification, authentication, and authorization mechanisms for users and computers.

When I log into a computer with a username and password, I am participating in IAM by authenticating myself and gaining authorization to access resources.

### Unique Subjects in IAM

- Personnel: Users like employees, the most common IAM subjects. However, they pose risks when handling credentials insecurely (e.g., writing down passwords).
- Endpoints: Devices like desktops, laptops, phones, and tablets that connect to networks. These devices also have their own IAM credentials.
- Servers: Unlike endpoints, servers often handle machine-to-machine communication and have their own IAM credentials for securing critical systems.
- Software: Applications also interact with IAM, typically via digital certificates.
- Roles: These define permissions for assets like servers, people, or endpoints based on their functions. Roles group assets into permission sets, often implemented in systems like Windows via group-based access.

### IAM Tasks

- Provisioning/Deprovisioning Accounts: Creating and deleting user accounts.
- Managing Accounts: Resetting passwords, updating certificates, and managing permissions.
- Auditing: Monitoring account activities to ensure legitimacy.
- Identity-Based Threat Evaluation: Ensuring security by checking for weak passwords and preventing unauthorized access.
- Maintaining Compliance: Ensuring the system follows security guidelines through audits and checks.

### IAM Risks

- User Accounts: Standard accounts with basic permissions, posing moderate risk.
- Privileged Accounts: Admin or superuser accounts with higher permissions, posing significant risk and requiring extra scrutiny.
- Shared Accounts: Often used in small setups, shared accounts are risky as they prevent identifying specific users, making accountability and auditing difficult. It's recommended to avoid shared accounts.

## Multi-factor Authentication

Multi-factor Authentication means that people authenticate or prove an identity using more than one method. o qualify as MFA, at least two different factors must be used, chosen from the following categories:

1. Something You Know (Knowledge Factor): This includes passwords, PINs, or answers to security questions. Using only knowledge factors like a username and password is single-factor authentication, not MFA.

2. Something You Have (Possession Factor): Physical objects like smart cards, key fobs, or RFID badges fall into this category. They provide added security when combined with knowledge factors (e.g., a smart card + PIN).

3. Something You Are (Inherence Factor): Biometrics, such as fingerprints, retina scans, or voice recognition, are part of this category. These are unique physical traits but are less commonly used in everyday systems due to intrusiveness.

4. Something You Do (Action Factor): This includes behaviors like signing my name, performing a gesture, or typing patterns. Though it’s a less common factor, it can add security when combined with others.

5. Somewhere You Are (Location Factor): This factor uses location-based controls, often involving geotagging or geofencing. Systems can check the user’s GPS location to verify their identity or restrict access based on geographic boundaries.

- Password Weaknesses: Passwords alone are vulnerable to common issues like unchanged default credentials, weak or common passwords (e.g., "password"), and attacks like dictionary, brute force, and hybrid attacks. Using long, complex passwords (12+ characters) with a mix of uppercase, lowercase, numbers, and special characters can improve password security.

- Authentication Methods & Security Considerations: MFA is essential because relying on passwords alone provides weak security. The combination of factors enhances security, making it harder for attackers to compromise systems, even if one factor is breached.

## Authentication Methods

Authentication is the process of verifying the identity of a user or device. Various methods are employed to ensure secure access,

1. Local Authentication: A common method where a user logs in with a username and password stored on a local device. The credentials are encrypted and compared with stored data for verification.

2. LDAP (Lightweight Directory Access Protocol): Centralizes network authentication by maintaining a hierarchical directory of users, groups, and resources. LDAP uses port 389 (or 636 for secure LDAPS) to validate login credentials across platforms like Linux, Mac, and Windows. Microsoft's Active Directory is an LDAP implementation used in Windows environments.

3. Kerberos: A ticket-based protocol used in Windows domains. It avoids sending passwords over the network, instead relying on tickets issued by the Key Distribution Center (KDC). Port 88 is used for communication. Kerberos provides mutual authentication but can become a single point of failure if the KDC goes down. To prevent that, most people will have both a primary and a secondary domain controller in a clustered or active-standby configuration.

4. Single Sign-On (SSO): Allows users to authenticate once and access multiple services. SSO reduces the need for multiple credentials but increases risk if the primary credentials are compromised. SSO often integrates with multi-factor authentication to enhance security.

5. SAML (Security Assertion Markup Language): An XML-based format used to exchange authentication data between a client and a service. SAML is widely used for federated identity management and single sign-on, allowing users to authenticate through a trusted identity provider (e.g., Google) without sharing credentials with the service provider.

6. RADIUS (Remote Authentication Dial-In User Service): Centralizes administration for VPN, dial-up, and wireless authentication. It uses UDP for communication, typically on ports 1812 (authentication) and 1813 (accounting). RADIUS is cross-platform and supports multiple authentication methods like EAP. It does not support all protocols.

7. TACACS+ (Terminal Access Controller Access-Control System Plus): A Cisco-proprietary protocol that operates over TCP. It separates authentication, authorization, and accounting (AAA) and supports all major network protocols, but it’s slower compared to RADIUS and mainly used in Cisco-only environments. It can provide some additional security features and supports all protocols.

8. Time-Based Authentication (TOTP): Generates temporary, one-time passwords that expire after a short time, typically 30 or 60 seconds. This is used in multi-factor authentication (MFA), providing extra security by ensuring even intercepted passwords are unusable after expiration. Examples include Google/Microsoft Authenticator and RSA Key Fobs/YubiKey.

## Security Principles

1.  Least Privilege : Using the lowest level of permissions or privileges needed in order to complete a job or admin task. Systems and networks need to be designed with the concept of least privilege.

    ### Application

    - User Accounts: Regular tasks (e.g., checking email) are performed with standard user accounts without administrative privileges. Administrative tasks (e.g., installing software) require logging in with elevated privileges.
    - System Design: Devices and services (e.g., IoT devices like LED lights) should have limited access, restricted to only necessary ports and services. For instance, IoT devices might only need internet access for firmware updates and specific ports for communication, but not access to file servers or printers.

    ### Benefits

    - Reduces the risk of accidental or malicious system changes.
    - Limits the potential damage from compromised accounts.

2.  Access Control Models

    - Discretionary Access Control (DAC):

      - Resource owners set access permissions for files or objects.

      - Challenges: Each object must have an owner, and the owner must set appropriate permissions.

    - Mandatory Access Control (MAC):

      - The system enforces access control using data labels that assign trust levels to users and objects.

      - Commonly used in military systems, where documents and users have clearance levels (e.g., Top Secret, Confidential). MAC is not used in most enterprise networks and is reserved only for highly classified information within military systems.

      - Users need both sufficient clearance and a "need to know" to access certain data.

    - Role-Based Access Control (RBAC)

      - Access is based on roles rather than individual permissions.

      - Roles are assigned to job functions (e.g., IT, HR, Sales), and users in each role inherit permissions based on their group.

      - Simplifies managing permissions and enforces the principle of least privilege. Creating groups makes it easy to control permissions based around actual job functions.

      - Example: Windows “Power Users” group has more permissions than regular users but less than administrators.

## Encryption

Data Encryption is a proven method for securing information, encryption encodes data, making it unreadable without the proper decryption key. It helps mitigate risks, even if access controls fail, ensuring confidentiality.

### Data can exist in three states

- Data at Rest: Stored data on devices like hard drives or memory. Encryption (e.g., full disk, file-level, or database encryption) protects this data.
- Data in Transit: Data moving across networks or within systems (e.g., over the internet or between devices). Encryption protocols such as TLS, SSL, IPSec, or WPA2 secure this data.
- Data in Use/Processing: Data actively being processed by a system (in CPU or RAM). It’s temporary and used during tasks like encryption, decryption, and other operations.

- Encryption protects the confidentiality of data in each of these states, safeguarding it from unauthorized access throughout its lifecycle. Systems like processors (Intel/AMD) enhance security during data processing.

## Internet Protocol Security (IPSec)

IPSec is a secure network protocol suite used to provide encrypted and authenticated communication over an IP network, primarily for VPNs (Virtual Private Networks). It ensures confidentiality, integrity, authentication, and anti-replay during data transmission, and supports both site-to-site and client-to-site VPNs.

### Key Concepts

- Confidentiality: Achieved through data encryption.
- Integrity: Ensures data is not modified in transit by using hash verification.
- Authentication: Verifies identities of the communicating parties.
- Anti-replay: Prevents replay attacks by checking packet sequence numbers.

### Five Main Steps of IPSec Tunnel Establishment

1. Key Exchange Request: Initiates a VPN connection.
2. IKE Phase 1: Authenticates peers and establishes a secure channel using Diffie-Hellman key exchange. This can happen via main mode (three exchanges for higher security) or aggressive mode (faster but less secure).
3. IKE Phase 2: Negotiates IPSec Security Associations (SAs) and establishes the secure tunnel for data transfer.
4. Data Transfer: Encrypted data transmission occurs using the parameters set in Phase 2.
5. Tunnel Termination: The tunnel ends when SAs are deleted or expire.

### Modes of Operation to allow the data transfer

- Transport Mode: Used in client-to-site VPNs, uses the original packet header and minimizes packet size.

- Tunnel Mode: Used in site-to-site VPNs, encapsulates the entire packet with a new header, which increases its size.

- The Diffie-Hellman Key Exchange is used to securely share secret keys between peers without prior knowledge of each other. This shared secret key is used to establish a secure communication tunnel.

### Real IPSec Application example

1. PC1 sends traffic to PC2 and then RTR1 (Router1) initiates creation of IPSec tunnel

2. RTR1 and RTR2 negotiate Security Association (SA) to form IKE Phase 1 tunnel (ISAKMP tunnel)

3. IKE Phase 2 tunnel (IPSec tunnel) is negotiated and set up

4. Tunnel is established and information is securely sent between PC1 and PC2

5. IPSec tunnel is torn down and the IPSec SA is deleted

### Additional Protocols

- Authentication Header (AH) : Provides data integrity and origin authentication, protecting against replay attacks.

- Encapsulating Security Payload (ESP) : Adds encryption for data confidentiality along with integrity and authentication.

## Public Key Infrastructure (PKI)

Public Key Infrastructure (PKI) is a comprehensive system designed to manage public and private keys, enabling secure data exchange through asymmetric encryption. It consists of hardware, software, policies, procedures, and people, ensuring secure communications, such as when connecting to HTTPS websites.

1. HTTPS Connection : When I visit a secure website, like `https://google.com`, my web browser communicates with a certificate authority (CA), which provides the server's public key. The browser then creates a shared secret key (used for symmetric encryption) and securely sends it to the web server using the server’s public key.

2. Asymmetric and Symmetric Encryption

   - Asymmetric encryption : Involves a pair of keys (public and private). The browser encrypts the shared secret with the server’s public key, which only the server can decrypt with its private key. This ensures secure key exchange.

   - Symmetric encryption : Once both the browser and server share the secret key, they use it to create a secure tunnel (using algorithms like AES) for encrypted data transmission.

3. Authentication and Confidentiality

   - Authentication : Ensures that the server is who it claims to be (e.g., google.com), thanks to the digital certificate issued by a trusted CA.

   - Confidentiality : Ensures only the intended parties (browser and server) can read the data transferred via the encrypted tunnel.

4. Public Key Infrastructure vs. Public Key Cryptography

   - Public Key Cryptography refers to the process of encryption and decryption using asymmetric keys.

   - PKI is a broader system encompassing key management, certificate issuance, validation, and the entire process of securing communications.

5. Certificate Authority (CA) : The trusted third party responsible for issuing digital certificates, verifying the authenticity of the public key, and maintaining global trust among CAs.

6. Key Escrow : A secure method of storing encryption keys with a third party, allowing retrieval in cases where keys are lost or needed for legal investigations. While key escrow is beneficial, it introduces security risks since unauthorized access to the escrow keys could compromise large amounts of data.

7. Security Considerations : PKI provides an essential framework for secure communication, but its components, especially key escrow, must be managed with stringent security measures to prevent unauthorized access.

## Digital Certificates

Digital Certificate : A digitally-signed electronic document that binds a public key with a user's identity (can be a person, server, or device). Commonly follows the X.509 standard in PKI (Public Key Infrastructure).

### Types of Certificates

1. Wildcard Certificate

   - Allows all subdomains to use the same certificate.

     - Pros: Cost-effective and easy to manage for multiple subdomains.
     - Cons: If compromised, all subdomains are affected.

2. Single-Sided Certificate

   - Only one party (usually the server) is authenticated.

3. Dual-Sided Certificate

   - Both the server and the client must authenticate each other using certificates, enhancing security but requiring more processing power.

4. Self-Signed Certificate

   - Signed by the entity itself, not by a trusted third party (CA).
   - Used mainly for testing or in closed systems.

5. Third-Party Certificate

   - Issued and signed by a trusted certificate authority (CA) like Verisign or Digi-sign.
   - Embedded in browsers for automatic trust validation.

6. Subject Alternative Name (SAN)

   - Field in a certificate that allows it to cover multiple domains, unlike a wildcard which covers only subdomains.

### Key Concepts

- Root of Trust: The foundational concept where each certificate can be validated using the concept of a root of trust or the chain of trust.

- Certificate Authority (CA) : Trusted third party that issues certificates, containing a digital signature, serial number, and expiration date.

- Registration Authority (RA) : Handles certificate requests and forwards them to the CA for issuance.

- Certificate Signing Request (CSR) : An encoded request from a user or entity to obtain a certificate from a CA. Contains details like the public key, organization, and domain.

- Certificate Revocation List (CRL) : A list maintained by CAs that tracks revoked certificates (e.g., due to compromise).

- Key Escrow Agent : Stores a secure copy of private keys to prevent data loss.

- Key Recovery Agent : Specialized software for restoring lost or corrupted keys, especially in disaster recovery scenarios.

ECC is favored when I am using mobile and low power devices, RSA is favored when I am using desktops.

## Key Management

Key management refers to how an organization will generate, exchange, store, and use encryption keys.

1. Key Generation : The process of creating strong encryption keys. Often, this is user-generated through passwords, which must be strong to ensure encryption strength.

2. Key Exchange : Securely sharing encryption keys, typically using asymmetric encryption methods (like Diffie-Hellman) to encrypt symmetric keys for transmission. Used in systems like VPNs, SSL, and TLS connections.

3. Key Storage : Keys must be securely stored to prevent unauthorized access. If a key is exposed, it can be used to decrypt sensitive information.

4. Key Rotation : Periodically changing encryption keys enhances security. By rotating keys, I need to reset the potential attack timeline, reducing the risk of long-term attacks.

These steps ensure encryption remains effective, preventing attackers from accessing sensitive information even if they intercept or discover a key.
