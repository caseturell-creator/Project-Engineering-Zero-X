# Network Layers and Data Units

## Overview

Computer networking is divided into layers so that different parts of communication can perform specific jobs.

Instead of treating network communication as one giant process, each layer is responsible for a different part of moving data between systems.

A useful simplified model is:

```text
Application
    ↓
Transport
    ↓
Network
    ↓
Data Link
    ↓
Physical
```

Each layer adds or processes different information.

---

# Why Network Layers Exist

Network layers separate responsibilities.

For example:

```text
Application Layer
"What application protocol are we using?"

Transport Layer
"Which program or service should receive this?"

Network Layer
"Which machine/network should this travel to?"

Data Link Layer
"Which device should receive this on the local network?"

Physical Layer
"How are the actual bits transmitted?"
```

This separation allows networking technologies to work together without every program needing to understand every part of the network.

---

# Simplified Layer Model

| Layer | Main Responsibility | Common Examples |
|---|---|---|
| Application | Application communication | HTTP, DNS, FTP, SSH |
| Transport | Process-to-process communication | TCP, UDP, Ports |
| Network | Routing between networks | IP, TTL, IP addresses |
| Data Link | Local network delivery | Ethernet, MAC addresses, Frames |
| Physical | Transmission of bits | Cables, radio, electrical signals |

---

# Application Layer

The application layer contains protocols used directly by applications.

Examples include:

```text
HTTP
HTTPS
DNS
FTP
SSH
SMTP
POP3
IMAP
```

These protocols define how applications communicate.

Example:

```text
Browser
   ↓
HTTP
   ↓
Web Server
```

HTTP defines how the browser and web server exchange web requests and responses.

---

# Transport Layer

The transport layer handles communication between processes running on systems.

The two major transport protocols are:

```text
TCP
UDP
```

The transport layer is also where:

```text
Port Numbers
```

belong.

---

## Port Numbers

A port identifies a specific application or service on a machine.

Example:

```text
IP Address
   ↓
Identifies machine

Port
   ↓
Identifies service/process
```

For example:

```text
192.168.1.10:80
```

can be mentally separated as:

```text
192.168.1.10
     ↓
Machine

80
↓
Service
```

Common examples:

```text
HTTP  → 80
HTTPS → 443
SSH   → 22
DNS   → 53
```

Therefore:

```text
Port Numbers = Transport Layer
```

not the Data Link layer.

---

# TCP

TCP stands for:

```text
Transmission Control Protocol
```

TCP provides reliable communication.

It can:

- Track transmitted data
- Detect missing data
- Retransmit missing information
- Maintain ordering
- Establish connections

A simplified flow:

```text
Application Data
      ↓
TCP
      ↓
Segment
```

---

# UDP

UDP stands for:

```text
User Datagram Protocol
```

UDP provides simpler communication without the same reliability mechanisms as TCP.

A simplified flow:

```text
Application Data
      ↓
UDP
      ↓
Datagram
```

UDP is useful when speed or low overhead is more important than guaranteed delivery.

---

# Network Layer

The network layer is responsible for moving packets between networks.

The major protocol here is:

```text
IP
```

IP stands for:

```text
Internet Protocol
```

The network layer handles things such as:

```text
IP addresses
Routing
Packets
TTL
```

---

# IP Addresses

An IP address identifies a system's logical location on a network.

Example:

```text
192.168.1.25
```

Routers examine IP information to determine where packets should travel.

Conceptually:

```text
Packet
   ↓
Destination IP
   ↓
Router
   ↓
Next network
```

---

# TTL

TTL stands for:

```text
Time To Live
```

TTL belongs to the:

```text
Network Layer
```

because TTL is a field inside the IP header.

It does **not** belong to TCP or the Transport layer.

---

## What TTL Does

TTL prevents packets from travelling around networks forever.

Every router that forwards the packet decreases the TTL value.

Example:

```text
TTL = 64
   ↓
Router
   ↓
TTL = 63
   ↓
Router
   ↓
TTL = 62
```

Eventually:

```text
TTL = 0
```

When this happens, the packet is discarded.

This protects networks from routing loops.

---

## TTL Mental Model

```text
Packet starts with TTL
        ↓
Router subtracts 1
        ↓
Router subtracts 1
        ↓
Router subtracts 1
        ↓
TTL reaches 0
        ↓
Packet dies
```

Because routers operate primarily using IP routing:

```text
TTL → IP Header → Network Layer
```

---

# Packets

The main data unit associated with the network layer is the:

```text
Packet
```

A packet contains information such as:

```text
Source IP
Destination IP
TTL
Protocol information
Payload
```

Simplified:

```text
+-----------------------+
| IP Header             |
|                       |
| Source IP             |
| Destination IP        |
| TTL                   |
+-----------------------+
| Data                  |
+-----------------------+
```

---

# Data Link Layer

The Data Link layer handles communication between devices on the local network.

Examples include:

```text
Ethernet
MAC addresses
Frames
```

The main data unit at this layer is:

```text
Frame
```

---

# MAC Addresses

A MAC address identifies a network interface on the local network.

Example structure:

```text
AA:BB:CC:DD:EE:FF
```

The distinction is important:

```text
IP Address
     ↓
Logical network location

MAC Address
     ↓
Local network interface
```

Routers care mainly about IP addresses.

Ethernet communication on the local network uses MAC addresses.

---

# Frames

At the Data Link layer, network data is carried inside:

```text
Frames
```

A simplified Ethernet frame contains:

```text
Destination MAC
Source MAC
EtherType
Payload
Error checking information
```

Conceptually:

```text
+------------------------+
| Ethernet Header        |
|                        |
| Destination MAC        |
| Source MAC             |
+------------------------+
| IP Packet              |
+------------------------+
| Trailer                |
+------------------------+
```

---

# Frame Arrival

When a network interface receives an Ethernet frame, processing initially occurs at the:

```text
Data Link Layer
```

The system checks information such as the destination MAC address.

If the frame belongs to the device:

```text
Frame
  ↓
Data Link Layer
  ↓
Ethernet header removed
  ↓
IP packet passed upward
```

Therefore:

```text
Frame arrival → Data Link Layer
```

---

# Physical Layer

The Physical layer is responsible for transmitting raw bits.

Examples include:

```text
Electrical signals
Fiber optic light
Wi-Fi radio signals
Ethernet cables
```

At this level, the network data is ultimately represented as:

```text
Bits
```

Example:

```text
1011010010100110
```

The Physical layer does not understand HTTP, ports, IP addresses, or MAC addresses.

Its job is transmission.

---

# Protocol Data Units

Each layer has a different name for the data it handles.

A simplified mapping is:

```text
Application
    ↓
Data

Transport
    ↓
Segment / Datagram

Network
    ↓
Packet

Data Link
    ↓
Frame

Physical
    ↓
Bits
```

---

# Encapsulation

As data moves down the networking stack, each layer adds information.

This process is called:

```text
Encapsulation
```

Example:

```text
HTTP Data
    ↓
TCP Header added
    ↓
TCP Segment
    ↓
IP Header added
    ↓
IP Packet
    ↓
Ethernet Header added
    ↓
Ethernet Frame
    ↓
Bits transmitted
```

Visually:

```text
Application Data

        ↓

+------------------+
| TCP              |
| Application Data |
+------------------+

        ↓

+------------------+
| IP               |
| TCP              |
| Application Data |
+------------------+

        ↓

+------------------+
| Ethernet         |
| IP               |
| TCP              |
| Application Data |
+------------------+
```

---

# Decapsulation

The receiving system performs the reverse process.

```text
Bits received
    ↓
Frame
    ↓
Packet
    ↓
Segment
    ↓
Application Data
```

Each layer removes and processes its own information.

Example:

```text
Ethernet examines MAC information

        ↓

IP examines IP information

        ↓

TCP examines ports

        ↓

Application receives data
```

This is called:

```text
Decapsulation
```

---

# One Communication Example

Imagine a browser connecting to a website.

```text
Browser creates HTTP request
        ↓
Application Layer
HTTP
        ↓
Transport Layer
TCP + destination port 443
        ↓
Network Layer
IP + destination IP + TTL
        ↓
Data Link Layer
Ethernet + destination MAC
        ↓
Physical Layer
Bits transmitted
```

The receiver performs the reverse process.

---

# How to Identify the Layer

When looking at a networking question, identify the object being discussed.

## MAC Address

Think:

```text
MAC
↓
Ethernet
↓
Data Link
```

---

## Frame

Think:

```text
Frame
↓
Data Link
```

---

## IP Address

Think:

```text
IP
↓
Network Layer
```

---

## TTL

Think:

```text
TTL
↓
IP Header
↓
Network Layer
```

---

## Port Number

Think:

```text
Port
↓
TCP / UDP
↓
Transport Layer
```

---

## TCP or UDP

Think:

```text
TCP / UDP
↓
Transport Layer
```

---

## HTTP, FTP, SSH or DNS

Think:

```text
Application Protocol
↓
Application Layer
```

---

# Fast Recognition Table

| You See | Think |
|---|---|
| MAC Address | Data Link |
| Ethernet | Data Link |
| Frame | Data Link |
| IP Address | Network |
| Router | Network |
| Packet | Network |
| TTL | Network |
| TCP | Transport |
| UDP | Transport |
| Port | Transport |
| Segment | Transport |
| HTTP | Application |
| FTP | Application |
| SSH | Application |
| DNS | Application |

---

# Common Confusions

## TTL vs Transport Layer

Incorrect:

```text
TTL → Transport
```

Correct:

```text
TTL
 ↓
IP Header
 ↓
Network Layer
```

---

## Ports vs Data Link Layer

Incorrect:

```text
Port → Data Link
```

Correct:

```text
Port
 ↓
TCP / UDP
 ↓
Transport Layer
```

---

## Frames vs Packets

These are not two names for the same thing.

```text
Frame
↓
Data Link Layer
```

while:

```text
Packet
↓
Network Layer
```

The packet is carried **inside** the frame.

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

# Engineering Mental Model

Do not memorize the layers as isolated vocabulary.

Ask:

```text
What information am I looking at?
```

Then trace who owns it.

Example:

```text
TTL
 ↓
Where is TTL stored?
 ↓
IP header
 ↓
Who owns IP?
 ↓
Network Layer
```

Another example:

```text
Port 443
 ↓
Who uses ports?
 ↓
TCP / UDP
 ↓
Transport Layer
```

Another:

```text
Destination MAC
 ↓
Who uses MAC addresses?
 ↓
Ethernet
 ↓
Data Link Layer
```

This is more reliable than memorizing random layer numbers.

---

# Key Takeaway

```text
Application = protocols applications use

Transport = TCP, UDP, ports

Network = IP, routing, TTL, packets

Data Link = Ethernet, MAC addresses, frames

Physical = bits and signals
```

The easiest way to understand networking layers is to follow the data:

```text
Application Data
      ↓
Segment
      ↓
Packet
      ↓
Frame
      ↓
Bits
```

and then reverse the process when the destination receives it:

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment
 ↓
Application Data
```
