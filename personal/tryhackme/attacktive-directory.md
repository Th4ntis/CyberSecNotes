# Attacktive Directory

My walkthrough on the [Attacktive Directory room](https://tryhackme.com/room/attacktivedirectory). For this room we need to install [Impacket](../../general/attack-and-defense/impacket.md) and [Bloodhound](../../general/attack-and-defense/bloodhound.md).

## Task 3

Basic enumeration starts out with an **nmap scan**. [Nmap](../../general/networking/nmap.md) is a utility that can be used to detect what ports are open on a device, what services are running, and even detect what operating system is running.

![](<../../.gitbook/assets/image (1) (1) (2) (1).png>)

### Question 1: What tool will allow us to enumerate port 139/445?

Answer: _**enum4linux**_

_This answer came from previous knowledge of enumeration tools... and guessing._

### Question 2: What is the NetBIOS-Domain Name of the machine?

Answer: **THM-AD**

![](<../../.gitbook/assets/image (2) (2) (1) (1) (1).png>)

### Question 3: What invalid TLD do people commonly use for their Active Directory Domain?

Answer: **.local**

## Task 4

