---
title: "Nmap room 1: Host Discovery"
date: 26-12-2024
categories: [Network Security,Network Mapping,nmap]
tags: [nmap , TryHackMe]
description: "This is the first room of the 4 room nmap series created by tryhackme.com "
---

## Overview: 
In this room diffrent techniques to discover offline and online Network Hosts are discovered without the need to scan for open ports with the pwerful network mapping tool nmap. This technique is a crucial for stealth network scanning which is the base of passive recon. 

## 1. Subnetworks:
Here a small recap of what subnetworks are is discussed.
Subnets are the smallest group of a network. Every subnet is assigned a unique IP-Adress with a subnet mask which determines how many IP-Adresses are available in the subnetwork like 10.1.100.0/24 where:
- The subnetwork IP-Adress is 10.1.100.0 
- The subnet mask is 10.1.100.0/24 or 255.255.255.0 which means that 254 IP-Adresses are available.

![A Network Model](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/aa787518e856e0094cb40da8399be0f3.png)

## 2. Target Enumeration specifications
Some example specifications are given.
- Simple listin glike `nmap IP-Adress dmain-name domain-name` in this example  hosts are targeted
- Using the subnet mask like `nmap Network-Adress/30` where 4 IP-Adresses will be targeted.
_ Using a text file like `nmap -iL file.txt`

**note:** To list the hosts that nmap will scan without scanning them use: `nmap -iL list_of_hosts.txt`

## 3. Discovering Live Hosts 
Here the diffrent methods of scans are introduced and categorized through the TCP/IP layers:
- ARP from Link Layer
- ICMP from Network Layer
- TCP from Transport Layer
- UDP from Transport Layer


## 4. Host discovery using ARP:
Here the ARP protrocol method is used to discover active host in the same subnet as the scanning host because ARP is a **Link Layer** protocol.

### a. How it works?
The scanning host sends a ARP request to the target host if the target host sends a reply then it is live if not then it is offline.
### b. The corresponding command
To perform an ARP scan the following command is used:
`nmap -PR -sn TARGETS`
**note:** The -sn flag prevents nmap from performing a port scan. This type of scans is called a **ping scan**

## 5. Host discovery using ICMP:
Here the 3 diffrent ICMP scanning methods are discussed.
- ICMP Echo Request or ping (ICMP Type 8)
- ICMP Timestamp Request (ICMP Type 13)
- ICMP Adress Mask Request (ICMP TYPE 17)
### a. How it works?
The scanning host sends a ICMP request of any type to the target host if the target host sends a corresponding reply then it is live if not then it is offline.
### b. The corresponding command
To perform an ARP scan the following command is used:
    - `nmap -PE -sn TARGETS` for ping (ICMP Echo Request).
    - `nmap -PP -sn TARGETS` for ICMP Timestamp Request.
    - `nmap -PM -sn TARGETS` for ICMP Adress Mask Request.

## 6. Host Discovery using TCP:
**note:** This scan is a port scan! 

Here the TCP protocal is used as a scanning method.
There are two methods which strongly base on the TCP Handshake mechanism.
- Send a SYN packet. Here a priviliged user (root or a sudoer) can perform a semi handshake ie. sendonly a SYN without the need to send the ACK packet as a response to the ACK request SYN/ACK if recieved from the Target. A normal user must complete all of the 3-way handshake!
- Send an ACK packet. Only a priviliged user can perform this method

**note:** It is considerable to note that the ACK method is stealthier than the SYN method.

### a. How it works?
- Using the SYN method, the scanner starts the handshake through sending a SYN packet to PORT 80 by default. If the scanner recieves a SYN-ACK packet then it means that the host is alive and PORT 80 is open.
- Using the ACK method, the scanner sends an ACK packet to PORT 80. If he recieves a RST packet (Reset Packet meaning that the ACK packet is not part of any ongoing connection) then it means that the host is offline and that PORT 80 is closed. If it does not receive anything then the host is live and PORT 80 is open.

### b. The corresponding commands:
- `nmap -PS -sn TARGETS` for SYN packet method.
- `nmap -PA -sn TARGETS` for ACK packet method.

## 7. Host Discovery using UDP
Here the UDP protocol is used to scan for live hosts.

### a. How it works?
The scanner sends a UDP Packet to a UDP PORT of the target. The packet. If the scanner recieves a response (ICMP Type3: Destination unreachable).
then the PORT is **closed**, if he doesn't recieve anything then the host is up.
### b. The corresponding commands:
- `nmap -PU -sn TARGETS` 

