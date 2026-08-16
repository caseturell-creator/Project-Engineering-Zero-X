# ARP and Local Network Resolution

## Overview

ARP stands for:

```text
Address Resolution Protocol
```

ARP is used on IPv4 local networks to determine which MAC address belongs to a known IP address.

The basic problem ARP solves is:

```text
I know the destination IP address.

But Ethernet needs a destination MAC address.

How do I find it?
```

ARP provides the answer.

---

# The Core Problem

IP communication uses:

```text
IP addresses
```

Ethernet communication on the local network uses:

```text
MAC addresses
```

Before a device can send an Ethernet frame to another local device, it needs to know the destination MAC address.

Example:

```text
Computer A wants to communicate with:

192.168.1.20
```

Computer A may know the IP address:

```text
192.168.1.20
```

but not the MAC address.

ARP is used to discover it.

---

# Basic ARP Workflow

The process looks like this:

```text
Known:

Destination IP

Unknown:

Destination MAC
```

The sender asks:

```text
Who has this IP address?
```

The device owning that IP responds:

```text
That IP belongs to my MAC address.
```

Then communication can continue.

---

# ARP Request

An ARP request asks which device owns a particular IPv4 address.

Conceptually:

```text
Computer A

"Who has 192.168.1.20?"
```

Computer A does not yet know which specific MAC address should receive the question.

Because of this, the ARP request is sent as a:

```text
Broadcast
```

---

# Broadcast MAC Address

The Ethernet broadcast address is:

```text
FF:FF:FF:FF:FF:FF
```

This means:

```text
Send this frame to every device on the local network segment.
```

Example:

```text
Source MAC:
AA:AA:AA:AA:AA:AA

Destination MAC:
FF:FF:FF:FF:FF:FF
```

Every local device can receive the request.

---

# ARP Request Example

Suppose:

```text
Computer A

IP:
192.168.1.10

MAC:
AA:AA:AA:AA:AA:AA
```

wants to contact:

```text
Computer B

IP:
192.168.1.20

MAC:
BB:BB:BB:BB:BB:BB
```

Computer A knows:

```text
192.168.1.20
```

but does not know:

```text
BB:BB:BB:BB:BB:BB
```

It sends:

```text
ARP Request

Who has 192.168.1.20?

Tell 192.168.1.10
```

The Ethernet frame is addressed to:

```text
FF:FF:FF:FF:FF:FF
```

---

# ARP Reply

Computer B sees that the requested IP belongs to it.

It responds with an:

```text
ARP Reply
```

The reply essentially says:

```text
192.168.1.20 is at BB:BB:BB:BB:BB:BB
```

Unlike the original request, the reply can normally be sent directly back to Computer A.

Conceptually:

```text
Computer A
   |
   | ARP Broadcast
   |
   | "Who has 192.168.1.20?"
   v

Local Network

   |
   v

Computer B
192.168.1.20

   |
   | ARP Reply
   |
   | "192.168.1.20 is at
   |  BB:BB:BB:BB:BB:BB"
   v

Computer A
```

---

# After ARP Resolution

Computer A now knows:

```text
IP:
192.168.1.20

MAC:
BB:BB:BB:BB:BB:BB
```

It can construct an Ethernet frame:

```text
Destination MAC:
BB:BB:BB:BB:BB:BB
```

containing the IP packet intended for:

```text
192.168.1.20
```

So the full process becomes:

```text
Know destination IP
        ↓
Need destination MAC
        ↓
ARP Request
        ↓
ARP Reply
        ↓
MAC discovered
        ↓
Ethernet frame created
        ↓
Communication continues
```

---

# ARP Cache

Devices do not normally perform a new ARP request for every packet.

After discovering the IP-to-MAC relationship, the operating system temporarily stores it in an:

```text
ARP Cache
```

Example:

```text
IP Address       MAC Address
192.168.1.1      11:22:33:44:55:66
192.168.1.20     BB:BB:BB:BB:BB:BB
192.168.1.30     CC:CC:CC:CC:CC:CC
```

This allows future traffic to use the known MAC address without repeating ARP immediately.

---

# Why ARP Entries Expire

ARP cache entries are not permanent.

Network conditions can change.

For example:

```text
Device disconnected

Network card replaced

IP reassigned

DHCP gives address to another device
```

If old ARP information remained forever, a device could continue sending frames to the wrong MAC address.

Therefore ARP entries normally expire and can be learned again.

---

# Viewing the ARP Cache

## Windows

A common command is:

```powershell
arp -a
```

Example output:

```text
Internet Address      Physical Address
192.168.1.1           11-22-33-44-55-66
192.168.1.20          bb-bb-bb-bb-bb-bb
```

PowerShell can also display neighbor information using:

```powershell
Get-NetNeighbor
```

---

## Linux

A common modern command is:

```bash
ip neigh
```

Example structure:

```text
192.168.1.1 dev eth0 lladdr 11:22:33:44:55:66 REACHABLE
```

Older systems may also support:

```bash
arp -a
```

---

# ARP and the Data Link Layer

ARP sits between the concepts of:

```text
IP addressing
```

and:

```text
Ethernet addressing
```

It exists because the local Ethernet network needs a MAC address while the higher-level communication is based on an IP address.

A useful mental model is:

```text
Network Layer

IP Address
    ↓

ARP

"Which MAC belongs to this IP?"

    ↓

Data Link Layer

MAC Address
```

---

# ARP Does Not Find Remote MAC Addresses

This is extremely important.

ARP only resolves addresses on the local network.

Suppose:

```text
Your computer:
192.168.1.10

Website:
142.250.x.x
```

The website is not on your local Ethernet network.

Your computer does NOT ARP for the website's MAC address.

Instead, it sends the frame to the MAC address of its:

```text
Default Gateway
```

---

# Communication With a Remote Network

Suppose:

```text
Computer:
192.168.1.10

Gateway:
192.168.1.1

Remote Server:
8.8.8.8
```

The computer determines:

```text
8.8.8.8 is not on my local subnet.
```

Therefore it sends the packet toward the router.

But to send an Ethernet frame to the router, it needs the router's MAC address.

So ARP is used for:

```text
192.168.1.1
```

not:

```text
8.8.8.8
```

Conceptually:

```text
Destination IP:
8.8.8.8

        ↓

Is destination local?

        ↓

No

        ↓

Send toward default gateway

        ↓

Need gateway MAC address

        ↓

ARP for 192.168.1.1

        ↓

Gateway MAC discovered
```

---

# IP Destination vs MAC Destination

When communicating with a remote server, the addresses can look like this:

```text
IP Header:

Source IP:
192.168.1.10

Destination IP:
8.8.8.8
```

while the Ethernet frame might contain:

```text
Ethernet Header:

Source MAC:
Computer MAC

Destination MAC:
Router MAC
```

The important distinction is:

```text
IP destination
=
Final network destination

MAC destination
=
Next local hop
```

---

# Routers Change the Frame

A router receives the Ethernet frame.

It removes the old Ethernet framing and examines the IP packet.

Then it creates a new frame for the next network connection.

Conceptually:

```text
Computer
   ↓

Ethernet Frame

Destination MAC:
Router

Inside:

IP Packet
Destination IP:
Remote Server

   ↓

Router
   ↓

Old Ethernet frame removed

   ↓

IP packet examined

   ↓

New Ethernet frame created

   ↓

Next hop
```

The IP packet is routed toward the destination while Layer 2 addressing changes from link to link.

---

# ARP Request vs ARP Reply

## ARP Request

Usually:

```text
Broadcast
```

Meaning:

```text
Everyone on the local network receives it.
```

Example:

```text
Who has 192.168.1.20?
```

Destination MAC:

```text
FF:FF:FF:FF:FF:FF
```

---

## ARP Reply

Usually:

```text
Unicast
```

Meaning:

```text
Sent directly to the requesting device.
```

Example:

```text
192.168.1.20 is at BB:BB:BB:BB:BB:BB
```

---

# Broadcast vs Unicast

## Broadcast

One sender communicates with every device on the local broadcast domain.

```text
One
 ↓
Everyone
```

ARP requests commonly use this.

---

## Unicast

One sender communicates directly with one destination.

```text
One
 ↓
One
```

ARP replies commonly use this.

---

# ARP in Wireshark

ARP traffic can be filtered in Wireshark using:

```text
arp
```

A typical ARP request may appear similar to:

```text
Who has 192.168.1.1? Tell 192.168.1.10
```

A reply may appear similar to:

```text
192.168.1.1 is at 11:22:33:44:55:66
```

This allows the ARP discovery process to be observed directly.

---

# What ARP Actually Resolves

ARP does not resolve:

```text
Domain name → IP address
```

That is primarily the job of:

```text
DNS
```

ARP resolves:

```text
IPv4 address → MAC address
```

So:

```text
DNS
example.com
     ↓
IP address
```

while:

```text
ARP
IP address
     ↓
MAC address
```

These are completely different resolution processes.

---

# DNS vs ARP

| Protocol | Resolves |
|---|---|
| DNS | Name → IP |
| ARP | IPv4 Address → MAC |

Example:

```text
www.example.com
      ↓
DNS
      ↓
93.184.216.34
```

Then, depending on whether the destination is local:

```text
Local destination
      ↓
ARP for destination
```

or:

```text
Remote destination
      ↓
ARP for default gateway
```

---

# ARP and Switches

ARP and Ethernet operate on the local network where switches forward Ethernet frames.

A switch mainly makes forwarding decisions using:

```text
MAC addresses
```

The switch does not perform the same job as ARP.

ARP determines:

```text
Which MAC belongs to an IP?
```

The switch determines:

```text
Which physical switch port should receive a frame for that MAC?
```

Conceptually:

```text
ARP
IP → MAC

Switch MAC Table
MAC → Switch Port
```

---

# ARP Table vs Switch MAC Table

These are often confused.

## ARP Table

Stored by hosts and routers.

Maps:

```text
IP Address
    ↓
MAC Address
```

---

## Switch MAC Table

Stored by Ethernet switches.

Maps:

```text
MAC Address
    ↓
Physical Switch Port
```

So:

```text
ARP Table

192.168.1.20
      ↓
BB:BB:BB:BB:BB:BB
```

while:

```text
Switch Table

BB:BB:BB:BB:BB:BB
      ↓
Port 4
```

---

# Full Local Communication Example

Suppose:

```text
Computer A

IP:
192.168.1.10

MAC:
AA:AA:AA:AA:AA:AA
```

wants to contact:

```text
Computer B

IP:
192.168.1.20

MAC:
BB:BB:BB:BB:BB:BB
```

Computer A checks its ARP cache.

```text
Is 192.168.1.20 already known?
```

If no:

```text
ARP Request
      ↓
Broadcast
      ↓
Who has 192.168.1.20?
```

Computer B responds:

```text
ARP Reply
      ↓
192.168.1.20 =
BB:BB:BB:BB:BB:BB
```

Computer A stores the result:

```text
192.168.1.20
        ↓
BB:BB:BB:BB:BB:BB
```

Then Computer A can send:

```text
Ethernet Frame

Destination MAC:
BB:BB:BB:BB:BB:BB

        ↓

IP Packet

Destination IP:
192.168.1.20
```

---

# Full Remote Communication Example

Suppose:

```text
Computer:
192.168.1.10

Gateway:
192.168.1.1

Remote Server:
8.8.8.8
```

The computer checks whether:

```text
8.8.8.8
```

belongs to its local subnet.

It does not.

Therefore:

```text
Final IP destination:
8.8.8.8

Next local destination:
192.168.1.1
```

The computer resolves:

```text
192.168.1.1
      ↓
ARP
      ↓
Gateway MAC
```

Then creates:

```text
Ethernet Frame

Destination MAC:
Gateway MAC

Inside:

IP Packet

Destination IP:
8.8.8.8
```

This is one of the most important networking distinctions:

```text
The MAC address gets the frame to the next local hop.

The IP address gets the packet toward the final destination.
```

---

# IPv6 Note

ARP is associated with:

```text
IPv4
```

IPv6 does not use ARP in the same way.

IPv6 uses:

```text
Neighbor Discovery Protocol
```

or:

```text
NDP
```

for similar neighbor-discovery functions.

So:

```text
IPv4
 ↓
ARP
```

while:

```text
IPv6
 ↓
NDP
```

---

# Security Relevance

ARP was designed for local network communication and does not inherently provide strong authentication.

A device can potentially send false ARP information and attempt to convince another system that:

```text
A certain IP address
```

belongs to:

```text
A different MAC address
```

This type of manipulation is commonly associated with:

```text
ARP spoofing
```

or:

```text
ARP poisoning
```

Understanding normal ARP behavior is necessary before understanding how those attacks work or how networks defend against them.

---

# Fast Recognition

If you see:

```text
Who has 192.168.x.x?
```

think:

```text
ARP Request
```

If you see:

```text
192.168.x.x is at AA:BB:CC:DD:EE:FF
```

think:

```text
ARP Reply
```

If you see:

```text
FF:FF:FF:FF:FF:FF
```

think:

```text
Ethernet Broadcast
```

If you see:

```text
IP → MAC
```

think:

```text
ARP
```

---

# Engineering Mental Model

Do not memorize ARP as:

```text
ARP finds MAC addresses.
```

Understand the problem it solves:

```text
Applications communicate using higher-level protocols.

        ↓

IP identifies the destination system.

        ↓

But Ethernet needs a local destination MAC.

        ↓

The system checks whether it already knows the MAC.

        ↓

If not, ARP asks the local network.

        ↓

The owner of the IP responds.

        ↓

The IP-to-MAC mapping is cached.

        ↓

Ethernet communication can proceed.
```

ARP is the bridge between:

```text
Logical addressing
```

and:

```text
Local physical/interface addressing
```

in an IPv4 Ethernet network.

---

# Key Commands

## Windows

```powershell
arp -a
```

Displays the ARP cache.

```powershell
Get-NetNeighbor
```

Displays IP neighbor information.

---

## Linux

```bash
ip neigh
```

Displays the neighbor table.

```bash
arp -a
```

May also display ARP information on systems where the older utility is installed.

---

## Wireshark

```text
arp
```

Filters the packet capture to ARP traffic.

---

# Key Takeaway

```text
ARP = IPv4 address → MAC address
```

For a local destination:

```text
ARP resolves the destination device.
```

For a remote destination:

```text
ARP resolves the default gateway.
```

And the most important distinction is:

```text
IP Address
=
Where the packet ultimately needs to go

MAC Address
=
Where the Ethernet frame needs to go next
```

That is why ARP is necessary.
