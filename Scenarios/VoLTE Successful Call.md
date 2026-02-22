# VoLTE Successful Call

## Description
This scenario represents a successful Voice over LTE (VoLTE) session in which a mobile device establishes a dedicated bearer, negotiates a multimedia session through IMS signaling, transmits real-time voice packets, and terminates the call cleanly.

It models the normal behavior of a healthy LTE voice call across control, signaling, and user planes.

---

## Objective
Allow a mobile subscriber to place a real-time voice call over an LTE packet network with guaranteed quality of service and low latency.

---

## Participants

User Equipment (UE) — initiates session  
Radio Access Node — forwards traffic to core  
Core Network — manages tunnels and bearers  
IMS Servers — handle call signaling  
Remote Endpoint — receives call  

Communication uses:

Control Plane:
[[GTPv2]] over [[UDP]] over [[IP]]

User Plane:
[[GTP-U]] over [[UDP]] over [[IP]]

Signaling:
[[SIP]] over [[UDP]] inside GTP tunnel

Media:
[[RTP]] over [[UDP]] inside GTP tunnel

---

## Session Phases

### 1 — Bearer Establishment
The network creates a dedicated bearer for voice traffic.

This allocates:
- bearer identifier
- QoS parameters
- tunnel endpoints

Purpose:
Guarantee bandwidth and latency requirements for voice.

---

### 2 — Tunnel Creation
GTP tunnels are established between network nodes.

Each tunnel is identified by:
TEID — Tunnel Endpoint Identifier

These tunnels carry subscriber traffic across the core network.

---

### 3 — Traffic Classification
Traffic Flow Templates (TFT) define which packets belong to the bearer.

Filters may include:
- protocol type
- IP addresses
- ports

This ensures only voice packets use the voice bearer.

---

### 4 — Session Signaling
The UE initiates call setup using [[SIP]].

Typical signaling sequence:

INVITE → Trying → Ringing → OK → ACK

This stage negotiates session parameters and establishes dialog state.

---

### 5 — Media Negotiation
[[SDP]] bodies exchanged during signaling define:

- codecs
- media ports
- direction
- timing parameters

Both endpoints must agree before media begins.

---

### 6 — Voice Transmission
Once signaling completes, voice flows as [[RTP]] streams inside GTP tunnels.

Characteristics:
- constant packet interval
- low latency
- prioritized delivery

Media transport is independent from signaling.

---

### 7 — Call Termination
Either endpoint ends the call using a SIP termination request.

The peer confirms, and:

- RTP stops
- tunnels remain until released
- bearer eventually removed

---

## Protocol Interaction

[[GTPv2]] manages bearer control  
[[GTP-U]] transports user traffic  
[[SIP]] controls session signaling  
[[SDP]] negotiates media parameters  
[[RTP]] carries voice media  
[[UDP]] transports real-time packets  
[[IP]] routes across networks  

---

## What This Scenario Demonstrates

- separation of control, signaling, and media planes
- dedicated bearer allocation
- tunneled packet transport
- real-time media delivery
- coordinated protocol operation

---

## Diagnostic Meaning

A trace matching this pattern indicates:

- successful bearer setup
- correct tunnel configuration
- functional signaling path
- working media path
- healthy LTE voice session

It represents the expected behavior of a properly functioning VoLTE call.

---

## Evidence
[[VoLTE Call Session]]]