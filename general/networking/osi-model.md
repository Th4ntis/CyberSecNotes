# OSI Model

The OSI model (Open Systems Interconnection Model) is an absolute fundamental model used in networking. This critical model provides a framework dictating how all networked devices will send, receive and interpret data.

One of the main benefits of the OSI model is that devices can have different functions and designs on a network while communicating with other devices. Data sent across a network that follows the uniformity of the OSI model can be understood by other devices.

The OSI model consists of seven layers which are illustrated in the diagram below. Each layer has a different set of responsibilities and is arranged from Layer 7 to Layer 1.



<table><thead><tr><th width="162.33333333333331">Layer Number</th><th width="133">Layer Name</th><th>Uses</th></tr></thead><tbody><tr><td>1</td><td>Physical</td><td>Data Cables, Ethernet Cables, etc.</td></tr><tr><td>2</td><td>Data</td><td>Switching, MAC Addresses</td></tr><tr><td>3</td><td>Network</td><td>IP addresses, Routing</td></tr><tr><td>4</td><td>Transport</td><td>TCP/UDP</td></tr><tr><td>5</td><td>Session</td><td>Session Management</td></tr><tr><td>6</td><td>Presentation</td><td>Media files(WMV, JPG, MOV, etc.)</td></tr><tr><td>7</td><td>Application</td><td>HTTP, HTTPS, FTP, SMTP, etc</td></tr></tbody></table>

**From Application to Physical (Layer 7 to Layer 1):** \
**- A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing\
\- **A**ll **P**ros **S**earch **T**op **N**otch **D**onut **P**laces\
\- **A** **P**enguin **S**aid **T**hat **N**obody **D**rinks **P**epsi\
\- **A** **P**riest **S**aw **T**wo **N**uns **D**oing **P**ushups

**From Physical to Application (Layer 1 to Layer 7):**\
**- P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza Away\
\- **P**ew! **D**ead **N**inja **T**urtles **S**mell **P**articularly **A**wful\
\- **P**eople **D**on’t **N**eed **T**o **S**ee **P**aula **A**bdul\
\- **P**ete **D**oesn’t **N**eed **T**o **S**ell **P**ickles **A**nymore

Receiving data go 1 to 7, while transferring Data goes 7 to 1, when trouble shooting, it's always best to start with layer 1(Physical).

### Layer 1: Physical

This layer is one of the easiest layers to grasp. Put simply, this layer references the physical components of the hardware used in networking and is the lowest layer that you will find. Devices use electrical signals to transfer data between each other in a binary numbering system (1's and 0's).

### Layer 2: Data

Layer 2, the data link layer, focuses on the physical addressing of the transmission. It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical MAC (Media Access Control) address of the receiving endpoint. Inside every network-enabled computer is a Network Interface Card (NIC) which comes with a unique MAC address to identify it.

MAC addresses are set by the manufacturer and literally burnt into the card; they can't be changed, although they can be spoofed. When information is sent across a network, it's actually the physical address that is used to identify where exactly to send the information.

Additionally, it's also the job of the data link layer to present the data in a format suitable for transmission.

### Layer 3: Network

Layer 3, the network layer, is where the magic of routing & re-assembly of data takes place (from these small chunks to the larger chunk). Firstly, routing simply determines the most optimal path in which these chunks of data should be sent.

Whilst some protocols at this layer determine exactly what is the "optimal" path that data should take to reach a device, we should only know about their existence at this stage of the networking module. Briefly, these protocols include OSPF (Open Shortest Path First) and RIP (Routing Information Protocol). The factors that decide what route is taken is decided by the following:

* What path is the shortest? I.e. has the least amount of devices that the packet needs to travel across.
* What path is the most reliable? I.e. have packets been lost on that path before?
* Which path has the faster physical connection? I.e. is one path using a copper connection (slower) or a fibre (considerably faster)?

At this layer, everything is dealt with via IP addresses such as 192.168.1.100. Devices such as routers capable of delivering packets using IP addresses are known as Layer 3 devices, because they are capable of working at the third layer of the OSI model.

### Layer 4: Transport

Layer 4, the transport layer,  plays a vital part in transmitting data across a network and can be a little bit difficult to grasp. When data is sent between devices, it follows one of two different protocols that are decided based upon several factors: TCP and UDP

* TCP (Transmissions Control Protocol) is a connection oriented protocol. More reliable, if a packet is dropped, the connection would stop until that packet was picked up again and sent, ensuring you are receiving all the data you are supposed to. Most websites, file transfers, etc. use this protocol.

TCP incorporates error checking into its design. Error checking is how TCP can guarantee that data sent from the small chunks in the session layer (layer 5) has then been received and reassembled in the same order.

* UDP is User Datagram Protocol, a connection-less protocol. If a stream of data packets were being sent to you and one was dropped, the stream would continue as the packet that was dropped is not important. VoIP, video streaming, video calls, etc. use this protocol.

Three-Way-Handshake: SYN > SYN-ACK > ACK

* Eg1. Syn - Saying Hello > Syn-Ack - Getting a Hello response > Ack - Starting a conversation
* Eg2. Syn - I want to connect to your website on port 443 > Syn-Ack - IF Port 443 is open, it will respond saying you're OK to connect > Ack - You continue the connection and go to the website.

### Layer 5: Session

Layer 5, the session layer. Once data has been correctly translated or formatted from the presentation layer (layer 6), the session layer (layer 5) will begin to create a connection to the other computer that the data is destined for. When a connection is established, a session is created. Whilst this connection is active, so is the session.

The session layer (layer 5) synchronizes the two computers to ensure that they are on the same page before data is sent and received. Once these checks are in place, the session layer will begin to divide up the data sent into smaller chunks of data and begin to send these chunks (packets) one at a time. This dividing up is beneficial because if the connection is lost, only the chunks that weren't yet sent will have to be sent again — not the entire piece of the data (think of it as loading a save file in a video game).

What is worthy of noting is that sessions are unique — meaning that data cannot travel over different sessions, but in fact, only across each session instead.

### Layer 6: Presentation

Layer 6, the presentation layer, is the layer in which standardization starts to take place. Because software developers can develop any software, such as an email client, differently. The data still needs to be handled in the same way, no matter how the software works.

This layer acts as a translator for data to and from the application layer (layer 7). The receiving computer will also understand data sent to a computer in one format destined for in another format. For example, when you send an email, the other user may have another email client to you, but the contents of the email will still need to display the same.

Security features such as data encryption (like HTTPS when visiting a secure site) occur at this layer.

### Layer 7: Application

Layer 7, application layer, is the layer that you will be most familiar with. This familiarity is because the application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received.

Everyday applications such as email clients, browsers, or file server browsing software such as FileZilla provide a friendly, Graphical User Interface (GUI) for users to interact with data sent or received. Other protocols include DNS&#x20;
