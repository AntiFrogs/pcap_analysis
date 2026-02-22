# Basic SIP Call — Scenario Description

## Overview
This scenario represents a standard VoIP session setup using [[SIP]] signaling, [[SDP]] negotiation, and [[RTP]] media transport. It illustrates the canonical workflow used in real-time communication systems.

---

## Objective
Establish a media session between two endpoints so that audio can be transmitted from one host to another.

---

## Participants
Caller — session initiator  
Callee — session receiver  

Communication occurs over [[UDP]] on top of [[IP]] networking.

---

## Protocol Interaction Model

**Signaling phase**  
[[SIP]] establishes and confirms the session.

**Negotiation phase**  
[[SDP]] defines media parameters such as codec, port, and direction.

**Media phase**  
[[RTP]] transports the audio stream.

**Stack relationship**

[[SIP]] → [[SDP]] → [[RTP]] → [[UDP]] → [[IP]]

---

## Call Flow Sequence

1. Caller sends **INVITE** via [[SIP]]  
2. Callee responds **100 Trying**  
3. Callee accepts with **200 OK** including [[SDP]] answer  
4. Caller sends **ACK**  
5. [[RTP]] media transmission begins  

This completes a SIP dialog lifecycle.

---

## Behavioral Interpretation
The trace reflects a successful session setup with:

- correct signaling exchange
- valid negotiation
- functioning media path

No retransmissions or protocol errors are observed.

---

## What This Scenario Demonstrates
This scenario is useful for understanding:

- how [[SIP]] dialogs form
- how [[SDP]] negotiation works
- how [[RTP]] sessions begin
- how transport via [[UDP]] and delivery via [[IP]] support real-time media

---

## Reference Capture
See → [[SIP Opus Call]]

---

## Practical Value
This scenario can serve as:

- a baseline comparison trace
- a learning reference
- a template for analyzing new captures