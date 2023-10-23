---
description: Networking Basics
---

# 💻 Networking

This is my notes on networking, covering the basics and details that I feel most everyone should grasp and understand. Such as the [OSI Model](osi-model.md) - [TCP/IP Model](tcp-ip-model.md) - [Common Ports and Protocols](common-ports-and-protocols.md) - and [Subnetting](subnetting.md)

## IPv4

Pv4 (Internet Protocol Version 4) is the fourth revision of the Internet Protocol (IP) used to to identify devices on a network through an addressing system. The Internet Protocol is designed for use in interconnected systems of packet-switched computer communication networks. IPv4 is the most widely deployed Internet protocol used to connect devices to the Internet. IPv4 uses a 32-bit address scheme allowing for a total of 2^32 addresses (just over 4 billion addresses). With the growth of the Internet it is expected that the number of unused IPv4 addresses will eventually run out because every device that connects to the Internet requires an address.

IP addresses are made up of 4 octets. An octet is made up of 8bits. 8bits is 1byte, so an IP address is 32bits, or 8bytes

00000000.00000000.00000000.00000000 is 32bits

Decimal Value: 128 64 32 16 8 4 2 1 = 255 Binary Value: 1 1 1 1 1 1 1 1 = 255 Add for each 1 in the binary value, add the decimal value to get the octet. Eg1. 00000111.00000111.00000111.00000111 = 7.7.7.7 Eg2. 11000000.10101000.00000001.01010100= 192.168.1.84

Private IP Ranges:

* **Class A:** 10.0.0.0 - 10.255.255.255 / **Subnet:** 255.0.0.0
* **Class B:** 172.16.0.0 - 172.16.31.0 / **Subnet:** 255.255.0.0
* **Class C:** 192.168.0.0 - 192.168.255.255 / **Subnet:** 255.255.255.0

NAT = Network Address Translation

**APIPA** is short for Automatic Private IP Addressing, a feature of Windows operating systems, meant for non-routed small business environments, usually less than 25 clients. With APIPA, DHCP clients can automatically self-configure an IP address and subnet mask when a DHCP server isn't available. When a DHCP client boots up, it first looks for a DHCP server in order to obtain an IP address and subnet mask. f the client is unable to find the information, it uses APIPA to automatically configure itself with an IP address. The IP address range is 169.254.0.1 through 169.254.255.254. The client also configures itself with a default class B subnet mask of 255.255.0.0. A client uses the self-configured IP address until a DHCP server becomes available. The APIPA service also checks regularly for the presence of a DHCP server (every five minutes, according to Microsoft). If it detects a DHCP server on the network, APIPA stops, and the DHCP server replaces the APIPA networking addresses with dynamically assigned addresses.

**A Loopback address** is an address that sends outgoing signals back to the same computer for testing. In a TCP/IP network, the loopback IP address is 127.0.0.1, and pinging this address will always return a reply unless the firewall prevents it. The loopback address allows someone to treat the local machine as if it were a remote machine.

## IPv6

A new Internet addressing system Internet Protocol version 6 (IPv6) is being deployed to fulfill the need for more Internet addresses. IPv6 (Internet Protocol Version 6) is also called IPng (Internet Protocol next generation) and it is the newest version of the Internet Protocol (IP) reviewed in the IETF standards committees to replace the current version of IPv4 (Internet Protocol Version 4). IPv6 is the successor to Internet Protocol Version 4 (IPv4). It was designed as an evolutionary upgrade to the Internet Protocol and will, in fact, coexist with the older IPv4 for some time. IPv6 is designed to allow the Internet to grow steadily, both in terms of the number of hosts connected and the total amount of data traffic transmitted. IPv6 is often referred to as the "next generation" Internet standard and has been under development now since the mid-1990s. IPv6 was born out of concern that the demand for IP addresses would exceed the available supply.

IPv6 is made up of 128bits and are written in groups of 4 hexadecimal digits separated by colons. Eg **2607:f0d0:1002:51::4** which is also **2607:f0d0:1002:0051:0000:0000:0000:0004**. They are divided into 2 parts, a 64bit network prefix, and a 64bit interface identifier.

There is no need to write the leading zeros. Leading zeros can be dropped: **2345:0425:2CA1:0000:0000:0567:5673:23b5** goes to **2345:425:2CA1:0000:0000:567:5673:23b5**

If we have an entire field of zeros we can use only one 0 for each colon: **2345:0425:2CA1:0000:0000:0567:5673:23b5** goes to **2345:0425:2CA1:0:0:0567:5673:23b5**

If we have a set of contiguous zero fields we can use double colons(::). Double colon can be used only one time in an IPv6 Address Example. **2345:0425:2CA1:0000:0000:0567:5673:23b5** goes to **2345:0425:2CA1::0567:5673:23b5**

* Unicast addresses – used to identify each network interface.
* Anycast addresses – used to identify a group of interfaces at different locations.
* Multicast addresses – used to deliver one packet to many interfaces.

IPv6 does not support the broadcast method. Some IPv6 addresses are used for special purposes, such as the address for loopback which look like **::1/128**

## MAC Addresses

A MAC (Media Access Control) address is a unique identifier assigned to network interface controllers (NICs) of network devices. It is a hardware address that is permanently assigned by the manufacturer and is stored in the device's firmware or read-only memory (ROM). MAC addresses are used at the data link layer (layer 2) of the OSI model to ensure that data is delivered to the correct device within a local network.

MAC addresses are typically 48 bits in length and are a sequence of six pairs of hexadecimal digits separated by colons or hyphens. Eg. The mac address "00:1A:2B:3C:4D:5E", the first three pairs of digits identify the manufacturer of the NIC, in this case, 00:1A:2B belongs to Ayecom Technology Co., Ltd. While the last three pairs provide a unique identifier for the specific device.

MAC addresses allow devices to communicate with each other within a local area network (LAN). When data is sent from one device to another on the same network, it is encapsulated within Ethernet frames that contain the source and destination MAC addresses. Routers and switches use these MAC addresses to forward the data to the appropriate destination.

It's important to note that MAC addresses are specific to a LAN, and do not have global uniqueness like IP addresses. When data needs to be transmitted outside the LAN, it is encapsulated in network packets that contain source and destination IP addresses.

In summary, a MAC address is a unique identifier assigned to the network interface controller of a device. It is used at the data link layer to facilitate communication within a local network. MAC addresses are hardware-based, manufacturer-specific, and differ from IP addresses, which are used for network communication on a larger scale.

