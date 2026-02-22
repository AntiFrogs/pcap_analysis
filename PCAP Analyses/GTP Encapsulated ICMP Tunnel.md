# GTP Encapsulated ICMP Tunnel

## Overview
This capture shows tunneled user-plane traffic transported using GTP over UDP. Inside the GTP tunnel, IP packets carrying ICMP echo requests and replies are exchanged between two endpoints.

The trace demonstrates encapsulated packet delivery through a tunneling protocol rather than direct IP transmission.

---

## Participants

Outer tunnel endpoints:
192.168.40.179  
192.168.40.178  

Inner packet endpoints:
202.11.40.158  
192.168.40.178

---

## Protocol Stack
Outer transport:

[[UDP]] → [[IP]] → [[Ethernet]]

Encapsulation layer:

[[GTP-U]]

Inner payload:

[[IP]] → [[ICMP]]

---

## Tunnel Behavior

### GTP Transport
All packets use:

UDP source port = 2152  
UDP destination port = 2152 

Port 2152 is the standard port used by GTP-U for user-plane traffic.

---

### Tunnel Identifier
All packets share the same tunnel identifier:

TEID = 0x00000001 

This confirms they belong to the same logical tunnel session.

---

### GTP Header Characteristics
Observed flags:

- Version = 1  
- Sequence number present  
- Extension header absent  

These values indicate standard GTPv1-U data packets.

---

## Encapsulated Traffic

### Inner Protocol
Encapsulated packets are IPv4 carrying ICMP.

Protocol field value:

1 → ICMP 

---

### ICMP Activity
ICMP message types observed:

Type 8 → Echo Request  
Type 0 → Echo Reply 

This confirms bidirectional ping traffic inside the tunnel.

---

### Sequence Behavior
ICMP sequence numbers increment between packets, indicating a continuous ping session rather than isolated probes.

---

## Timing Characteristics

Packet timing shows:

≈1 second spacing between request packets

This matches standard ping interval behavior.

---

## Network Layer Observations

TTL values for encapsulated packets:

64 

This suggests a Linux-like originating system or default TTL configuration.

---

## Link Layer Observations

MAC addresses resolve to:

VMware virtual interfaces 

This indicates the capture environment is virtualized.

---

## Interpretation
This capture represents a tunneled connectivity test where ICMP packets are transported inside a GTP tunnel between two endpoints.

The traffic confirms:

- tunnel establishment already completed
- active user-plane data forwarding
- bidirectional connectivity through tunnel

No packet loss or retransmissions are observed.


---

## Related Protocol References
[[GTP-U]]  
[[UDP]]  
[[IP]]  
[[ICMP]]

---

## Related Scenario
[[GTP User Plane Tunnel Traffic]]