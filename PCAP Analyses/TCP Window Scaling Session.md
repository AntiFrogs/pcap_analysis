# TCP Window Scaling Session

## Overview
This capture shows a TCP session between two hosts including connection establishment, data exchange, and graceful connection termination. The trace demonstrates TCP reliability features and negotiated flow-control parameters.

---

## Participants
Client: 192.168.200.135  
Server: 192.168.200.21  

Destination service port: 2000   

---

## Protocol Stack
[[TCP]] → [[IP]] → [[Ethernet]]

---

## Session Behavior

### Connection Presence
The TCP completeness flags confirm this capture contains:

- SYN  
- SYN-ACK  
- ACK  
- data  
- FIN  

indicating a full TCP lifecycle. 

---

### Data Exchange
The trace includes packets marked as containing data segments. 

This confirms the connection was not only established but also used to transmit application payload.

---

### Connection Termination
FIN flags are present in both directions.

Example:

- ACK + FIN detected  
- flagged as connection closing event 

This indicates a **graceful TCP shutdown** rather than reset termination.

---

### Bidirectional Close
Packets show:

- passive FIN from one side  
- active FIN from the other  

This confirms both endpoints properly closed their side of the connection. 

---

## TCP Flow Control Observations

Advertised window values differ per endpoint.

Example values:
- window = 1026  
- scaled window = 262656   

Another packet shows:

- raw window = 502  
- scaled window = 64256   

This confirms that TCP **window scaling** is active and negotiated.

---

## Network Layer Observations

Source host:
192.168.200.135  

Destination host:
192.168.200.21 

TTL observed:
128 

TTL value suggests a Windows-based sender or system using similar defaults.

---

## Link Layer Observations

Source MAC vendor:
VMware, Inc.  

Destination MAC vendor:
Dell Inc. 

This indicates a likely virtual machine communicating with a physical host.

---

## Interpretation
This capture represents a complete TCP session demonstrating:

- full handshake
- negotiated flow control
- successful data transmission
- orderly connection termination

The session shows normal TCP behavior with no resets or errors.


---

## Related Protocol References
[[TCP]]  
[[IP]]  
[[Ethernet]]

---

## Related Scenario
[[TCP Normal Session Lifecycle]]