# Network Layer Recognition Chart

## Purpose

This chart is for quickly identifying which networking layer owns a protocol, address, field, or data unit.

The goal is:

```text
See the clue
    ↓
Recognize who owns it
    ↓
Identify the layer
```

---

# Main Recognition Chart

| Layer | Name | Main Job | Things to Recognize |
|---|---|---|---|
| 7 | Application | Application communication | HTTP, HTTPS, DNS, FTP, SSH, SMTP, POP3, IMAP |
| 6 | Presentation | Representation / encoding / encryption concepts | Encoding, serialization, encryption concepts |
| 5 | Session | Managing communication sessions | Session establishment/management concepts |
| 4 | Transport | Process-to-process delivery | TCP, UDP, ports, segments, datagrams |
| 3 | Network | Routing between networks | IPv4, IPv6, IP addresses, packets, routers, TTL, ICMP |
| 2 | Data Link | Local link delivery | Ethernet, MAC addresses, frames, switches, ARP |
| 1 | Physical | Raw transmission | Bits, cables, radio, electrical/optical signals |

---

# Fast Recognition

```text
HTTP / HTTPS / DNS / FTP / SSH
                ↓
          Application
            Layer 7
```

```text
TCP / UDP / Port Number
            ↓
       Transport
        Layer 4
```

```text
IP Address / TTL / Packet / ICMP
                ↓
             Network
             Layer 3
```

```text
MAC Address / Ethernet / Frame / ARP
                ↓
             Data Link
              Layer 2
```

```text
Bits / Cable / Radio / Electrical Signal
                ↓
             Physical
              Layer 1
```

---

# Layer 1 — Physical

Think:

```text
Actual transmission medium
```

Examples:

```text
Bits

Electrical signals

Fiber-optic light

Wi-Fi radio waves

Ethernet cable
```

Data unit:

```text
Bits
```

Important:

```text
A FRAME is not Layer 1.

The physical signals carrying the frame are Layer 1.
```

---

# Layer 2 — Data Link

Think:

```text
Local network delivery
```

Examples:

```text
Ethernet

MAC addresses

Frames

Switches

ARP
```

Data unit:

```text
Frame
```

---

# MAC Address

```text
MAC
 ↓
Ethernet
 ↓
Data Link
 ↓
Layer 2
```

Example:

```text
AA:BB:CC:DD:EE:FF
```

---

# Frame

```text
Frame
 ↓
Ethernet
 ↓
Data Link
 ↓
Layer 2
```

Important:

```text
Frame = Layer 2
```

not:

```text
Layer 1
```

---

# ARP

ARP connects:

```text
Known IPv4 address
        ↓
Find MAC address
```

It operates for local-link resolution and is normally associated with:

```text
Layer 2 / link-layer operation
```

Mental model:

```text
IP → MAC
```

---

# Layer 3 — Network

Think:

```text
Where does the packet need to go?
```

Examples:

```text
IPv4

IPv6

IP addresses

Routers

Packets

TTL

ICMP
```

Data unit:

```text
Packet
```

---

# IP Address

```text
IP Address
    ↓
Network location
    ↓
Layer 3
```

---

# TTL

TTL stands for:

```text
Time To Live
```

TTL is stored inside the:

```text
IP header
```

Therefore:

```text
TTL
 ↓
IP
 ↓
Network Layer
 ↓
Layer 3
```

Not:

```text
Transport Layer
```

---

# Router

Routers primarily make forwarding decisions using:

```text
IP information
```

Therefore:

```text
Router
 ↓
Network Layer
 ↓
Layer 3
```

---

# ICMP

Examples:

```text
Ping

Echo Request

Echo Reply

Time Exceeded

Destination Unreachable
```

Recognition:

```text
ICMP
 ↓
Network-control behavior
 ↓
Layer 3
```

---

# Layer 4 — Transport

Think:

```text
Which application/process should receive the data?
```

Examples:

```text
TCP

UDP

Ports

TCP segments

UDP datagrams
```

---

# Port Number

```text
Port
 ↓
TCP / UDP
 ↓
Transport
 ↓
Layer 4
```

Examples:

```text
22
53
80
443
```

Important:

```text
Port numbers do NOT belong to Data Link.
```

---

# TCP

Recognition clues:

```text
SYN

SYN-ACK

ACK

FIN

RST

Sequence number

Acknowledgment number

Port
```

All point toward:

```text
TCP
 ↓
Transport
 ↓
Layer 4
```

---

# UDP

Recognition clues:

```text
UDP

Source port

Destination port

Datagram
```

point toward:

```text
Transport
 ↓
Layer 4
```

---

# Layer 7 — Application

Examples:

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

These define how applications communicate.

Example:

```text
Browser
   ↓
HTTP
   ↓
Web Server
```

---

# HTTPS Note

HTTPS combines technologies.

At a practical recognition level:

```text
HTTPS
 ↓
Application communication
 ↓
Layer 7
```

TLS handles encryption underneath the HTTP application exchange.

Real protocol stacks do not always map perfectly to every OSI layer.

The layer model is an abstraction used to reason about responsibilities.

---

# Encapsulation Chart

```text
Application Data
      ↓
Layer 4
TCP Segment / UDP Datagram
      ↓
Layer 3
IP Packet
      ↓
Layer 2
Ethernet Frame
      ↓
Layer 1
Bits / Signals
```

---

# Decapsulation

Receiving side:

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment / Datagram
 ↓
Application Data
```

---

# Nesting Mental Model

```text
Ethernet Frame
│
└── IP Packet
    │
    └── TCP Segment
        │
        └── HTTP Data
```

So:

```text
HTTP
inside TCP

TCP
inside IP

IP
inside Ethernet
```

---

# Address Mental Model

```text
MAC Address
=
Next local destination
```

```text
IP Address
=
Logical/final network destination
```

```text
Port
=
Application/service on that machine
```

A useful analogy:

```text
IP Address
=
Building address

Port
=
Room inside the building

MAC Address
=
How the local delivery actually reaches
the next device on this network
```

---

# Wireshark Recognition

When looking inside Wireshark:

```text
Ethernet II
 ↓
Layer 2
```

```text
Internet Protocol Version 4
 ↓
Layer 3
```

```text
Transmission Control Protocol
 ↓
Layer 4
```

```text
Hypertext Transfer Protocol
 ↓
Layer 7
```

---

# Important Wireshark "Frame" Note

Wireshark often displays a top section called:

```text
Frame
```

containing values such as:

```text
Arrival Time

Frame Length

Capture Length

Protocols in frame
```

This Wireshark section is:

```text
capture metadata
```

It should NOT be treated as proof that:

```text
Arrival Time = OSI Layer 1
```

`Arrival Time` is information recorded by the packet-capture system about when the frame was observed.

Meanwhile:

```text
Ethernet Frame
=
Layer 2
```

and:

```text
Physical signals carrying it
=
Layer 1
```

This distinction prevents mixing Wireshark metadata with actual protocol-layer fields.

---

# Data Unit Chart

| Layer | Data Unit |
|---|---|
| 7 Application | Data |
| 4 Transport | Segment / Datagram |
| 3 Network | Packet |
| 2 Data Link | Frame |
| 1 Physical | Bits |

---

# Device Chart

| Device | Main Layer Association |
|---|---|
| Hub / repeater | Layer 1 |
| Switch | Layer 2 |
| Router | Layer 3 |

Modern devices can perform additional functions, but these are the basic recognition mappings.

---

# Question → Layer

If the question mentions:

```text
MAC address
```

answer:

```text
Layer 2 — Data Link
```

If it mentions:

```text
Frame
```

answer:

```text
Layer 2 — Data Link
```

If it mentions:

```text
IP address
```

answer:

```text
Layer 3 — Network
```

If it mentions:

```text
TTL
```

answer:

```text
Layer 3 — Network
```

If it mentions:

```text
Port number
```

answer:

```text
Layer 4 — Transport
```

If it mentions:

```text
TCP / UDP
```

answer:

```text
Layer 4 — Transport
```

If it mentions:

```text
HTTP / FTP / DNS
```

answer:

```text
Layer 7 — Application
```

---

# Fastest Mental Model

```text
Signal
 ↓
1 Physical

MAC / Frame
 ↓
2 Data Link

IP / TTL / Packet
 ↓
3 Network

TCP / UDP / Port
 ↓
4 Transport

HTTP / DNS / FTP / SSH
 ↓
7 Application
```

---

# Engineering Takeaway

Instead of memorizing seven isolated layers, ask:

```text
What object am I looking at?
```

Then:

```text
Who owns that object?
```

Example:

```text
TTL
 ↓
Stored in IP header
 ↓
IP belongs to Network layer
 ↓
Layer 3
```

Example:

```text
Port 443
 ↓
Port belongs to TCP/UDP
 ↓
TCP/UDP belong to Transport
 ↓
Layer 4
```

Example:

```text
Destination MAC
 ↓
Ethernet uses MAC addresses
 ↓
Ethernet belongs to Data Link
 ↓
Layer 2
```

That reasoning is more reliable than memorizing random numbers.
