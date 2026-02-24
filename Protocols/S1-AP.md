# S1-AP — S1 Application Protocol

## Definition
S1-AP (S1 Application Protocol) is the control-plane signaling protocol used between the eNodeB (LTE base station) and the MME (Mobility Management Entity).

It manages UE context, bearer control, mobility procedures, and session establishment over the S1 interface in LTE networks.

---

## Purpose
S1-AP is responsible for:

- UE context setup and release
- bearer establishment coordination
- mobility management
- handover procedures
- paging
- NAS message transport

It carries signaling required to connect a mobile device to the EPC core network.

---

## Interface
S1-AP runs over the **S1-MME interface**, which connects:

eNodeB ↔ MME

---

## Transport Stack
S1-AP runs over:

[[SCTP]] → [[IP]]

SCTP provides reliable, message-oriented transport with multi-streaming support.

---

## Message Categories

### UE-Associated Signaling
Messages related to a specific subscriber.

Examples:
Initial UE Message  
UE Context Setup Request  
UE Context Release  

---

### Non-UE-Associated Signaling
Network-wide messages not tied to one subscriber.

Examples:
S1 Setup Request  
Reset  
Error Indication  

---

## Key Identifiers

MME UE S1AP ID  
eNB UE S1AP ID  

These identifiers uniquely map a UE between the eNodeB and MME.

---

## Role in Session Establishment

During attach or call setup:

1. UE sends NAS message to eNodeB.
2. eNodeB wraps NAS inside S1-AP.
3. S1-AP forwards to MME.
4. MME responds via S1-AP.
5. Bearers are created via coordination with [[GTPv2]].

S1-AP does not carry user data.

---

## Relationship with NAS

S1-AP acts as a transport wrapper for:

NAS messages

NAS handles authentication and mobility logic.
S1-AP carries NAS between radio and core.

---

## Mobility Support

S1-AP supports:

- intra-LTE handovers
- path switch procedures
- context transfer
- UE release during idle transition

This allows seamless mobility without dropping sessions.

---

## Encoding
S1-AP messages are encoded using:

ASN.1 PER (Packed Encoding Rules)

This makes them binary and compact.

---

## Reliability
Reliability is provided by:

[[SCTP]]

SCTP supports:
- multi-homing
- ordered delivery
- congestion control

---

## Used In
LTE (4G EPC)  
VoLTE control procedures  
Attach procedures  
Bearer establishment  
Mobility management  

---

## Specification
3GPP TS 36.413 — S1 Application Protocol (S1AP)