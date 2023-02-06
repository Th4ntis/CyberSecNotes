---
description: Additional notes
---

# 3-Way Handshake

## 3-Way Handshake Process:

Transmission Control Protocol (TCP) provides a secure and reliable connection between two devices using the 3-way handshake process. TCP uses the full-duplex connection to synchronize (SYN) and acknowledge (ACK) each other on both sides. There are three steps for both establishing and closing a connection. They are − **SYN**, **SYN-ACK**, and **ACK**.

#### Synchronization Sequence Number (SYN) − The client sends the SYN to the server

* When the client wants to connect to the server, then it sends the message to the server by setting the SYN flag as 1.
* The message carries some additional information like the sequence number (32-bit random number).
* The ACK is set to 0. The maximum segment size and the window size are also set. For example, if the window size is 1000 bits and the maximum segment size is 100 bits, then a maximum of 10 data segments can be transmitted in the connection by dividing (1000/100=10).

#### Synchronization and Acknowledgement (SYN-ACK) to the client

* The server acknowledges the client request by setting the ACK flag to 1.
* The ACK indicates the response of the segment it received and SYN indicates with what sequence number it will start the segments.
* For example, if the client has sent the SYN with sequence number = 500, then the server will send the ACK using acknowledgment number = 5001.
* The server will set the SYN flag to '1' and send it to the client if the server also wants to establish the connection.
* The sequence number used for SYN will be different from the client's SYN.
* The server also advertises its window size and maximum segment size to the client. And, the connection is established from the client-side to the server-side.

#### Acknowledgment (ACK) to the server

* The client sends the acknowledgment (ACK) to the server after receiving the synchronization (SYN) from the server.
* After getting the (ACK) from the client, the connection is established between the client and the server.
* Now the data can be transmitted between the client and server sides.

#### 3 -Way Handshake Closing Connection Process

To close a 3-way handshake connection:

* First, the client requests the server to terminate the established connection by sending FIN.
* After receiving the client request, the server sends back the FIN and ACK request to the client.
* After receiving the FIN + ACK from the server, the client confirms by sending an ACK to the server.

## Common ports/protocols:

