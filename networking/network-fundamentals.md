# Network Fundamentals

These are my notes on networking fundamentals - the addressing, core protocols, ports, and subnetting concepts that most everyone working in IT or security should understand. For how data actually moves through a network in layers, see the companion note on [Network Models](network-models.md) (OSI, TCP/IP, and the 3-way handshake).

**Contents**

* IPv4
* IPv6
* MAC Addresses
* Core Protocols: DHCP, DNS, ARP
* Common Ports and Protocols
* Subnetting

***

### IPv4

IPv4 (Internet Protocol version 4) is the fourth revision of the Internet Protocol and still the most widely deployed. It identifies devices on a network through an addressing system designed for packet-switched communication. IPv4 uses a **32-bit** address scheme, allowing for 2³² addresses - just over **4.29 billion**. Because every device that connects to the Internet needs an address, the pool of unused public IPv4 addresses has effectively been exhausted, which is one of the main reasons IPv6 was developed.

#### How an IPv4 address is structured

An IPv4 address is made up of **4 octets**. An octet is 8 bits, and 8 bits is 1 byte - so an address is 32 bits (4 bytes) total.

```
00000000.00000000.00000000.00000000   ← 32 bits
```

Each octet is read in binary using place values that double from right to left:

| Bit position  | 1   | 2  | 3  | 4  | 5 | 6 | 7 | 8 |
| ------------- | --- | -- | -- | -- | - | - | - | - |
| Decimal value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

For each `1` in the binary octet, add its decimal value. All eight bits set (`11111111`) equals 255, which is why octet values range from **0 to 255**.

* Example 1: `00000111.00000111.00000111.00000111` → `7.7.7.7`
* Example 2: `11000000.10101000.00000001.01010100` → `192.168.1.84`
  * `11000000` = 128 + 64 = **192**
  * `10101000` = 128 + 32 + 8 = **168**
  * `00000001` = **1**
  * `01010100` = 64 + 16 + 4 = **84**

#### Public vs. private addresses

Most networks use **private** address ranges internally and share a single **public** address to reach the Internet. The private ranges (defined in RFC 1918) are:

| Class | Range                         | Default subnet mask | CIDR |
| ----- | ----------------------------- | ------------------- | ---- |
| **A** | 10.0.0.0 – 10.255.255.255     | 255.0.0.0           | /8   |
| **B** | 172.16.0.0 – 172.31.255.255   | 255.255.0.0         | /16  |
| **C** | 192.168.0.0 – 192.168.255.255 | 255.255.255.0       | /24  |

> **Note:** the Class B private range runs all the way to `172.31.255.255`, not `172.16.31.0`.

#### NAT (Network Address Translation)

**NAT** is what lets many devices on a private network share one public IP address. The router rewrites the source address (and port) of outbound packets to its public address, keeps a translation table, and reverses the process on the way back. NAT is a major reason the IPv4 address shortage hasn't been more disruptive - an entire household or office can sit behind a single public address.

#### APIPA (Automatic Private IP Addressing)

**APIPA** is a Windows feature for non-routed small environments (typically fewer than \~25 clients). When a client boots, it first looks for a DHCP server to obtain an IP address and subnet mask. If none is found, APIPA automatically self-assigns an address from the range **169.254.0.1 – 169.254.255.254** with a default Class B mask of `255.255.0.0`. The client keeps checking for a DHCP server (roughly every five minutes); once one appears, the APIPA address is replaced by a properly assigned one. In practice, seeing a `169.254.x.x` address is a strong sign that **DHCP failed**.

#### Loopback address

The **loopback** address sends outgoing signals back to the same machine for testing. In IPv4 the loopback address is **127.0.0.1**, and pinging it will always return a reply unless a firewall blocks it. It lets you treat the local machine as if it were a remote host - useful for testing whether the TCP/IP stack itself is working.

***

### IPv6

IPv6 (Internet Protocol version 6, originally "IPng" - IP next generation) is the successor to IPv4, developed since the mid-1990s out of concern that IPv4 addresses would run out. It is an evolutionary upgrade designed to coexist with IPv4 and to let the Internet keep growing in both host count and traffic volume.

IPv6 uses **128-bit** addresses, written as **eight groups of 4 hexadecimal digits separated by colons**. An address is split into two halves: a **64-bit network prefix** and a **64-bit interface identifier**.

```
2607:f0d0:1002:0051:0000:0000:0000:0004
```

#### Shortening rules

IPv6 addresses can be abbreviated with three rules:

1. **Drop leading zeros** in any group:\
   `2345:0425:2CA1:0000:0000:0567:5673:23b5` → `2345:425:2CA1:0000:0000:567:5673:23b5`
2. **Collapse an all-zero group to a single `0`:**\
   `2345:0425:2CA1:0000:0000:0567:5673:23b5` → `2345:0425:2CA1:0:0:0567:5673:23b5`
3. **Replace one run of contiguous all-zero groups with `::`** - but only **once** per address:\
   `2345:0425:2CA1:0000:0000:0567:5673:23b5` → `2345:0425:2CA1::0567:5673:23b5`

So `2607:f0d0:1002:0051:0000:0000:0000:0004` compresses to `2607:f0d0:1002:51::4`.

#### Address types

IPv6 **does not use broadcast**. Instead it relies on three delivery methods:

* **Unicast** - identifies a single network interface (one-to-one).
* **Anycast** - identifies a group of interfaces, usually at different locations; the packet is delivered to the nearest one (one-to-nearest). Commonly used for services like DNS roots and CDNs.
* **Multicast** - delivers one packet to many interfaces at once (one-to-many). This replaces broadcast's role.

The IPv6 loopback address is **`::1/128`** (the equivalent of IPv4's `127.0.0.1`).

***

### MAC Addresses

A **MAC (Media Access Control) address** is a unique identifier assigned to a device's network interface controller (NIC). It is a hardware address, set by the manufacturer and stored in the device's firmware/ROM. MAC addresses operate at **Layer 2 (Data Link)** of the OSI model and ensure data reaches the correct device within a local network.

A MAC address is **48 bits**, written as six pairs of hexadecimal digits separated by colons or hyphens:

```
00:1A:2B:3C:4D:5E
└──┬───┘ └──┬───┘
  OUI     Device-specific
```

* The **first three pairs** (the OUI, _Organizationally Unique Identifier_) identify the manufacturer. Here, `00:1A:2B` belongs to Ayecom Technology Co., Ltd.
* The **last three pairs** uniquely identify the specific NIC.

When two devices communicate on the same LAN, the data is encapsulated in Ethernet frames carrying the **source and destination MAC addresses**, and switches use those addresses to forward frames to the right port.

MAC addresses are only meaningful **within a local network** - they are not globally routable the way IP addresses are. When traffic leaves the LAN, it's the **IP addresses** that route it across networks; the MAC addresses change hop-by-hop while the IP addresses stay the same end-to-end. Although burned in by the manufacturer, a MAC address can be **spoofed** (changed in software), which matters for both attacks and privacy.

***

### Core Protocols

These three protocols quietly make a local network usable: DHCP hands out addresses, DNS resolves names, and ARP maps IP addresses to hardware addresses.

#### DHCP (Dynamic Host Configuration Protocol)

[**DHCP**](https://www.fortinet.com/resources/cyberglossary/dynamic-host-configuration-protocol-dhcp) dynamically assigns IP addresses to devices on a network so they don't have to be configured by hand. Beyond the IP address, DHCP also hands out the **subnet mask**, **default gateway**, and **DNS server** addresses - everything a device needs to communicate on the network and reach the Internet.

The exchange follows the **DORA** process:

1. **Discover** - the client broadcasts, looking for a DHCP server.
2. **Offer** - a server responds with an available address.
3. **Request** - the client requests the offered address.
4. **Acknowledge** - the server confirms and leases the address.

DHCP runs on **UDP ports 67 (server) and 68 (client)**.

#### DNS (Domain Name System)

[**DNS**](https://www.fortinet.com/resources/cyberglossary/what-is-dns) translates human-friendly domain names into IP addresses. Every device on the Internet has an IP address, but people can't remember those, so DNS lets you type `google.com` instead of looking up its address. When you request a domain, a resolver walks the DNS hierarchy (root → top-level domain → authoritative server) to find the matching IP, then your device connects to it. DNS primarily uses **port 53**.

#### ARP (Address Resolution Protocol)

[**ARP**](https://www.fortinet.com/resources/cyberglossary/what-is-arp) maps an IP address to a fixed physical **MAC address** on a local network. When a device knows the destination IP but not the MAC, it broadcasts an ARP request ("who has 192.168.1.10?") and the owner replies with its MAC. The result is cached in an **ARP table** to avoid repeating the lookup.

> **ARP vs. DNS:** ARP matches an IP address to a MAC address _inside a LAN_. DNS matches a public IP address to a _domain name_ on the Internet.

**ARP Spoofing / ARP Poisoning**

**ARP spoofing** (also called ARP poisoning or ARP cache poisoning) is an attack in which an adversary sends forged ARP messages onto a LAN, associating **their** MAC address with the IP address of a legitimate device or gateway. Hosts then unknowingly send that traffic to the attacker instead of the real destination.

Because ARP has no built-in authentication, this is easy to pull off on a local segment and dangerous - sensitive data can pass through the attacker without the victim's knowledge. ARP spoofing is also the foundation for other attacks, including **Man-in-the-Middle (MITM)**, **Denial of Service (DoS)**, and **session hijacking**.

***

### Common Ports and Protocols

Ports identify which service a packet is destined for on a host. The combination of an IP address and a port (e.g. `192.168.1.10:443`) is a **socket**. Ports 0–1023 are the **well-known** ports listed below. See Network Models for where TCP and UDP sit in the stack.

#### Common TCP ports

| Port      | Protocol | Description                                        |
| --------- | -------- | -------------------------------------------------- |
| 21        | FTP      | File Transfer Protocol (control channel)           |
| 22        | SSH      | Secure Shell - encrypted remote login              |
| 23        | Telnet   | Remote login (unencrypted - legacy)                |
| 25        | SMTP     | Simple Mail Transfer Protocol (sending mail)       |
| 53        | DNS      | Domain Name System (also UDP)                      |
| 80        | HTTP     | HyperText Transfer Protocol                        |
| 110       | POP3     | Post Office Protocol v3 (retrieving mail)          |
| 139 / 445 | SMB      | Server Message Block / Samba (file sharing)        |
| 143       | IMAP     | Internet Message Access Protocol (retrieving mail) |
| 389       | LDAP     | Lightweight Directory Access Protocol (also UDP)   |
| 443       | HTTPS    | HTTP Secure (HTTP over TLS)                        |
| 990       | FTPS     | FTP over TLS/SSL                                   |
| 3306      | MySQL    | MySQL database                                     |
| 3389      | RDP      | Remote Desktop Protocol                            |

#### Common UDP ports

| Port    | Protocol | Description                                           |
| ------- | -------- | ----------------------------------------------------- |
| 53      | DNS      | Domain Name System (also TCP)                         |
| 67 / 68 | DHCP     | Dynamic Host Configuration Protocol (server / client) |
| 69      | TFTP     | Trivial File Transfer Protocol                        |
| 123     | NTP      | Network Time Protocol                                 |
| 161     | SNMP     | Simple Network Management Protocol                    |

> **Note:** Some ISPs (e.g. Comcast) block **port 25 (SMTP)** for residential and some commercial lines by default, so mail submission is often moved to **port 587**.

***

### Subnetting

**Subnetting** is the process of dividing a network into smaller "subnetworks" (subnets). It makes better use of IP address space and improves network management and routing. It's used mostly in IPv4 networks.

Subnetting works by **borrowing bits from the host portion** of an IP address to create a subnet identifier. By borrowing host bits, one network can be split into multiple subnets, each with its own range of addresses.

**Recommended resources:**

* [Professor Messer - "Seven-Second Subnetting"](https://www.youtube.com/watch?v=ZxAwQB8TZsM) (great starting point)
* [A Subnetting Guide](https://drive.google.com/file/d/1ETKH31-E7G-7ntEOlWGZcDZWuukmeHFe/view) by The Cyber Mentor

#### CIDR notation

**CIDR (Classless Inter-Domain Routing)** notation represents an IP address together with its subnet mask. It specifies the **network prefix length** - how many bits belong to the network portion - by appending a slash and that number to the address.

```
192.168.0.0/24
            └── the first 24 bits are the network portion;
                the remaining 8 bits are the host portion
```

A `/24` prefix corresponds to the subnet mask **255.255.255.0**: the first three octets are the network, and the last octet is free for host addresses (giving 254 usable hosts, since the first and last addresses are reserved for the network and broadcast).

#### Borrowing bits to create subnets

To subnet further, borrow additional bits from the host portion. Borrowing 2 bits creates 2² = **4 subnets**, and changes the mask from `/24` to `/26` → **255.255.255.192**.

The four resulting subnets of `192.168.0.0/24` are:

| Subnet | CIDR             | Network range                 |
| ------ | ---------------- | ----------------------------- |
| 1      | 192.168.0.0/26   | 192.168.0.0 – 192.168.0.63    |
| 2      | 192.168.0.64/26  | 192.168.0.64 – 192.168.0.127  |
| 3      | 192.168.0.128/26 | 192.168.0.128 – 192.168.0.191 |
| 4      | 192.168.0.192/26 | 192.168.0.192 – 192.168.0.255 |

Each subnet can then be assigned to a different segment or purpose. In every subnet, the **first address is the network ID** and the **last is the broadcast address**, so a `/26` has 64 total addresses but **62 usable hosts**.

#### Quick reference

| CIDR | Subnet mask     | Host bits | Usable hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 8         | 254          |
| /25  | 255.255.255.128 | 7         | 126          |
| /26  | 255.255.255.192 | 6         | 62           |
| /27  | 255.255.255.224 | 5         | 30           |
| /28  | 255.255.255.240 | 4         | 14           |
| /29  | 255.255.255.248 | 3         | 6            |
| /30  | 255.255.255.252 | 2         | 2            |

CIDR gives a concise way to describe networks and subnets, allowing flexible network boundaries and efficient address allocation.
