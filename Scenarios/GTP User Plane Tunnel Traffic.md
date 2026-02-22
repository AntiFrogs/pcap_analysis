# GTP User Plane Tunnel Traffic

## Description
This scenario represents user-plane data transmission through a GTP tunnel where packets from one endpoint are encapsulated and transported across an intermediate network before being delivered to their destination.

It illustrates how tunneling allows one network to carry traffic belonging to another logical network.

---

## Objective
Allow user traffic to traverse a core network transparently while preserving the original packet structure.

The tunnel hides the inner packet from intermediate routers and delivers it intact to the tunnel endpoint.

---

## Participants
Tunnel Endpoint A — encapsulates packets  
Tunnel Endpoint B — decapsulates packets  

Inner hosts — original sender and receiver of payload traffic  

Communication occurs using:

[[GTP-U]] over [[UDP]] over [[IP]].

---

## Session Phases

### 1 — Encapsulation
The sending endpoint receives an IP packet from a user device.

It wraps that packet inside a GTP header and sends it across the transport network.

---

### 2 — Transport
The encapsulated packet travels through the network as ordinary UDP traffic.

Intermediate routers only see:

UDP → IP → Ethernet

They do not inspect the inner payload.

---

### 3 — Decapsulation
The receiving endpoint reads the GTP header, identifies the tunnel using the TEID, removes the tunnel header, and forwards the original packet.

---

### 4 — Payload Delivery
The inner packet is delivered to its destination as if it had traveled normally, even though it crossed a tunnel.

In this capture, the payload traffic is:

ICMP echo request/reply packets.

---

## Tunnel Identification
Each GTP session is uniquely identified using:

TEID — Tunnel Endpoint Identifier

Packets with the same TEID belong to the same logical tunnel.

---

## Protocol Interaction
[[GTP-U]] handles tunneling and session multiplexing  
[[UDP]] transports tunnel packets  
[[IP]] handles routing across networks  
[[Ethernet]] handles local delivery  

---

## What This Scenario Demonstrates
- packet encapsulation and decapsulation
- logical tunnel transport
- separation of transport and payload networks
- user-plane forwarding

---

## Diagnostic Meaning
A trace matching this pattern indicates:

- tunnel is active
- TEID mapping works
- endpoints are reachable
- payload traffic passes successfully

This is considered a baseline example of a healthy user-plane tunnel.

---

## Evidence
[[GTP Encapsulated ICMP Tunnel]]