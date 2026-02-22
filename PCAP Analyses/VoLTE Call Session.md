# VoLTE Call Session — End-to-End EPS Bearer + SIP + RTP

## Overview
This trace shows a Voice over LTE session that includes:

- bearer setup
- tunnel creation
- SIP signaling
- media transport

The capture contains both control-plane and user-plane traffic.

---

## Protocol Stack Observed

Control Plane:
[[IP]] → [[UDP]] → [[GTPv2]]

User Plane:
[[IP]] → [[UDP]] → [[GTP-U]] → inner [[IP]] → [[UDP]] → [[RTP]]

Signaling Plane:
[[IP]] → [[UDP]] → [[GTP-U]] → inner [[IP]] → [[UDP]] → [[SIP]]

Evidence:
Frame protocols explicitly show nested stacks. 

---

## Phase 1 — Bearer Creation

A bearer context is created and accepted.

Evidence:

- EPS Bearer ID = 7 
- Cause = Request accepted (16) 

Meaning:
Core network successfully created a dedicated bearer for this session.

---

## Phase 2 — Tunnel Establishment

Two tunnel endpoints assigned:

eNodeB TEID  
0x000000b2 → 172.24.0.45 

SGW TEID  
0x00000021 → 10.4.128.21 

Meaning:
User-plane path is now established between radio and core.

---

## Phase 3 — Traffic Flow Template Installation

Packet filters define which packets belong to this bearer.

Filters specify:

- protocol = UDP (0x11) 
- remote IP = 192.168.101.3 
- core IP = 10.4.128.21 
- ports = 50016 / 31238 

Meaning:
Only packets matching these rules will be carried in this tunnel.

This is how LTE isolates voice traffic from data traffic.

---

## Phase 4 — SIP Signaling Through Tunnel

SIP packets are encapsulated inside GTP-U.

Evidence:

Frame protocol stack contains SIP after GTP layers. 

Observed SIP headers:

Via:
SIP/2.0/UDP 10.4.128.21 

Second hop:
SIP/2.0/TCP 192.168.101.3:5060 

Meaning:
Call signaling traverses IMS core nodes.

---

## Phase 5 — SDP Media Negotiation

SDP payload describes media session.

Owner IP:
10.4.128.21 

Media attributes:

- sendrecv
- ptime = 20 ms 

Telephone-event payload declared. 

Meaning:
Endpoints negotiated bidirectional audio and DTMF support.

---

## Phase 6 — RTP Media Flow

Media packets appear as:

outer UDP port 2152 → GTP-U tunnel 

Inside tunnel:

RTP stream visible after decapsulation. 

Meaning:
Voice packets are transported inside LTE user plane.

---

## Phase 7 — Additional Transport Traffic

Local TCP/TLS traffic observed:

TCP → TLS → port 27017 

Meaning:
Capture environment also included local application communication (likely database or logging).

This is unrelated to VoLTE signaling.

---

## Timeline Reconstruction

1 Bearer created and accepted  
2 Tunnel endpoints exchanged  
3 Traffic filters installed  
4 SIP signaling begins  
5 SDP negotiates media parameters  
6 RTP flows inside GTP-U  
7 Session proceeds normally  

No failure codes observed.

---

## Network Architecture Identified

From addresses and roles:

UE side: 192.168.101.3  
Core node: 10.4.128.21  
eNodeB: 172.24.0.45  

This is a standard LTE architecture:

UE → eNodeB → SGW → IMS

---

## Behavioral Conclusion

This capture represents a fully successful VoLTE call.

Evidence:

- bearer accepted
- tunnels established
- signaling completed
- RTP present
- no error causes

---

## Diagnostic Value

This trace is a textbook example of:

successful IMS voice session establishment over LTE

It can be used as a reference model for:

- troubleshooting VoLTE failures
- verifying core network behavior
- validating QoS bearer setup

---

## Related Protocol References

[[GTPv2]]  
[[GTP-U]]  
[[SIP]]  
[[SDP]]  
[[RTP]]  
[[UDP]]  
[[IP]]

---

## Scenario Type
[[VoLTE Successful Call]]