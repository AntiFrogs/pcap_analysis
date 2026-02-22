# ARP — Address Resolution Protocol

## Definition
ARP is a Layer-2/Layer-3 bridging protocol used to map an IPv4 address to its corresponding MAC address on a local network.

It allows devices to discover the physical hardware address required for Ethernet delivery when only an IP address is known.

---

## Purpose
IP addresses identify hosts logically.  
MAC addresses deliver frames physically.

ARP connects these two addressing systems.

Without ARP, IP communication inside a LAN would fail.

---

## When ARP Is Used
ARP is triggered whenever a device needs to send an IP packet and does not already know the destination MAC address.

Typical cases:
- first packet to a host
- first packet to gateway
- cache expiration
- network interface reset

---

## Operation

### Step 1 — Request
Sender broadcasts:

"Who has IP X.X.X.X?"

Broadcast destination MAC:
FF:FF:FF:FF:FF:FF

---

### Step 2 — Reply
Target device responds directly:

"IP X.X.X.X is at MAC AA:BB:CC:DD:EE:FF"

Reply is unicast.

---

### Step 3 — Cache Storage
Sender stores result in ARP table for later use.

---

## ARP Packet Fields
Hardware Type  
Protocol Type  
Hardware Length  
Protocol Length  
Operation (Request or Reply)  
Sender MAC  
Sender IP  
Target MAC  
Target IP  

---

## ARP Table
Each device maintains a cache:

IP → MAC mapping

Entries expire automatically after a timeout.

---

## Types of ARP

### Standard ARP
Normal request/reply mapping.

---

### Gratuitous ARP
Device announces its own IP/MAC mapping without request.

Used for:
- IP conflict detection
- failover systems
- redundancy protocols

---

### Proxy ARP
Router answers ARP requests on behalf of another device.

Used in special routing setups.

---

## Scope Limitation
ARP only works within a local broadcast domain.

Routers do not forward ARP broadcasts.

---

## Relationship in Stack
[[Ethernet]] → ARP resolves address → [[IP]] packet sent

ARP is not encapsulated in IP.  
It is carried directly inside Ethernet frames.

---

## Diagnostic Clues

No ARP reply → host unreachable or offline  
Repeated ARP requests → target not responding  
Duplicate replies → IP conflict  
Unexpected MAC → spoofing attack  

---

## Security Notes
ARP has no authentication.

This allows attacks such as:
- ARP spoofing
- man-in-the-middle interception
- traffic redirection

Security tools may use static ARP entries or inspection mechanisms to mitigate this.

---

## Why ARP Matters
ARP is foundational for LAN communication. Every TCP, UDP, or ICMP packet sent locally depends on it.

Failures in ARP often appear as:

"Network unreachable"  
"Host unreachable"  
or silent packet loss.

---

## Summary
ARP is the translation service between logical and physical addressing. It operates silently but is essential for all local IP communication.

Without ARP, Ethernet networks carrying IP traffic cannot function.