# TCP/IP Model

The [OSI Model](osi-model.md) is a reference/logical model. It was designed to describe the functions of the communication system by dividing the communication procedure into smaller and simpler components. The TCP/IP model was designed and developed by the Department of Defense (DoD) and is based on standard protocols. It stands for Transmission Control Protocol/Internet Protocol. This model is a concise version of the OSI model. It contains four layers, unlike seven layers in the OSI model. The layers are:

1. Process/Application Layer
2. Host-to-Host/Transport Layer
3. Internet Layer
4. Network Access/Link Layer

<figure><img src="../../.gitbook/assets/image (2) (7).png" alt=""><figcaption></figcaption></figure>

### Comparing the 2 models

| TCP/IP                                                                           | OSI                                                                                                    |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| TCP refers to Transmission Control Protocol.                                     | OSI refers to Open Systems Interconnection.                                                            |
| TCP/IP has 4 layers.                                                             | OSI has 7 layers.                                                                                      |
| TCP/IP is more reliable                                                          | OSI is less reliable                                                                                   |
| TCP/IP does not have very strict boundaries.                                     | OSI has strict boundaries                                                                              |
| TCP/IP follow a horizontal approach.                                             | OSI follows a vertical approach.                                                                       |
| TCP/IP uses both session and presentation layer in the application layer itself. | OSI uses different session and presentation layers.                                                    |
| TCP/IP developed protocols then model.                                           | OSI developed model then protocol.                                                                     |
| Transport layer in TCP/IP does not provide assurance delivery of packets.        | In OSI model, transport layer provides assurance delivery of packets.                                  |
| TCP/IP model network layer only provides connection less services.               | Connection less and connection oriented both services are provided by network layer in OSI model.      |
| Protocols cannot be replaced easily in TCP/IP model.                             | While in OSI model, Protocols are better covered and is easy to replace with the change in technology. |

### Breakdown of the TCP/IP Model

#### 1. Network Access Layer

This layer corresponds to the combination of Data Link Layer and Physical Layer of the OSI model. It looks out for hardware addressing and the protocols present in this layer allows for the physical transmission of data.\
ARP being a protocol of Internet layer, but there is a conflict about declaring it as a protocol of Internet Layer or Network access layer. It is described as residing in layer 3, being encapsulated by layer 2 protocols.

#### 2. Internet Layer

This layer parallels the functions of OSI’s Network layer. It defines the protocols which are responsible for logical transmission of data over the entire network.

The main protocols residing at this layer:

1. **IP,** or Internet Protocol and it is responsible for delivering packets from the source host to the destination host by looking at the IP addresses in the packet headers. IP has 2 versions:\
   IPv4 and IPv6. IPv4 is the one that most of the websites are using currently. But IPv6 is growing as the number of IPv4 addresses are limited in number when compared to the number of users.
2. **ICMP,** or Internet Control Message Protocol. It is encapsulated within IP datagrams and is responsible for providing hosts with information about network problems.
3. **ARP,** or Address Resolution Protocol. Its job is to find the hardware address of a host from a known IP address. ARP has several types: Reverse ARP, Proxy ARP, Gratuitous ARP and Inverse ARP.

**3. Host-to-Host Layer**

This layer is analogous to the transport layer of the OSI model. It is responsible for end-to-end communication and error-free delivery of data. It shields the upper-layer applications from the complexities of data.

The two main protocols are:

1. **Transmission Control Protocol (TCP) –** It is known to provide reliable and error-free communication between end systems. It performs sequencing and segmentation of data. It also has acknowledgment feature and controls the flow of the data through flow control mechanism. It is a very effective protocol but has a lot of overhead due to such features. Increased overhead leads to increased cost.
2. **User Datagram Protocol (UDP) –** On the other hand does not provide any such features. It is the go-to protocol if your application does not require reliable transport as it is very cost-effective. Unlike TCP, which is connection-oriented protocol, UDP is connectionless.

#### 4. Application Layer

This layer performs the functions of top three layers of the OSI model: Application, Presentation and Session Layer. It is responsible for node-to-node communication and controls user-interface specifications. Some of the protocols present in this layer are: HTTP, HTTPS, FTP, TFTP, Telnet, SSH, SMTP, SNMP, NTP, DNS, DHCP, NFS, X Window, LPD. Have a look at Protocols in Application Layer for some information about these protocols.

Protocols are:

1. **HTTP and HTTPS –** HTTP, or Hypertext transfer protocol. It is used by the World Wide Web to manage communications between web browsers and servers. HTTPS, or HTTP-Secure. It is a combination of HTTP with SSL(Secure Socket Layer). It is efficient in cases where the browser need to fill out forms, sign in, authenticate and carry out bank transactions.
2. **SSH –** SSH, or Secure Shell. It is a terminal emulations software similar to Telnet. The reason SSH is more preferred is because of its ability to maintain the encrypted connection. It sets up a secure session over a TCP/IP connection.
3. **NTP –** NTP, or Network Time Protocol. It is used to synchronize the clocks on our computer to one standard time source. It is very useful in situations like bank transactions. Assume the following situation without the presence of NTP. Suppose you carry out a transaction, where your computer reads the time at 2:30 PM while the server records it at 2:28 PM. The server can crash very badly if it’s out of sync.
