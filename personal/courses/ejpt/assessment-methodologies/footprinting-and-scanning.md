# Footprinting & Scanning

## Mapping a Network

The **Purpose** is Scope and Discovery. Find out what device(s) on the network are we allowed to target, or find what is in scope.&#x20;

#### Physical Access

* Physical Security
  * Testing Access Control, Guards, Cameras, anything we can find or get into physically.
* OSINT
  * DNS Records, Websites, IPs, Emails, Domains, etc.
* Social Engineering
  * 'Trick' someone into giving us any information we are after.

#### Sniffing

* Passive Recon
  * Find hosts, IPs, MAC Addresses are on the network with sniffing.&#x20;
* Watch Network Traffic
  * Using TCPDump, Wireshark, etc. to see emails, websites visited, what files are being stored or accessed from a file server.&#x20;

#### ARP

Taking advantage of ARP to resolve IP addresses to MAC addresses to add machines to our ARP table.

#### ICMP

ICMP can be used for network connectivity issues using Ping or Traceroute.

## Tools:

### Wireshark

<figure><img src="../../../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

We will be looking at the `vmnet8` adapter to start a packet capture.

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

We can go to Statistics > Endpoints to see a list of MAC addresses.

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Looking in the logs, we can also see a reply telling us the MAC address of the IP

<figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

### ARP-Scan

Wecan initiate the arp-scan with `sudo arp-scan -I (interface) (IP and Subnet)`

`` `sudo arp-scan -I vmnet8 172.16.8.0/24` ``

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### Ping

We can ping an IP we have found from our scanning to verify communication with the host.

### FPing

Will send out pings to multiple hosts at one time. Using `fping -i (internaface) -g (IP Range) -a 2>/dev/null` to show us only the alive hosts removing the all the errors of the unreachable hosts.

`fping -I vmnet8 -g 172.16.8.0/24 -a 2>/dev/null`

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Notice the .131 address is missing, this is due to the machine not responding to ping requests.

### Nmap

We have seen in the previous section

`sudo nmap -sn 172.16.8.0/24`

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Zenmap

Simple, a GUI version of NMap
