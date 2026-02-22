# GTPv2 — GPRS Tunneling Protocol Version 2 (Control Plane)

## Definition
GTPv2 is the control-plane protocol used in LTE and EPC networks to create, modify, and delete bearer sessions.

It manages signaling between core network nodes.

---

## Role
Responsible for:
- session creation
- bearer management
- mobility handling
- QoS assignment
- tunnel setup

---

## Transport
Runs over:

[[UDP]] port 2123

---

## Message Types
Common messages:

Create Session Request  
Create Session Response  
Modify Bearer Request  
Delete Session Request  

Each message contains Information Elements (IEs).

---

## Key Identifiers

TEID — Tunnel Endpoint Identifier  
EPS Bearer ID — identifies logical bearer  

These values map subscriber sessions to tunnels.

---

## Information Elements
Examples:

- IMSI
- APN
- Bearer QoS
- F-TEID
- Cause codes

Each IE defines a specific parameter of a session.

---

## Reliability
	GTPv2 uses transaction identifiers and sequence numbers for request/response matching.

---

## Relationship
[[GTPv2]] controls tunnels used by [[GTP-U]].