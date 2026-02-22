# SIP Call With Codec Negotiation

## Description
This scenario represents a full SIP voice call lifecycle including address discovery, session negotiation, codec capability exchange, media transmission, and session teardown.

It demonstrates a successful real-time communication session where signaling and media planes operate correctly together.

---

## Objective
Allow two endpoints to establish a multimedia session, negotiate media capabilities, exchange real-time audio, and terminate the session cleanly.

---

## Participants

Caller — initiates call  
Callee — receives call  

Transport occurs using:

[[SIP]] over [[UDP]] over [[IP]] over [[Ethernet]]

Media is transported separately using:

[[RTP]] over [[UDP]] over [[IP]]

---

## Session Phases

### 1 — Address Resolution
Before signaling can begin, the initiating host must discover the MAC address of the destination using [[ARP]].

This step enables Layer-2 delivery.

---

### 2 — Session Initiation
Caller sends:

INVITE request

This message:

- identifies destination
- creates dialog
- includes SDP offer

---

### 3 — Capability Advertisement
The SDP body lists supported codecs and media parameters.

This stage determines:

- codec compatibility
- media ports
- transport protocol
- payload formats

The callee selects one codec from the offered list.

---

### 4 — Call Progress
Provisional responses inform caller of call state:

100 Trying → request received  
180 Ringing → destination alerted  

These messages do not complete session establishment.

---

### 5 — Session Establishment
When callee accepts call:

200 OK is returned.

Caller confirms using:

ACK

At this point signaling phase is complete and media can begin.

---

### 6 — Media Exchange
Audio packets flow using [[RTP]] streams.

Media transport is independent of SIP signaling.

Packets may be marked with QoS priority to reduce latency.

---

### 7 — Session Termination
Either endpoint may end call using:

BYE request

Peer responds with:

200 OK

After this exchange, session resources are released.

---

## Protocol Interaction

[[SIP]] manages session control  
[[SDP]] negotiates media parameters  
[[RTP]] transports media  
[[UDP]] carries signaling and media  
[[IP]] routes packets  
[[Ethernet]] delivers frames locally  

---

## What This Scenario Demonstrates

- multi-layer protocol cooperation
- signaling/media separation
- codec negotiation process
- real-time packet prioritization
- proper call teardown

---

## Diagnostic Meaning

A trace matching this pattern indicates:

- endpoints reachable
- signaling path functional
- media path functional
- codec compatibility successful
- no session errors

This is considered a reference model of a healthy VoIP call.

---

## Evidence
[[SIP Call With SDP Codec Negotiation (AMR-WB Included)]]