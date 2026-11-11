# Network Models

## Network Models

Network models describe **how data is packaged, addressed, transmitted, and interpreted** as it moves between devices. This note covers the two models you'll meet constantly - the **OSI model** and the **TCP/IP model** - and then walks through the **3-way handshake**, the TCP mechanism that opens and closes reliable connections.

For addressing and the protocols referenced here (IP, MAC, ARP, DNS, DHCP, ports), see [Networking Fundamentals](network-fundamentals.md).

**Contents**

* The OSI Model
* The TCP/IP Model
* OSI vs. TCP/IP
* The 3-Way Handshake

***

### The OSI Model

The **OSI model** (Open Systems Interconnection model) is a fundamental reference model in networking. It provides a framework that dictates how networked devices send, receive, and interpret data.

Its main benefit is **interoperability**: devices can have completely different hardware, operating systems, and functions, yet still communicate as long as they follow the uniform structure the OSI model describes. Data that conforms to the model can be understood by any other compliant device.

The model has **seven layers**, each with its own responsibilities, numbered from Layer 7 (closest to the user) down to Layer 1 (the physical medium).

| Layer | Name         | Example uses                                       |
| ----- | ------------ | -------------------------------------------------- |
| 7     | Application  | HTTP, HTTPS, FTP, SMTP, DNS                        |
| 6     | Presentation | Encryption/formatting; media files (JPG, MOV, WMV) |
| 5     | Session      | Session management                                 |
| 4     | Transport    | TCP / UDP                                          |
| 3     | Network      | IP addresses, routing                              |
| 2     | Data Link    | Switching, MAC addresses                           |
| 1     | Physical     | Cables, Ethernet, electrical signals               |

#### Remembering the order

**Layer 7 → 1 (Application to Physical):**

* **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
* **A**ll **P**ros **S**earch **T**op **N**otch **D**onut **P**laces
* **A** **P**enguin **S**aid **T**hat **N**obody **D**rinks **P**epsi

**Layer 1 → 7 (Physical to Application):**

* **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way
* **P**ew! **D**ead **N**inja **T**urtles **S**mell **P**articularly **A**wful
* **P**eople **D**on't **N**eed **T**o **S**ee **P**aula **A**bdul

> Data being **sent** travels **down** the stack (7 → 1); data being **received** travels **up** (1 → 7). When troubleshooting, it's usually best to start at **Layer 1 (Physical)** - check the cable before blaming the application. This bottom-up approach is sometimes called "ping the cable first."

As data moves **down** the stack on the sending side, each layer wraps it with its own header - a process called **encapsulation**. The receiving side **de-encapsulates**, stripping headers as the data moves back **up**. The unit of data has a different name at different layers: **data** (L7–5) → **segment** (L4, TCP) / **datagram** (L4, UDP) → **packet** (L3) → **frame** (L2) → **bits** (L1).

#### Layer 1: Physical

The lowest and most literal layer. It refers to the **physical hardware** - cables, connectors, radio - and the raw transmission of data as electrical, optical, or radio signals in binary (1s and 0s).

#### Layer 2: Data Link

The data link layer handles **physical addressing**. It receives a packet from the network layer (which carries the destination IP address) and adds the **MAC address** of the next-hop endpoint. Every NIC has a unique MAC address burned in by the manufacturer (it can't be changed, though it can be spoofed). When frames are sent across a local network, it's the physical/MAC address that determines exactly where they go. This layer is also responsible for formatting the data suitably for transmission. **Switches** operate here.

#### Layer 3: Network

The network layer is where **routing and the reassembly of data** take place. Routing determines the optimal path that chunks of data should take to reach their destination. Routing protocols such as **OSPF (Open Shortest Path First)** and **RIP (Routing Information Protocol)** decide the "best" path based on factors like:

* **Shortest path** - fewest devices (hops) to cross.
* **Reliability** - have packets been lost on that path before?
* **Speed of the physical link** - e.g. copper (slower) vs. fibre (much faster).

Everything here is handled via **IP addresses** (e.g. `192.168.1.100`). Devices that forward packets using IP addresses - **routers** - are called **Layer 3 devices**.

#### Layer 4: Transport

The transport layer is central to moving data across a network. It chooses one of two protocols based on the application's needs:

* **TCP (Transmission Control Protocol)** - **connection-oriented** and reliable. If a packet is dropped, the connection pauses until it's re-sent, guaranteeing all the data arrives in order. Used by most websites, file transfers, and email. TCP's built-in **error checking** guarantees that the chunks created higher up are received and reassembled in the correct order. Connections are established with the 3-way handshake.
* **UDP (User Datagram Protocol)** - **connectionless** and lightweight. If a packet is dropped, the stream simply continues because that packet isn't worth waiting for. Used for VoIP, video streaming, and video calls, where speed matters more than perfect delivery.

#### Layer 5: Session

Once data has been formatted by the presentation layer, the session layer **establishes, maintains, and tears down the connection** (the "session") between the two computers. While the connection is active, so is the session.

The session layer **synchronizes** the two computers so they're on the same page before data flows, then divides the data into smaller chunks and sends them one at a time. This chunking matters: if the connection drops, only the chunks not yet sent need to be re-sent - not the whole transfer (think of reloading a save file in a video game). Sessions are **unique** - data from one session cannot cross into another.

#### Layer 6: Presentation

The presentation layer is where **standardization** happens. Different developers can write software (say, email clients) however they like, but the data still has to be handled in a common way. This layer acts as a **translator** to and from the application layer, so that a message sent from one program is correctly understood by a different program on the other end - the email contents display the same regardless of which client is used.

**Encryption** also happens here - for example, the TLS that turns HTTP into **HTTPS** when visiting a secure site.

#### Layer 7: Application

The layer you interact with most directly. It holds the protocols and rules that determine **how the user interacts with data**. Everyday software - email clients, browsers, file-transfer tools like FileZilla - provides a friendly **GUI** on top of this layer. Protocols here include HTTP, HTTPS, FTP, SMTP, and DNS.

***

### The TCP/IP Model

Where the OSI model is a **reference/logical** model (built as a conceptual framework, then protocols followed), the **TCP/IP model** was built around **protocols that already existed**. It was designed by the U.S. **Department of Defense (DoD)** and named for its two core protocols: **Transmission Control Protocol** and **Internet Protocol**.

The TCP/IP model is a more concise version of OSI, collapsing the seven OSI layers into **four**:

1. **Application Layer** (= OSI Application + Presentation + Session)
2. **Host-to-Host / Transport Layer** (= OSI Transport)
3. **Internet Layer** (= OSI Network)
4. **Network Access / Link Layer** (= OSI Data Link + Physical)

#### Layer breakdown

**1. Network Access Layer**

Corresponds to OSI's **Data Link + Physical** layers combined. It handles **hardware addressing** and the protocols that allow the physical transmission of data across a medium.

> **Where does ARP live?** ARP is a point of debate: it's often described as a Layer 3 (Internet) protocol because it works with IP addresses, yet it's encapsulated directly by Layer 2 protocols, which places it at the boundary between the Internet and Network Access layers.

**2. Internet Layer**

Parallels OSI's **Network** layer. It defines the protocols responsible for the **logical transmission of data across the whole network**. Main protocols:

1. **IP (Internet Protocol)** - delivers packets from source host to destination host by reading the IP addresses in the packet headers. Comes in **IPv4** (most common today) and **IPv6** (growing, because IPv4 addresses are limited). See Networking Fundamentals.
2. **ICMP (Internet Control Message Protocol)** - encapsulated within IP datagrams; reports network problems and diagnostics back to hosts. (This is what `ping` and `traceroute` use.)
3. **ARP (Address Resolution Protocol)** - finds a host's hardware (MAC) address from a known IP address. Variants include Reverse ARP, Proxy ARP, Gratuitous ARP, and Inverse ARP.

**3. Host-to-Host (Transport) Layer**

Analogous to OSI's **Transport** layer. Responsible for **end-to-end communication** and error-free delivery, shielding the upper-layer applications from the complexity underneath. Two main protocols:

1. **TCP (Transmission Control Protocol)** - reliable, error-free communication. It handles **sequencing** and **segmentation**, uses **acknowledgments**, and manages **flow control**. All of this makes it effective but adds overhead (and therefore cost).
2. **UDP (User Datagram Protocol)** - provides none of those guarantees. It's connectionless and very cost-effective, making it the go-to when the application doesn't need reliable transport.

**4. Application Layer**

Performs the functions of OSI's **top three layers** (Application, Presentation, Session). It handles node-to-node communication and user-interface specifications. Common protocols include HTTP, HTTPS, FTP, TFTP, Telnet, SSH, SMTP, SNMP, NTP, DNS, DHCP, NFS, X Window, and LPD. A few worth knowing:

1. **HTTP / HTTPS** - HTTP (HyperText Transfer Protocol) manages communication between web browsers and servers. **HTTPS** combines HTTP with **TLS/SSL** for encryption, essential for forms, sign-ins, authentication, and banking.
2. **SSH (Secure Shell)** - a terminal protocol similar to Telnet, but it maintains an **encrypted** connection over TCP/IP, which is why it's preferred.
3. **NTP (Network Time Protocol)** - synchronizes computer clocks to a standard time source. Critical for things like bank transactions: if your computer reads 2:30 PM while the server records 2:28 PM, the mismatch can cause serious problems.

***

### OSI vs. TCP/IP

| TCP/IP                                                       | OSI                                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------------------ |
| Stands for Transmission Control Protocol / Internet Protocol | Stands for Open Systems Interconnection                                  |
| 4 layers                                                     | 7 layers                                                                 |
| More reliable (built from working protocols)                 | Less reliable (conceptual)                                               |
| Boundaries between layers are loose                          | Boundaries are strict                                                    |
| Horizontal approach                                          | Vertical approach                                                        |
| Combines session + presentation into the application layer   | Separate session and presentation layers                                 |
| Protocols were developed first, then the model               | Model was developed first, then protocols                                |
| Transport layer does not guarantee packet delivery           | Transport layer guarantees packet delivery                               |
| Network layer offers only connectionless service             | Network layer offers both connectionless and connection-oriented service |
| Protocols are hard to replace                                | Protocols are easier to replace as technology changes                    |

**Bottom line:** OSI is the teaching/troubleshooting framework; TCP/IP is what the Internet actually runs on. Most people reason in OSI layer numbers ("that's a Layer 2 problem") while working on TCP/IP-based networks.

***

### The 3-Way Handshake

**TCP** provides a reliable, ordered connection between two devices using the **3-way handshake**. TCP is **full-duplex** (both sides can send at once), so before any data flows, both sides **synchronize (SYN)** and **acknowledge (ACK)** each other. Opening a connection takes three steps: **SYN → SYN-ACK → ACK**.

#### Opening a connection

**1. SYN - client → server**

* The client initiates by sending a segment with the **SYN flag set to 1**.
* It includes an **Initial Sequence Number** (a 32-bit random number), and advertises its **maximum segment size (MSS)** and **window size**.
* The ACK flag is 0 at this stage. _(Window-size example: with a window of 1000 bits and an MSS of 100 bits, up to 10 segments can be outstanding at once - 1000 / 100 = 10.)_

**2. SYN-ACK - server → client**

* The server acknowledges the request by setting the **ACK flag to 1**.
* The **acknowledgment number** is the client's sequence number **+ 1**. _(If the client sent SYN with sequence number 500, the server replies with acknowledgment number **501**.)_
* The server also sets its **own SYN flag to 1** to open the connection in its direction, using a **different, independent sequence number** from the client's.
* It advertises its own window size and MSS.

**3. ACK - client → server**

* The client sends a final **ACK** acknowledging the server's SYN.
* Once the server receives this ACK, the connection is **established** and data can flow in both directions.

```
Client                         Server
  │  ──────── SYN  ──────────▶  │   "Hello - I want to connect (seq=500)"
  │  ◀────── SYN-ACK ──────────  │   "Hello back, OK (ack=501, my seq=800)"
  │  ──────── ACK  ──────────▶  │   "Great, let's talk (ack=801)"
  │        connection established │
```

A plain-language version:

* **SYN** - "Hi, can I connect to your website on port 443?"
* **SYN-ACK** - "If port 443 is open, I respond: yes, you're OK to connect."
* **ACK** - "Thanks - continuing the connection, now loading the site."

#### Closing a connection

Tearing down a TCP connection uses the **FIN** flag:

1. The client requests termination by sending **FIN**.
2. The server replies with **ACK**, and then its own **FIN** (acknowledging the request and signaling it's also ready to close).
3. The client confirms with a final **ACK**, and the connection closes.

> Because each direction is closed independently, a full teardown is often described as a **four-way** exchange (FIN, ACK, FIN, ACK), though the server's ACK and FIN are frequently combined.
