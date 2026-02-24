# SCTP — Stream Control Transmission Protocol

## Definition
SCTP (Stream Control Transmission Protocol) is a reliable, message-oriented transport protocol designed for signaling applications.

It combines features of TCP and UDP while introducing multi-streaming and multi-homing capabilities.

---

## Purpose
SCTP is designed to transport signaling traffic that requires:

- reliable delivery
- ordered messages
- congestion control
- fault tolerance

It is widely used in telecom networks.

---

## Layer Position
SCTP operates at the transport layer.

Protocol stack example:

Application → [[SCTP]] → [[IP]]

---

## Key Characteristics

### Message-Oriented
Unlike TCP, which is byte-stream oriented, SCTP preserves message boundaries.

Each send corresponds to one message.

---

### Multi-Streaming
An SCTP connection can contain multiple independent streams.

If one stream experiences loss, other streams continue unaffected.

This prevents head-of-line blocking.

---

### Multi-Homing
An endpoint can use multiple IP addresses within a single SCTP association.

If one path fails, traffic switches automatically.

This improves resilience.

---

## Connection Model

SCTP uses an "association" instead of a TCP connection.

Association setup uses a 4-way handshake:

INIT  
INIT-ACK  
COOKIE-ECHO  
COOKIE-ACK  

This protects against SYN flood attacks.

---

## Reliability Mechanisms

- acknowledgments (SACK)
- retransmissions
- congestion control
- flow control

Reliability behavior is similar to TCP but message-based.

---

## Ports
SCTP uses port numbers similar to TCP/UDP.

Common telecom ports:

S1-AP → typically 36412

---

## Chunk Structure

SCTP packets contain chunks.

Common chunk types:

DATA  
INIT  
SACK  
HEARTBEAT  
SHUTDOWN  

Each packet may contain multiple chunks.

---

## Heartbeat Mechanism
SCTP sends heartbeat chunks to verify path availability.

If no response is received, path failover may occur.

---

## Common Use Cases

LTE control plane (e.g., [[S1-AP]])  
SIGTRAN (SS7 over IP)  
Telecom core signaling  
Diameter transport  

---

## Diagnostic Clues

Repeated INIT → association not established  
Missing COOKIE-ACK → handshake failure  
Frequent retransmissions → congestion or path issue  
Heartbeat failures → link instability  

---

## Advantages Over TCP

- no head-of-line blocking (multi-streaming)
- built-in multi-homing
- improved DoS resistance
- message boundary preservation

---

## What SCTP Does Not Do

It does not:

- encrypt traffic
- provide application logic
- carry user-plane data in LTE

It is purely a transport protocol.

---

## Relationship

[[SCTP]] commonly transports:

- [[S1-AP]]
- [[Diameter]]
- other telecom signaling protocols

---

## Used In

LTE (control plane)  
IMS signaling  
Telecom core networks  

---

## Specification

RFC 4960 — Stream Control Transmission Protocol