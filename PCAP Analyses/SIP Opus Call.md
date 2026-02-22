# SIP Opus Call — Full Trace Analysis

Source Capture: :contentReference[oaicite:0]{index=0}

---

## 1. Executive Summary

This capture represents a complete and successful SIP call establishment sequence between two endpoints followed by RTP media initialization. The trace demonstrates a textbook implementation of the SIP offer/answer model with SDP-based media negotiation and UDP transport.

The session is established in under 6 milliseconds, indicating a controlled lab or virtualized environment rather than a real WAN network.

No packet loss, retransmissions, or protocol violations are observed. This makes the trace suitable as a reference baseline for comparison against faulty captures.

---

## 2. Network Participants

| Role | IP | Port | Notes |
|-----|----|------|------|
Caller | 10.0.2.20 | 5060 | SIP client (likely SIPp generator) |
Callee | 10.0.2.15 | 5060 | SIP server (FreeSWITCH) |

Evidence:
User-Agent header identifies server as:
FreeSWITCH-mod_sofia/1.6.12

---

## 3. Protocol Stack Observed

Signaling Stack:
[[SIP]] → [[UDP]] → [[IP]]

Media Stack:
[[RTP]] → [[UDP]] → [[IP]]

---

## 4. Packet Timeline Analysis

| Frame | Time | Direction | Protocol | Meaning |
|------|------|-----------|----------|--------|
1 | 0.000000 | Caller → Callee | SIP | INVITE |
2 | 0.000189 | Callee → Caller | SIP | 100 Trying |
3 | 0.003679 | Callee → Callee | RTP | Test packet |
4 | 0.005554 | Callee → Caller | SIP | 200 OK |
5 | 0.005641 | Caller → Callee | SIP | ACK |

Interpretation:

The dialog is established in only 5.6 ms. That is far faster than real network conditions and confirms:

• local VM environment  
• or loopback testing  
• or SIP testing tool  

---

## 5. SIP Transaction Breakdown

### INVITE Request
Caller sends INVITE requesting session with SDP offer.

Important headers:

Call-ID = unique dialog identifier  
CSeq = 1 INVITE  
Via = transport route  
From tag = caller dialog identifier  

SDP Offer contains:

audio port 6000  
codec opus/48000/2  
direction recvonly  

Meaning:
Caller requests audio but will not transmit audio.

---

### 100 Trying Response
Server acknowledges request receipt.

Purpose:
Prevents retransmission by caller.

---

### 200 OK Response
Server accepts session and returns SDP answer.

Important SDP parameters:

audio port = 24196  
codecs = 99 (Opus) and 101 (DTMF events)  
ptime = 20 ms  
direction = sendonly  

Meaning:
Server will transmit audio only.

Combined SDP Result:

Caller = receive only  
Callee = send only  

This is a one-way media stream.

---

### ACK Request
Caller confirms dialog establishment.

At this moment:

SIP signaling phase is complete.  
Session is officially established.

---

## 6. RTP Analysis

A single RTP packet appears shortly after the INVITE exchange.

Payload:
"TEST"

Interpretation:
This is not real media.

It is a probe packet used to verify:

• RTP port reachability  
• firewall openness  
• NAT traversal  
• codec pipeline readiness  

Professional testing systems often send such packets.

---

## 7. Transport Layer Observations

### UDP
Used for both SIP signaling and RTP media.

No retransmissions observed.  
Checksums valid.  
Packet spacing consistent.

Conclusion:
Transport layer is healthy.

---

### IP
TTL = 64 for all packets.

This strongly indicates:

• Linux stack
• or Linux-based VoIP platform
• or virtualized environment

No fragmentation observed.  
DF flag set on some packets → Path MTU discovery enabled..

---

## 12. Related Protocol References

[[SIP]]  
[[SDP]]  
[[RTP]]  
[[UDP]]  
[[IP]]

---

## 13. Final Verdict

Status: VALID SESSION  
Quality: CLEAN TRACE  
Use Case: REFERENCE BASELINE

No faults detected.