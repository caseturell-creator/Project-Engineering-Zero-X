# TCP, UDP, and Ports

## Overview

The Transport layer is responsible for communication between applications running on networked systems.

Two of the most important Transport layer protocols are:

```text
TCP
UDP
```

The Transport layer is also where:

```text
Port numbers
```

are used.

A useful mental model is:

```text
IP Address = Which building/house?

Port Number = Which room/service inside?
```

Getting traffic to the correct computer is not enough.

The computer also needs to know:

```text
Which application should receive it?
```

That is one of the main jobs of ports.

---

# IP Address vs Port

Suppose a computer has:

```text
IP Address:
192.168.1.20
```

That identifies the machine's network location.

But the same computer may simultaneously run:

```text
Web Server
SSH Server
DNS Service
Email Service
```

The IP address gets traffic to:

```text
The machine
```

The port gets traffic to:

```text
The correct service
```

Conceptually:

```text
Internet
   ↓
192.168.1.20
   ↓
Computer
   |
   +-- Port 22  → SSH
   |
   +-- Port 53  → DNS
   |
   +-- Port 80  → HTTP
   |
   +-- Port 443 → HTTPS
```

---

# Your House Analogy

Think of the IP address as the address of a building.

```text
123 Main Street
```

gets the delivery person to the correct building.

But imagine the building contains many different rooms.

```text
Room 22
Room 53
Room 80
Room 443
```

The building address alone is not enough.

The delivery still needs to reach the correct room.

Networking works similarly:

```text
IP Address
   ↓
Gets traffic to the machine

Port Number
   ↓
Gets traffic to the correct service
```

So:

```text
IP = location

Port = service at that location
```

---

# What Is a Port?

A port is a logical number used by TCP or UDP to identify an application or service.

Port numbers range from:

```text
0 - 65535
```

Examples:

```text
22  → SSH
53  → DNS
80  → HTTP
443 → HTTPS
```

A connection may therefore look like:

```text
192.168.1.20:443
```

which means:

```text
192.168.1.20
      ↓
Target machine

443
 ↓
Target service
```

---

# Ports Belong to the Transport Layer

This is important:

```text
Ports do NOT belong to the Data Link layer.
```

Ports are used by:

```text
TCP
UDP
```

Therefore:

```text
Port
 ↓
TCP / UDP
 ↓
Transport Layer
```

---

# Source Port and Destination Port

Network communication normally contains both:

```text
Source Port
Destination Port
```

Example:

```text
Client:

192.168.1.10:53124
```

connecting to:

```text
Web Server:

192.168.1.20:443
```

The communication can be represented as:

```text
192.168.1.10:53124
        ↓
192.168.1.20:443
```

The server knows:

```text
443 = HTTPS service
```

The client uses a temporary source port so the operating system knows which local connection should receive the response.

---

# Why Clients Use Temporary Ports

Imagine opening several websites at once.

Your computer may create connections like:

```text
192.168.1.10:53001 → Website A:443

192.168.1.10:53002 → Website B:443

192.168.1.10:53003 → Website C:443
```

All three websites may use:

```text
443
```

but your computer uses different local source ports.

This allows the operating system to keep the connections separate.

Conceptually:

```text
Browser Connection 1 → Local Port 53001

Browser Connection 2 → Local Port 53002

Browser Connection 3 → Local Port 53003
```

---

# TCP

TCP stands for:

```text
Transmission Control Protocol
```

TCP is:

```text
Connection-oriented
```

and designed to provide reliable delivery.

TCP can:

```text
Establish a connection
Track transmitted data
Maintain ordering
Acknowledge received data
Detect missing data
Retransmit missing data
Close connections cleanly
```

---

# TCP Mental Model

Think of TCP like a conversation where both people constantly confirm what was heard.

```text
Sender:

"Did you get message 1?"

Receiver:

"Yes."

Sender:

"Did you get message 2?"

Receiver:

"No."

Sender:

"I'll send message 2 again."
```

TCP does not literally communicate using sentences like this, but the idea is similar.

TCP keeps track of communication.

---

# TCP Three-Way Handshake

Before normal TCP communication begins, the two systems establish a connection.

This is commonly called the:

```text
Three-Way Handshake
```

The basic sequence is:

```text
SYN
SYN-ACK
ACK
```

---

## Step 1 - SYN

The client sends:

```text
SYN
```

Conceptually:

```text
Client:

"I want to start a connection."
```

---

## Step 2 - SYN-ACK

The server responds:

```text
SYN-ACK
```

Conceptually:

```text
Server:

"I received your request,
and I am ready too."
```

---

## Step 3 - ACK

The client responds:

```text
ACK
```

Conceptually:

```text
Client:

"Confirmed."
```

The TCP connection is now established.

---

# TCP Handshake Diagram

```text
Client                           Server

   |                               |
   | -------- SYN ---------------> |
   |                               |
   | <------ SYN-ACK ------------- |
   |                               |
   | -------- ACK ---------------> |
   |                               |
   |      Connection Ready         |
```

---

# Why the Handshake Exists

TCP needs both sides to agree that communication can begin.

The handshake helps establish:

```text
Connection state

Initial sequence information

Communication readiness
```

This is part of what makes TCP:

```text
Connection-oriented
```

---

# TCP Sequence Numbers

TCP needs to know the order of transmitted data.

Suppose data is split into pieces.

Conceptually:

```text
Piece 1
Piece 2
Piece 3
Piece 4
```

They might travel through the network and arrive like:

```text
Piece 1
Piece 3
Piece 2
Piece 4
```

TCP can use sequence information to reconstruct the proper order:

```text
1
2
3
4
```

---

# TCP Acknowledgments

TCP receivers acknowledge data.

Conceptually:

```text
Sender
   ↓
Data

Receiver
   ↓
ACK
```

The acknowledgment tells the sender that data has been received.

If expected acknowledgment does not arrive, TCP may retransmit data.

---

# Retransmission

Networks are not perfect.

Packets can be:

```text
Lost
Dropped
Corrupted
Delayed
```

TCP is designed to recover from many of these problems.

Example:

```text
Sender
   ↓
Segment 1

Receiver
   ↓
ACK

Sender
   ↓
Segment 2

X Lost

No expected acknowledgment

Sender
   ↓
Segment 2 sent again
```

This is called:

```text
Retransmission
```

---

# TCP Reliability

TCP reliability comes from mechanisms including:

```text
Sequence numbers

Acknowledgments

Retransmission

Connection state
```

This does not mean TCP guarantees that the entire network or application will always work.

It means TCP provides mechanisms designed to detect and recover from certain transmission problems.

---

# UDP

UDP stands for:

```text
User Datagram Protocol
```

UDP is:

```text
Connectionless
```

Unlike TCP, UDP does not establish a connection using the TCP three-way handshake.

It can simply send data.

Conceptually:

```text
Sender
   ↓
UDP Datagram
   ↓
Receiver
```

---

# UDP Mental Model

TCP is like:

```text
Calling someone
Waiting for them to answer
Having a conversation
Confirming information
```

UDP is closer to:

```text
Throwing them a message
and continuing immediately
```

The sender does not automatically require the same level of confirmation from the Transport protocol.

---

# TCP vs UDP

```text
TCP
 |
 +-- Connection-oriented
 +-- Reliable delivery mechanisms
 +-- Sequencing
 +-- Acknowledgments
 +-- Retransmission
```

Compared with:

```text
UDP
 |
 +-- Connectionless
 +-- Lower protocol overhead
 +-- No TCP handshake
 +-- No built-in TCP-style retransmission
 +-- No built-in TCP-style sequencing
```

---

# Why Use UDP?

UDP's simpler design can be useful when:

```text
Low latency matters

Small messages are being exchanged

Applications handle reliability themselves

Old information is less useful than new information
```

Examples of protocols or applications that may use UDP include:

```text
DNS
DHCP
Voice traffic
Streaming
Gaming
```

The exact protocol behavior depends on the application.

---

# Why Use TCP?

TCP is useful when accurate and ordered delivery matters.

Examples commonly include:

```text
HTTP / HTTPS
SSH
FTP
Email protocols
```

If downloading a file, for example:

```text
Missing random pieces
```

would be unacceptable.

TCP's reliability mechanisms help prevent that.

---

# TCP Segment

TCP data is commonly referred to as a:

```text
Segment
```

A simplified TCP header contains information such as:

```text
Source Port

Destination Port

Sequence Number

Acknowledgment Number

Flags
```

Conceptually:

```text
+-------------------------+
| TCP Header              |
|                         |
| Source Port             |
| Destination Port        |
| Sequence Number         |
| ACK Information         |
| Flags                   |
+-------------------------+
| Application Data        |
+-------------------------+
```

---

# UDP Datagram

UDP communication is commonly called a:

```text
Datagram
```

The UDP header is much simpler.

It includes fields such as:

```text
Source Port

Destination Port

Length

Checksum
```

Conceptually:

```text
+-------------------------+
| UDP Header              |
|                         |
| Source Port             |
| Destination Port        |
| Length                  |
| Checksum                |
+-------------------------+
| Application Data        |
+-------------------------+
```

---

# TCP Flags

TCP uses flags to indicate what is happening in a connection.

Important examples include:

```text
SYN
ACK
FIN
RST
```

---

## SYN

Used when establishing a TCP connection.

```text
SYN
↓
Start connection
```

---

## ACK

Indicates acknowledgment.

```text
ACK
↓
Data/control information acknowledged
```

---

## FIN

Used during normal connection termination.

```text
FIN
↓
"I am finished sending."
```

---

## RST

RST stands for:

```text
Reset
```

It indicates that a TCP connection is being abruptly reset or rejected.

---

# Opening and Closing a TCP Connection

Simplified connection lifecycle:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
 ↓
Connection established
 ↓
Data exchanged
 ↓
FIN / ACK process
 ↓
Connection closed
```

---

# Listening Ports

A server application can:

```text
Listen
```

on a port.

Example:

```text
SSH server
    ↓
Listening on port 22
```

This means the operating system is prepared to direct appropriate incoming traffic on that port to the SSH service.

---

# Open vs Closed Ports

A port may commonly be described as:

```text
Open

Closed

Filtered
```

An open port generally means a service is listening and reachable there.

A closed port means the system is reachable but no service is accepting that connection on the port.

A filtered result often means something such as a firewall is preventing a clear response.

---

# Port Does Not Equal Vulnerability

An open port does not automatically mean:

```text
The machine is vulnerable.
```

It means:

```text
A network service is accessible there.
```

The next questions are:

```text
What service is listening?

What version?

How is it configured?

Does it contain a known weakness?
```

---

# Ports and Services

A useful relationship is:

```text
Port
 ↓
Service
 ↓
Software
 ↓
Configuration
 ↓
Possible security exposure
```

This is why identifying ports is often part of network enumeration.

---

# Viewing Connections on Windows

PowerShell provides:

```powershell
Get-NetTCPConnection
```

This can display TCP connection information such as:

```text
LocalAddress
LocalPort
RemoteAddress
RemotePort
State
```

Example mental model:

```text
LocalAddress : LocalPort
          ↓
Connection
          ↓
RemoteAddress : RemotePort
```

---

# Viewing Connections on Linux

A common Linux command is:

```bash
ss -tuln
```

Common flags include:

```text
-t = TCP

-u = UDP

-l = listening

-n = show numeric addresses and ports
```

This can help identify which services are listening.

---

# Wireshark

Wireshark can filter Transport layer traffic.

TCP:

```text
tcp
```

UDP:

```text
udp
```

A specific TCP port:

```text
tcp.port == 443
```

A specific UDP port:

```text
udp.port == 53
```

A TCP handshake can often be observed as:

```text
SYN
SYN-ACK
ACK
```

---

# How This Fits Into Encapsulation

Suppose a browser sends an HTTPS request.

Application data:

```text
HTTPS Data
```

Transport layer adds TCP information:

```text
TCP Header
 |
 +-- Source Port
 +-- Destination Port 443
```

Then the Network layer adds IP information:

```text
IP Header
 |
 +-- Source IP
 +-- Destination IP
 +-- TTL
```

Then Ethernet adds Data Link information:

```text
Ethernet Header
 |
 +-- Source MAC
 +-- Destination MAC
```

So:

```text
Ethernet Frame
      |
      +-- IP Packet
             |
             +-- TCP Segment
                    |
                    +-- Application Data
```

---

# Fast Recognition

If you see:

```text
Port number
```

think:

```text
Transport Layer
```

If you see:

```text
SYN
SYN-ACK
ACK
```

think:

```text
TCP handshake
```

If you see:

```text
Sequence number
Acknowledgment
Retransmission
```

think:

```text
TCP reliability
```

If you see:

```text
Connectionless
```

think:

```text
UDP
```

---

# Engineering Mental Model

When examining network traffic, ask:

```text
Which machine?
      ↓
IP Address

Which application?
      ↓
Port

Which Transport protocol?
      ↓
TCP or UDP

How does that protocol behave?
      ↓
Reliable connection or connectionless delivery
```

Do not memorize:

```text
443 = HTTPS
```

without understanding why the number matters.

The deeper model is:

```text
Machine
   ↓
IP Address
   ↓
Transport Protocol
   ↓
Port
   ↓
Application
```

---

# Key Takeaway

```text
IP Address
=
Which machine?

Port
=
Which service?

TCP
=
Connection-oriented transport with
reliability mechanisms

UDP
=
Connectionless transport with
less built-in overhead
```

The easiest analogy is:

```text
IP Address = Building address

Port = Room inside the building

TCP / UDP = Rules used to deliver
the message to that room
```
