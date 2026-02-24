# RTCP — Real-time Transport Control Protocol

## Definition
RTCP (Real-time Transport Control Protocol) is a companion protocol to [[RTP]] used to monitor and control real-time media sessions.

It provides feedback about media transmission quality but does not carry media data itself.

---

## Purpose
RTCP is responsible for:

- reporting packet loss
- reporting jitter
- reporting round-trip delay
- identifying stream participants
- synchronizing multiple media streams

It ensures that RTP sessions can adapt to network conditions.

---

## Relationship with RTP

RTP → carries media  
RTCP → monitors RTP

They are typically sent on separate UDP ports.

If RTP uses port N, RTCP usually uses port N+1.

---

## Transport
RTCP runs over:

[[UDP]]

It is sent periodically during an RTP session.

---

## Packet Types

Common RTCP packet types include:

### Sender Report (SR)
Sent by active RTP senders.  
Contains:

- RTP timestamp
- packet count
- octet count
- NTP timestamp

Used for synchronization.

---

### Receiver Report (RR)
Sent by receivers.  
Contains:

- fraction lost
- cumulative packets lost
- highest sequence number received
- jitter
- last SR timestamp

Used for quality monitoring.

---

### Source Description (SDES)
Provides identification information such as:

- CNAME (canonical name)
- user identification

---

### Goodbye (BYE)
Indicates that a participant is leaving the session.

---

### Application-Defined (APP)
Custom application-specific messages.

---

## Key Metrics Reported

Packet Loss → number of missing RTP packets  
Jitter → variation in packet arrival time  
Round Trip Time (RTT) → latency measurement  

These values help detect network instability.

---

## Bandwidth Rule
RTCP traffic is limited to a small percentage (typically 5%) of the total RTP session bandwidth.

This prevents control traffic from overwhelming media traffic.

---

## Synchronization Role
RTCP Sender Reports include NTP timestamps.

This allows synchronization of:

- audio and video streams
- lip-sync in multimedia sessions

---

## Diagnostic Clues

High packet loss → network congestion  
Increasing jitter → unstable path  
No RTCP reports → monitoring disabled  
RTCP BYE → session termination  

RTCP is often the fastest way to detect quality problems in VoIP.

---

## What RTCP Does Not Do

It does not:

- retransmit lost RTP packets
- encrypt media
- control session establishment

Session setup is handled by [[SIP]] and media parameters by [[SDP]].

---

## Used In

VoIP  
Video conferencing  
Streaming media  
WebRTC  
VoLTE media sessions  

---

## Specification

RFC 3550 — RTP: A Transport Protocol for Real-Time Applications