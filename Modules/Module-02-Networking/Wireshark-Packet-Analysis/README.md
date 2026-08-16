# Wireshark Packet Analysis

## Overview

Wireshark is a network protocol analyzer.

It captures network traffic and allows individual packets and protocol fields to be inspected.

Instead of only seeing:

```text
"The network worked"
```

Wireshark lets us inspect:

```text
What was sent?

Who sent it?

Where was it going?

Which protocol was used?

Which ports were involved?

What information was inside the packet?

What happened before and after it?
```

Wireshark turns network communication into observable evidence.

---

# Core Mental Model

A network conversation can contain thousands of packets.

The goal is not:

```text
Click random packets until something looks useful.
```

The better process is:

```text
Question
   ↓
What evidence would answer it?
   ↓
Which protocol contains that evidence?
   ↓
Filter the capture
   ↓
Locate the relevant packet
   ↓
Inspect the correct protocol field
   ↓
Confirm the answer
```

This is much faster than visually searching an entire capture.

---

# Your Evidence-Room Mental Model

Think of a Wireshark capture like a giant evidence room.

```text
Capture File
    ↓
Thousands of pieces of evidence
```

Every packet is another item.

The wrong approach is:

```text
Open every box one at a time.
```

The better approach is:

```text
Know what evidence you need
        ↓
Narrow the evidence set
        ↓
Open only the relevant boxes
        ↓
Inspect the exact detail
```

Wireshark filters are what make that possible.

---

# The Wireshark Interface

Wireshark is mainly divided into three important areas.

```text
Packet List
    ↓
Packet Details
    ↓
Packet Bytes
```

---

# Packet List

The top section displays captured packets.

Common columns include:

```text
No.
Time
Source
Destination
Protocol
Length
Info
```

Example:

```text
No.   Source        Destination   Protocol   Info

38    10.0.0.5      10.0.0.10     HTTP       GET /index.html
```

---

## Packet Number

The:

```text
No.
```

column is the packet's position inside the capture.

Example:

```text
Packet 38
```

means:

```text
The 38th captured packet
```

It does NOT mean:

```text
Port 38

Protocol 38

38 packets total
```

The packet number is simply an index into the capture.

---

# Packet Details

Selecting a packet displays its protocol structure.

Example:

```text
Frame
  ↓
Ethernet II
  ↓
Internet Protocol Version 4
  ↓
Transmission Control Protocol
  ↓
Hypertext Transfer Protocol
```

Each section corresponds to another layer of encapsulation.

---

# Packet Details and Network Layers

A packet may appear as:

```text
Frame
 |
 +-- Ethernet
 |
 +-- IPv4
 |
 +-- TCP
 |
 +-- HTTP
```

This matches the networking model:

```text
Data Link
    ↓
Network
    ↓
Transport
    ↓
Application
```

---

# Frame Section

The `Frame` section contains information about the captured frame itself.

This can include:

```text
Arrival time

Frame length

Capture length

Protocols contained inside
```

This is information about how Wireshark captured the network data.

---

# Ethernet Section

The Ethernet section contains Data Link information.

Important fields can include:

```text
Source MAC Address

Destination MAC Address

EtherType
```

Mental model:

```text
Ethernet
   ↓
Local delivery
   ↓
MAC addresses
```

---

# IPv4 Section

The IPv4 section contains Network layer information.

Important fields can include:

```text
Source IP

Destination IP

TTL

Protocol
```

Example:

```text
Internet Protocol Version 4

Source Address: 192.168.1.10
Destination Address: 192.168.1.20
Time to Live: 64
```

---

# Finding TTL

TTL belongs inside the IP header.

So when looking for TTL:

```text
Packet
  ↓
Internet Protocol Version 4
  ↓
Time to Live
```

Mental model:

```text
TTL
 ↓
IP Header
 ↓
Network Layer
```

---

# TCP Section

The TCP section contains Transport layer information.

Important fields include:

```text
Source Port

Destination Port

Sequence Number

Acknowledgment Number

TCP Flags
```

Example:

```text
Transmission Control Protocol

Source Port: 53124
Destination Port: 80
```

Mental model:

```text
TCP
 ↓
Ports
 ↓
Transport Layer
```

---

# HTTP Section

When HTTP traffic is present, Wireshark may decode application information.

Examples include:

```text
GET requests

POST requests

Host headers

Response codes

Content types

HTML content
```

Example:

```text
GET /index.html HTTP/1.1
Host: example.com
```

---

# Packet Bytes

The bottom section displays the raw packet bytes.

These are commonly shown as:

```text
Hexadecimal
```

alongside:

```text
ASCII
```

Example structure:

```text
0000  45 00 00 3c ...
0010  c0 a8 01 0a ...
```

This is the actual byte-level representation of the packet.

---

# Hexadecimal

Network tools frequently display data using hexadecimal.

Hexadecimal uses:

```text
0-9
A-F
```

Each hexadecimal digit represents:

```text
4 bits
```

Two hexadecimal digits represent:

```text
1 byte
```

Example:

```text
FF
```

represents one byte.

---

# Selecting Fields

When a protocol field is selected in the Packet Details panel, Wireshark highlights the corresponding bytes below.

Conceptually:

```text
Human-readable field
        ↓
Exact raw bytes that represent it
```

This connects:

```text
Protocol abstraction
```

with:

```text
Actual transmitted data
```

---

# Capture Filters vs Display Filters

Wireshark has two different kinds of filters.

```text
Capture Filters
```

and:

```text
Display Filters
```

They are not the same thing.

---

# Capture Filters

Capture filters decide:

```text
What traffic gets recorded?
```

They are applied while capturing traffic.

Traffic that does not match the capture filter may never be stored in the capture.

---

# Display Filters

Display filters decide:

```text
Which already-captured packets are shown?
```

The packets remain inside the capture.

Wireshark simply hides packets that do not match the filter.

Mental model:

```text
Capture Filter
=
Which evidence enters the evidence room

Display Filter
=
Which evidence boxes are currently visible
```

---

# Display Filter Bar

The filter bar near the top of Wireshark allows display filters to be entered.

Example:

```text
http
```

This displays packets decoded as HTTP.

---

# Common Display Filters

## HTTP

```text
http
```

Shows HTTP traffic.

---

## TCP

```text
tcp
```

Shows TCP traffic.

---

## UDP

```text
udp
```

Shows UDP traffic.

---

## DNS

```text
dns
```

Shows DNS traffic.

---

## ARP

```text
arp
```

Shows ARP traffic.

---

## ICMP

```text
icmp
```

Shows ICMP traffic.

---

# Filtering by IP Address

Example:

```text
ip.addr == 192.168.1.10
```

This matches packets where the address appears as either:

```text
Source

or

Destination
```

---

# Source IP Only

```text
ip.src == 192.168.1.10
```

---

# Destination IP Only

```text
ip.dst == 192.168.1.10
```

---

# Filtering by TCP Port

Example:

```text
tcp.port == 80
```

This finds TCP traffic using port:

```text
80
```

as either source or destination.

---

# Filtering by UDP Port

Example:

```text
udp.port == 53
```

This can help isolate DNS traffic using UDP port 53.

---

# Combining Filters

Filters can be combined using logical operators.

Example:

```text
http && ip.addr == 192.168.1.10
```

Meaning:

```text
Show HTTP traffic
AND
traffic involving this IP address
```

Another example:

```text
tcp.port == 443 && ip.dst == 192.168.1.20
```

---

# Logical Operators

Common operators include:

```text
&&
```

Meaning:

```text
AND
```

---

```text
||
```

Meaning:

```text
OR
```

---

```text
!
```

Meaning:

```text
NOT
```

---

# Filter Mental Model

Do not think:

```text
"What filter am I supposed to memorize?"
```

Ask:

```text
What traffic do I want to see?
```

Then convert the question into conditions.

Example:

```text
I need HTTP traffic
from this particular machine.
```

becomes:

```text
http && ip.src == <address>
```

The filter is just the question translated into Wireshark syntax.

---

# Applying Filters From Packet Fields

Wireshark can build filters directly from selected protocol fields.

A field can often be:

```text
Right-clicked
```

and used with options such as:

```text
Apply as Filter
```

This is useful when the exact display-filter syntax is not remembered.

The important skill is still understanding:

```text
Which field you want to isolate.
```

---

# Follow Stream

Individual packets are pieces of a larger conversation.

Wireshark can reconstruct certain conversations using:

```text
Follow Stream
```

For TCP traffic:

```text
Follow
   ↓
TCP Stream
```

For HTTP traffic, depending on the capture and Wireshark version, related stream views may also be available.

---

# Why Follow Stream Matters

Suppose an HTTP conversation was split across many packets.

Looking at individual packets may show:

```text
Packet 101

Packet 102

Packet 103

Packet 104
```

But what we actually care about is:

```text
The complete conversation
```

Follow Stream combines related data into a more readable form.

Mental model:

```text
Individual packets
=
Pieces of a shredded document

Follow Stream
=
Reassembling the document
```

---

# TCP Streams

TCP connections can be identified as streams.

Packets belonging to the same TCP conversation share connection information.

Conceptually:

```text
Client IP
Client Port

Server IP
Server Port
```

together identify the communication flow.

Wireshark tracks these conversations using stream numbers.

---

# HTTP Traffic

HTTP traffic can expose application-layer information.

Possible examples include:

```text
Requested pages

Host names

User agents

Response codes

File names

HTML

Text content
```

For unencrypted HTTP, this information may be readable directly.

---

# HTTP vs HTTPS

HTTP traffic may be visible as readable application data.

HTTPS encrypts the HTTP communication using TLS.

Conceptually:

```text
HTTP

Readable application data
```

versus:

```text
HTTPS

HTTP data
   ↓
Encrypted by TLS
   ↓
Network capture sees encrypted payload
```

Wireshark can still show information about the connection, but the application contents are normally encrypted unless decryption material is available.

---

# Searching Packet Contents

Wireshark can search through packet data.

The Find Packet feature can search for things such as:

```text
String values

Hex values

Display-filter conditions
```

This is useful when the task provides a known clue.

Example:

```text
Artist name

File name

Specific text

HTTP header
```

Instead of scrolling through thousands of packets:

```text
Search for the evidence.
```

---

# Protocol Hierarchy

Wireshark can summarize which protocols exist in a capture.

The Protocol Hierarchy view can show relationships such as:

```text
Ethernet
   ↓
IPv4
   ↓
TCP
   ↓
HTTP
```

and the amount of traffic associated with each protocol.

This is useful for quickly understanding:

```text
What kinds of communication exist in this capture?
```

---

# Conversations

Wireshark can display network conversations between endpoints.

This can help identify:

```text
Which systems communicated

Which pairs exchanged the most traffic

Which TCP or UDP conversations existed
```

---

# Endpoints

Endpoint statistics can identify systems appearing in a capture.

Possible endpoint categories include:

```text
Ethernet addresses

IPv4 addresses

IPv6 addresses

TCP endpoints

UDP endpoints
```

This gives a high-level map of participants.

---

# Expert Information

Wireshark includes:

```text
Expert Information
```

which highlights events Wireshark considers noteworthy.

Categories can include things such as:

```text
Errors

Warnings

Notes

Chats
```

Depending on the traffic, examples may involve:

```text
TCP retransmissions

Malformed packets

Connection problems

Protocol warnings
```

---

# Expert Information Is Not Automatic Proof of an Attack

This is important.

Wireshark may mark something as:

```text
Warning

Error
```

but that does not automatically mean:

```text
Malicious traffic
```

or:

```text
The network is broken
```

Expert Information is:

```text
A clue
```

not:

```text
A final conclusion
```

The packet still needs to be interpreted in context.

---

# Retransmissions

TCP retransmissions can occur when data needs to be sent again.

Possible causes include:

```text
Packet loss

Network congestion

Timing issues

Capture limitations
```

A retransmission is worth investigating, but it is not automatically evidence of malicious activity.

---

# Colors

Wireshark uses coloring rules to make certain traffic easier to identify visually.

Different protocols or packet conditions can appear in different colors.

The important point is:

```text
Color helps recognition.
```

But:

```text
Color alone does not explain the packet.
```

Always inspect the protocol fields.

---

# Packet Length

The `Length` column shows the size of a captured frame.

This is not:

```text
The number of packets.
```

It represents:

```text
How many bytes the individual frame contains.
```

---

# Packet Number vs Packet Count

These are easy to confuse.

Example:

```text
No. 33790
```

means:

```text
This is packet number 33790.
```

It does not automatically mean:

```text
There are exactly 33790 packets.
```

Although the last packet number may equal the capture count in a simple capture, the concepts are different.

---

# Merging Capture Files

Wireshark can merge capture files.

When two captures are merged, packets from both files become part of the resulting capture.

This can cause:

```text
Packet numbers to change

Total packet count to change

Packet positions to change
```

Therefore if a question references:

```text
Packet 38
```

but the capture was modified or merged, the referenced packet number may no longer correspond to the same original traffic.

Mental model:

```text
Packet numbers are positions in the current evidence stack.
```

Change the stack:

```text
Positions may change.
```

---

# Do Not Modify Evidence Before You Need To

If a task asks about an original capture:

```text
Analyze the original capture first.
```

Merging or altering captures before answering packet-number-specific questions can create unnecessary confusion.

This follows a broader engineering principle:

```text
Do not change the system
before understanding the original state.
```

---

# Finding a Specific Value

Suppose the question asks:

```text
What is the TTL?
```

Do not search every number on the screen.

Use the protocol model:

```text
TTL
 ↓
IP Header
 ↓
IPv4 section
```

Then inspect:

```text
Internet Protocol Version 4
    ↓
Time to Live
```

---

# Finding an HTTP Header

Suppose the task asks about:

```text
ETag
```

Reason through it:

```text
ETag
 ↓
HTTP header
 ↓
Application layer
 ↓
Find HTTP packet
 ↓
Expand HTTP
 ↓
Locate ETag
```

---

# Finding Content in an HTTP Stream

Suppose a web response contains:

```text
HTML

Artist names

Text file contents

A hidden comment
```

The workflow becomes:

```text
Filter HTTP
   ↓
Find relevant request/response
   ↓
Follow the stream
   ↓
Search reconstructed content
```

This is often more efficient than examining every packet individually.

---

# HTML Clues

HTTP responses may contain HTML.

Common HTML structures include:

```html
<a href="...">Link Text</a>
```

```html
<img src="...">
```

```html
<!-- Comment -->
```

When analyzing HTTP traffic, understanding basic HTML makes it easier to distinguish:

```text
Attribute

Value

Visible text

Comment
```

For example:

```html
<a href="/artist/123">Artist Name</a>
```

contains:

```text
href
=
Link destination

Artist Name
=
Visible text
```

They are different pieces of information.

---

# Packet Analysis Workflow

A reliable workflow is:

```text
1. Read the question carefully

2. Identify what type of information is needed

3. Determine which protocol should contain it

4. Apply a display filter

5. Narrow to the relevant conversation

6. Inspect protocol fields

7. Follow the stream if necessary

8. Search for exact evidence

9. Confirm the result before answering
```

---

# Example: Find a Web Request

Question:

```text
Which page did the client request?
```

Reasoning:

```text
Page request
   ↓
HTTP
   ↓
Filter:
http
   ↓
Look for GET request
```

Possible evidence:

```text
GET /login HTTP/1.1
```

Answer:

```text
/login
```

---

# Example: Find a Destination Port

Question:

```text
Which destination port was used?
```

Reasoning:

```text
Port
 ↓
Transport Layer
 ↓
TCP or UDP
```

Then inspect:

```text
Transmission Control Protocol
    ↓
Destination Port
```

---

# Example: Find TTL

Question:

```text
What TTL value does this packet contain?
```

Reasoning:

```text
TTL
 ↓
IP
 ↓
IPv4 Header
```

Then:

```text
Internet Protocol Version 4
    ↓
Time to Live
```

---

# Example: Find Text Hidden in Web Traffic

Question:

```text
What name appears inside the web response?
```

Workflow:

```text
Filter HTTP
    ↓
Locate response
    ↓
Follow HTTP/TCP stream
    ↓
Search response content
    ↓
Read exact value
```

---

# Common Mistake: Scrolling Without a Theory

Bad workflow:

```text
Scroll

Click

Scroll

Click

Scroll

Click
```

This creates visual overload.

Better workflow:

```text
Question
 ↓
Prediction
 ↓
Filter
 ↓
Evidence
```

---

# Common Mistake: Assuming Green Means Correct

Wireshark colors packets based on configured coloring rules.

A packet being:

```text
Green
```

does not mean:

```text
"This is the answer."
```

Color is a visual classification tool.

The packet contents determine relevance.

---

# Common Mistake: Looking at the Wrong Layer

If the question asks for:

```text
Port
```

do not search Ethernet.

If it asks for:

```text
MAC address
```

do not search TCP.

Use the layer model:

```text
MAC
 ↓
Ethernet

IP / TTL
 ↓
IPv4

Port
 ↓
TCP / UDP

HTTP Header
 ↓
HTTP
```

---

# Common Mistake: Treating the GUI as the Concept

Wireshark's interface may change between versions.

Buttons may move.

Menus may look different.

Colors may differ.

But the underlying networking concepts remain:

```text
Frame
Packet
Segment
Protocol
Header
Field
Stream
```

Knowing the concept is more important than memorizing one exact menu location.

---

# Troubleshooting the GUI

If a tutorial says:

```text
Click this exact button
```

but the interface looks different:

```text
Do not immediately assume the concept changed.
```

Ask:

```text
What operation is the tutorial trying to perform?
```

Example:

```text
Goal:
Filter HTTP traffic
```

There may be several ways to accomplish it:

```text
Type display filter manually

Apply field as filter

Use protocol menus
```

The operation matters more than the exact button.

---

# Engineering Mental Model

Wireshark is not just:

```text
A program that shows packets.
```

It is an evidence inspection system.

The deeper workflow is:

```text
Network event
    ↓
Packet captured
    ↓
Protocol decoded
    ↓
Fields exposed
    ↓
Evidence filtered
    ↓
Conversation reconstructed
    ↓
Meaning determined
```

---

# Important Layer Mapping

```text
Ethernet
=
Data Link

IP
=
Network

TCP / UDP
=
Transport

HTTP / DNS / FTP / SSH
=
Application
```

When a question asks for a field:

```text
First identify the layer.
```

---

# Useful Display Filters

```text
http
```

HTTP traffic.

```text
tcp
```

TCP traffic.

```text
udp
```

UDP traffic.

```text
dns
```

DNS traffic.

```text
arp
```

ARP traffic.

```text
icmp
```

ICMP traffic.

```text
ip.addr == <IP>
```

Traffic involving an IP.

```text
ip.src == <IP>
```

Traffic originating from an IP.

```text
ip.dst == <IP>
```

Traffic going to an IP.

```text
tcp.port == <PORT>
```

TCP traffic using a port.

```text
udp.port == <PORT>
```

UDP traffic using a port.

```text
ip.ttl == <VALUE>
```

Packets containing a specific IPv4 TTL.

---

# Fast Recognition

If you see:

```text
MAC address
```

look inside:

```text
Ethernet
```

If you see:

```text
TTL
```

look inside:

```text
IPv4
```

If you see:

```text
Port
```

look inside:

```text
TCP / UDP
```

If you see:

```text
GET
POST
ETag
Host
```

look inside:

```text
HTTP
```

If you need:

```text
Entire conversation
```

think:

```text
Follow Stream
```

---

# Key Takeaway

Wireshark analysis should not be:

```text
Packet hunting by eyesight.
```

It should be:

```text
Question
   ↓
Protocol
   ↓
Filter
   ↓
Packet
   ↓
Field
   ↓
Evidence
   ↓
Conclusion
```

The goal is not to memorize where every button is.

The goal is to understand:

```text
What information exists

Which layer owns it

How to isolate it

How to verify it
```

That turns Wireshark from a confusing wall of packets into a structured network debugging and analysis tool.
