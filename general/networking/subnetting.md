# Subnetting

**I recommend:** [**Professor Messer Seven Second Subnetting**](https://www.youtube.com/watch?v=ZxAwQB8TZsM) **as a great video to start with.**

{% embed url="https://youtu.be/ZxAwQB8TZsM" %}

[A Subnetting Guide](https://drive.google.com/file/d/1ETKH31-E7G-7ntEOlWGZcDZWuukmeHFe/view) by The Cyber Mentor

Subnetting is the process of dividing a network into smaller "subnetworks" called "subnets". It allows for a better use of IP addresses and uses network management and routing, mostly used in IPv4 networks

Subnetting involves borrowing bits from the host portion of an IP address to create a subnet identifier. By doing this, a network can be divided into multiple subnets, each with its own range of IP addresses.

CIDR (Classless Inter-Domain Routing) notation is used to represent IP addresses and their corresponding subnet masks. It specifies the network prefix length, which indicates the number of bits used for the network portion of the IP address. CIDR notation is expressed by appending a forward slash (/) followed by the prefix length to the IP address.

Eg. The IP address: **192.168.0.0/24**

The IP address is in the format of "192.168.0.0" and the "/24" represents the prefix length, indicating that the first 24 bits represent the network portion of the IP address, while the remaining 8 bits represent the host portion.

With a /24 prefix length, the subnet mask for this network would be 255.255.255.0. This means that the first three octets are reserved for the network, and the last octet can be used for giving IP addressed to hosts within the subnet.

To subnet this network more, additional bits can be borrowed from the host portion. For instance, if we borrow 2 bits, we can create 4 subnets. The subnet mask would become 255.255.255.192.

The four subnets would then be:

* Subnet 1: 192.168.0.0/26 (network range: 192.168.0.0 - 192.168.0.63)
* Subnet 2: 192.168.0.64/26 (network range: 192.168.0.64 - 192.168.0.127)
* Subnet 3: 192.168.0.128/26 (network range: 192.168.0.128 - 192.168.0.191)
* Subnet 4: 192.168.0.192/26 (network range: 192.168.0.192 - 192.168.0.255)

Each subnet can then be assigned to a different segment or used for different purposes within the network.

CIDR notation provides a concise way to represent networks and subnets by specifying the prefix length. It allows for flexibility in defining network boundaries and enables efficient address allocation in IP networking.
