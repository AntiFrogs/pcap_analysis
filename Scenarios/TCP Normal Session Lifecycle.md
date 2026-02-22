# TCP Normal Session Lifecycle

## Description
This scenario represents a standard TCP connection where two hosts successfully establish communication, exchange data, and terminate the session cleanly.

It illustrates the expected behavior of a healthy transport-layer session.

---

## Objective
Allow two endpoints to reliably exchange data over an IP network while guaranteeing delivery, order, and integrity.

---

## Participants
Client — initiates connection  
Server — accepts connection  

Communication occurs over [[TCP]] running on [[IP]] over Ethernet.

---

## Session Phases

### 1 — Connection Establishment
The client initiates a connection using a SYN packet.

The server replies with SYN-ACK.

The client sends ACK.

After this exchange, the connection enters the **ESTABLISHED** state.

---

### 2 — Capability Negotiation
During handshake, both endpoints announce transport capabilities such as:

- receive window size
- scaling factors
- segment limits

This negotiation determines throughput potential and flow-control behavior.

---

### 3 — Data Transfer
After establishment, payload data is transmitted.

TCP guarantees:
- ordered delivery
- retransmission if lost
- duplicate suppression

Acknowledgments confirm successful reception.

---

### 4 — Idle State
Connections may remain open without data transfer.

During this state:
- no packets are exchanged
- connection remains valid
- resources stay reserved

---

### 5 — Connection Termination
TCP sessions close using a four-step shutdown:

1. One side sends FIN
2. Peer acknowledges
3. Peer sends FIN
4. First host acknowledges

This is called a **graceful close**.

---

## Protocol Interaction
[[TCP]] handles reliability and session control  
[[IP]] handles addressing and routing  
Ethernet handles local delivery

---

## What This Scenario Demonstrates
- standard TCP state transitions
- negotiated transport parameters
- reliable data exchange
- orderly session shutdown


￼￼￼Why This Capture Is Valuable
This trace serves as a clean reference example of:

- correct TCP state transitions
- window scaling negotiation
- bidirectional session closure
- stable transport behavior

It can be used as a baseline when analyzing faulty TCP connections.

---

## Diagnostic Meaning
A session matching this pattern indicates:

- reachable host
- functioning network path
- correct protocol behavior
- no transport-layer faults

It is considered a baseline example of a healthy TCP connection.

---

## Evidence
[[TCP Window Scaling Session]]