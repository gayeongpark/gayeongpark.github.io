---
layout: post
title: TCM - networking refresher (security)
subtitle: Preparing for PJPT (Practical Junior Penetration Tester) certification
tags: [ethical hacking, tcm, pjpt, ip address]
comments: true
author: Lantana Park
---

# Networking Refresher

## IP addresses

### What is an IP address?

IP addresses (logical addresses) are the numbers assigned to the every device on the computer networking. It is used to identify the communication across the internet. And also it is utilized to identify and locate devices on a network.

### How the IP address is structured?

There are main two versions of the internet protocols: **IPv4(Internet Protocol version 4)** and **IPv6(Internet Protocol version 6)**

**IPv4** is often referred to as "**inet**", which is shorthand for "**Internet**".

It is 32-bit and separated by a dot (.)(Dot-decimal notation).

For example,

`192.168.1.1`
= `11000000.10101000.00000001.00000001`

128 | 64 | 32 | 16 | 8 | 4 | 2 | 1
1 | 1 | 0 | 0 | 0 | 0 | 0 | 0

= 128 + 64 = 192

Binary (Base2) to Decimal(Base10)

**IPv6** is often referred to as "**inet6**"

It is 128-bit and separated by a clone (clone-hexadecimal notation)

For instance,

`2001:0db8:85a3:0000:0000:8a2e:0370:7334`
= `0010 0000 0000 0001 0000 0011 0110 1110 0000 0001 0110 1000 1100 0000 1100 0000 0000 0000 0000 0000 0000 0000 0000 0000 1000 1010 0010 1110 0000 0000 1101 1100 0000 0000 1110 0110 0110 0101 0011 0100`

Binary (Base2) to Hexadecimal (Base16)

More rules on it,

omitting leading zeros within a group and representing consecutive groups of zeros with a double colon `(::)`.

step1: `2001:db8:0:0:8a2e:370:7334:0`
step2: `2001:db8::8a2e:370:7334:0`

![table](/gayeongpark.github.io/assets/img/PJPT/hex-table.webp)

### Types of IP address

The different version of ip addresses (IPv4 and IPv6) can be divided into public and private ip addresses.

**Public IP addresses** are assigned to a device by the internet service provider (ISP)

**Private IP addresses** are assigned to devices on a private network, such as a home or office network

**Dynamic IP addresses change over time**. It can be used for devices such as computers, smartphones, and tablets, where a constant address is not necessary. And it is for devices that connect to a network temporarily, like guest devices or IoT devices, often use dynamic IP addresses.

### What is NAT

NAT is a method used by routers or servers to translate private, local IP addresses to a public IP address and vice versa.

This clever design, not only saves IPv4 addresses(because of the address limitation of IPv4) but also adds a layer of security by hiding the internal IP addresses of local devices from the internet.

NAT is not needed in IPv6 addresses because IPv6 has a vast address space. This allows direct communication between devices, simplifying networks and improving security.

![nat](../assets/img/PJPT/NAT-in-IPv6-03.png)

## MAC addresses

`MAC` (Media Access Control - physical address) address is identified under `ether`. It is usually fixed and cannot be changed unless the device’s network interface is replaced.

It address may look like `00:1A:2B:3C:4D:5E`. It allows devices to communicate with each other a local area network (LAN).
