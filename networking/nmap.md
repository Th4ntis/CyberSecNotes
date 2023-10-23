# NMap

[NMap](https://nmap.org/) (Network Mapper) is a network scanning tool. From the NMap website: "...an open source tool for network exploration and security auditing. It was designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. While Nmap is commonly used for security audits, many systems and network administrators find it useful for routine tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime."

## Scan Types

### TCP Scan

Similar to the 3-Way Handshake, the TCP Scan(-sT) sends a TCP request to the target with the SYN flag set, the target then responds with a SYN flag, as well as an ACK flag, finally our machine completes the handshake by sending the target the ACK flag.

If the port is closed, the target will respond with a RST packet.

### SYN Scan

SYN Scans(-sS), sometimes known as "Half-open" or "Stealth" scans. How TCP Scans perform the full 3-way handshake, the SYN scan send back a RST packet after receiving the SYN/ACK from the target. Without having to bother about completing (and disconnecting from) a three-way handshake for every port, SYN scans are significantly faster than a standard TCP Connect scan.

### UDP Scan

UPD Scans (-sU) is when a packet is sent to an open UDP port, there should be no response as a UDP Scan send an empty UDP packet. When this happens, Nmap refers to the port as being "open | filtered". Which just means it suspects that the port is open, but it could be firewalled. If it gets a UDP response, then the port is marked as _open_. More commonly there is no response, which then the request is sent a second time as a double-check. If there is still no response then the port is marked as "open | filtered" and Nmap moves on.\


When a packet is sent to a _closed_ UDP port, the target should respond with an ICMP (ping) packet containing a message that the port is unreachable. This identifies closed ports, which Nmap marks as closed and moves on.

## ICMP(Ping) Scan

ICMP Scanning (-sn) sends an ICMP packet to each host on the network see which hosts are up and active and which are not, also known as a "ping sweep". &#x20;

## NMap Scripting Engine

Also known as [NSE](https://nmap.org/nsedoc/), are scripts written in LUA that can be used to scanning for vulnerabilities and automatically exploiting them. There's plenty of categories for the scripting library though and more information on them can be found [here](https://nmap.org/book/nse-usage.html).&#x20;

## Scan Arguments

* **-t** - Set timing template 0-5 (higher is faster, but noisier) - T4/T5 is usually better.
* **-sS** - SYN scan, "Half-Open"/"Stealth". Must be used with sudo permissions as SYN scans require the ability to create raw packets, which is a privilege only the root user has by default.
* **-sT -** TCP Scan
* **-sU** - UDP scan
* **-v** - Increase verbosity level (use -vv or more for greater effect)
* **-sn** - Ping sweep, sends an ICMP packet to each possible IP address for the specified network. When it receives a response, it marks the IP address that responded as being alive.&#x20;
* **-A** - Enables OS and version detection, executes in-build scripts for further enumeration
* **-sC** - Scan with the default nmap scripts
* **-Pn** - Disable host discovery and just scan for open ports
* **-sV** - Attempts to determine the version of the services running
* **-oA** - Saves out to .gnmap, .nmap, and .xml format
* **-oN** - Saves results in a "normal" format
* **-oG** - Saves results in a "grepable" format
