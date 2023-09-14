# General Networking

## DHCP

[Dynamic Host Configuration Protocol (DHCP)](https://www.fortinet.com/resources/cyberglossary/dynamic-host-configuration-protocol-dhcp) is used to dynamically assign IP addresses to each machine on your organization's network.&#x20;

In the context of this DHCP definition, DHCP also assigns [Domain Name System (DNS)](https://www.fortinet.com/resources/cyberglossary/what-is-dns) addresses, subnet masks, and default gateways. All of these enable devices to communicate with the internet and each other within the confines of your network.

DHCP sends messages to devices that connect to your network, providing them with what they need to interface with essential network functions. Assigning IP addresses, subnet masks, DNS addresses, and other essential data, DHCP automatically provides this information to all of the devices that connect to your network.

## DNS

[Domain Name System (DNS)](https://www.fortinet.com/resources/cyberglossary/what-is-dns) turns domain names into IP addresses. Every device connected to the internet has its own IP address, which is used by other devices to locate the device. DNS servers make it possible for people to input normal words into their browsers, such as google.com, without having to keep track of the IP address for every website.

## ARP

[Address Resolution Protocol (ARP)](https://www.fortinet.com/resources/cyberglossary/what-is-arp) is a protocol or procedure that connects an ever-changing Internet Protocol (IP) address to a fixed physical machine address, also known as a media access control (MAC) address, in a local-area network (LAN). Essentially ARP is the process of connecting a dynamic IP address to a physical machine's MAC address.

ARP matches IP addresses to MAC addresses on a LAN. While DNS matches a public internet IP to a domain name.

### ARP Spoofing/ARP Poisoning

ARP spoofing, ARP poison routing or ARP cache poisoning is a type of malicious attack in which a cyber criminal sends fake ARP messages to a target LAN with the intention of linking their MAC address with the IP address of a legitimate device or server within the network. The link allows for data from the victim's computer to be sent to the attacker's computer instead of the original destination.

ARP spoofing attacks can prove dangerous, as sensitive information can be passed between computers without the victims' knowledge. ARP spoofing also enables other forms of cyberattacks, like Man-In-The-Middle, Denial of Service, and Session Hijacking,
