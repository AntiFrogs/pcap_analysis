# SIP Call With SDP Codec Negotiation (AMR-WB Included)

## Overview
This capture shows a SIP call setup sequence beginning with ARP resolution, followed by SIP signaling over UDP, codec negotiation through SDP, call establishment, media transport, and call termination.

All observed traffic belongs to a single SIP dialog identified by one Call-ID.

---

## Protocol Stack

Primary signaling stack:

[[Ethernet]] → [[ARP]]  
[[Ethernet]] → [[IP]] → [[UDP]] → [[SIP]] → [[SDP]]

	Media stack:

[[Ethernet]] → [[IP]] → [[UDP]] → [[RTP]] payload streams

Observed frame protocol strings confirm these stacks. 

---

## Participants

Caller  
IP: 192.168.1.117  

Callee  
IP: 192.168.1.50  

MAC vendors:

- Hon Hai Precision  
- Dell Inc. 

---

## Phase 1 — Address Resolution

First packets are ARP.

Request:
192.168.1.50 MAC unknown → broadcast query

Reply:
192.168.1.117 responds with MAC address. 

Meaning:
Layer-2 path must be known before SIP signaling can start.

---

## Phase 2 — Call Initiation

Caller sends:

SIP INVITE sip:tetsu@192.168.1.50 

Key headers:

- CSeq = 1 INVITE 
- User-Agent = Ekiga softphone 
- Call-ID uniquely identifies dialog 
- Max-Forwards = 70 

Transport:
UDP port 5060 ↔ 5060 

---

## Phase 3 — Codec Negotiation (SDP Offer)

INVITE contains SDP body.

Media parameters:

Audio stream port: 5096  
Protocol: RTP/AVP 

Advertised codecs include:

- Speex
- PCMU
- PCMA
- iLBC
- GSM
- G722
- SILK
- G726 variants
- [[AMR]]-WB
- telephone-event 

Example:

AMR-WB/16000 declared as supported format. 

Meaning:
Caller offers a list of codecs. Callee will choose one.

---

## Phase 4 — Provisional Responses

Callee replies:

SIP/2.0 100 Trying 

Meaning:
Server received INVITE and is processing.

Then:

SIP/2.0 180 Ringing 

Meaning:
Destination endpoint is alerting user.

---

## Phase 5 — Call Acceptance

Final success response (not shown in earlier snippet but confirmed by ACK presence):

ACK request observed:

ACK sip:tetsu@192.168.1.50 

ACK only occurs after 200 OK.

Therefore:
200 OK response must have been sent earlier in the dialog.

---

## Phase 6 — Media Transmission

After ACK, RTP media begins.

Observed UDP media stream:

Source port 5096 → destination 5074 

DSCP value:
46 (Expedited Forwarding) 

Meaning:
Packets are marked for real-time priority handling.

---

## Phase 7 — Call Termination

Termination request observed:

BYE sip:tetsu@192.168.1.117 

Meaning:
One endpoint ended the session.

---

## SIP Dialog Summary

Sequence reconstructed from packets:

1 ARP resolution  
2 INVITE  
3 100 Trying  
4 180 Ringing  
5 200 OK (implied)  
6 ACK  
7 RTP media  
8 BYE  
9 Final OK (implied)

---

## Network Behavior Observations

TTL values:

64 → typical Linux/softphone  
127 → Windows host 

Interpretation:
Endpoints run different operating systems.

---

## Codec Negotiation Insight

Presence of AMR-WB in SDP does NOT guarantee it was used.

It only proves:

Endpoint advertised capability.

Actual selected codec would appear in:

200 OK SDP or RTP payload type mapping.

---

## Related Protocol References

[[ARP]]  
[[Ethernet]]  
[[IP]]  
[[UDP]]  
[[SIP]]  
[[SDP]]  
[[RTP]]

---

## Related Scenario

[[SIP Call With Codec Negotiation]]