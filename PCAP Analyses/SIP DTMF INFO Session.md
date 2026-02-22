# SIP DTMF INFO Session

## Overview
This capture shows a SIP dialog containing INVITE transactions, CANCEL attempts, and mid-dialog INFO requests carrying DTMF digits. The trace demonstrates SIP signaling timing behavior and DTMF delivery using the SIP INFO method.

---

## Participants
Client: 178.45.73.241  
Server: 213.192.59.x network  

Client software: Ekiga/3.2.0  
Server software: Sip Express Media Server

---

## Protocol Stack
[[SIP]] → [[SDP]] → [[UDP]] → [[IP]]

---

## SIP Methods Observed
- INVITE
- CANCEL
- ACK
- INFO
- 200 OK responses

Supported methods advertised:
INVITE, ACK, OPTIONS, BYE, CANCEL, SUBSCRIBE, NOTIFY, REFER, MESSAGE, INFO, PING

---

## Session Behavior

### INVITE Transactions
INVITE requests are sent toward:

sip:echo@iptel.org

INVITE messages include SDP bodies describing media capabilities.

---

### CANCEL Attempts
Multiple CANCEL requests appear in the trace.  
Each CANCEL receives:

SIP/2.0 200 ok -- no more pending branches

This response indicates the server acknowledges the cancel request but has no remaining pending transaction branches to cancel.

---

### ACK Presence
ACK requests are observed after final responses to INVITE transactions.

This is correct SIP behavior:
Whenever a final response to an INVITE is received, the client must send ACK to complete the transaction.

---

### Mid-Dialog INFO Requests (DTMF)
INFO requests are present with:

Content-Type: application/dtmf-relay

Message bodies include values such as:

Signal= 3  
Duration= 180  

and

Signal= 4  

These INFO messages are acknowledged with:

SIP/2.0 200 OK

This confirms successful delivery of DTMF signaling via SIP INFO.

---

## SDP Capabilities Advertised

Audio:
- PCMA codec
- telephone-event payload types

Video:
- H.261
- Theora

Media direction:
sendrecv

Meaning:
Bidirectional media supported.

---

## Routing Behavior
ACK requests contain Route headers pointing to:

213.192.59.75

This indicates a proxy is on the signaling path and Record-Route logic is active.

---

## Interpretation
This trace demonstrates real SIP dialog behavior including:

- multiple simultaneous transactions
- cancellation logic
- INFO method signaling
- proxy routing
- DTMF delivery inside SIP messages

The observed message ordering reflects normal asynchronous SIP operation over UDP rather than a protocol error.

---

## Why This Capture Is Valuable
This capture shows several real-world behaviors not visible in simple traces:

- overlapping transactions
- cancel handling
- mid-dialog requests
- DTMF signaling via INFO
- proxy routing influence

It is useful for studying realistic SIP signaling behavior.

---

## Related Protocol References
[[SIP]]  
[[SDP]]  
[[UDP]]  
[[IP]]

---

## Related Scenario
[[DTMF via SIP INFO]]