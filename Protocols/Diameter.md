# Diameter — Authentication, Authorization, and Accounting Protocol

## Definition
Diameter is a signaling protocol used for Authentication, Authorization, and Accounting (AAA) in modern telecom networks.

It is the successor to RADIUS and is widely used in LTE, IMS, and core network architectures.

---

## Purpose
Diameter is responsible for:

- subscriber authentication
- policy control
- charging coordination
- session authorization
- mobility-related subscriber management

It is a control-plane protocol.

---

## Transport
Diameter typically runs over:

[[SCTP]] or [[TCP]]

It uses port 3868 by default.

SCTP is preferred in telecom environments due to multi-streaming and resilience.

---

## Architecture Model
Diameter operates in a peer-to-peer architecture.

Nodes include:

Client  
Server  
Relay  
Proxy  

Each node can route requests to appropriate destinations.

---

## Message Structure

Diameter messages consist of:

Header  
Attribute-Value Pairs (AVPs)

AVPs carry all protocol data.

---

## Core Concepts

### Command Codes
Each Diameter message is identified by a command code.

Examples:

- Capabilities-Exchange
- Credit-Control
- Authentication-Information
- Update-Location

---

### AVPs (Attribute-Value Pairs)
AVPs contain parameters such as:

- Session-Id
- User-Name
- Result-Code
- Origin-Host
- Destination-Realm
- Charging information

AVPs are extensible and vendor-specific extensions are allowed.

---

## Role in LTE

In LTE (EPC), Diameter is used on several interfaces:

S6a → MME ↔ HSS  
Gx → PGW ↔ PCRF  
Rx → IMS ↔ PCRF  
Gy → PGW ↔ OCS  

Diameter coordinates subscriber data and policy decisions.

---

## Example Workflow (LTE Attach)

1. UE sends attach request.
2. MME contacts HSS using Diameter.
3. HSS returns authentication vectors.
4. MME authorizes session.
5. Bearer setup proceeds via [[GTPv2]].

Diameter does not transport user data.

---

## Reliability
Reliability is provided by:

[[SCTP]] or [[TCP]]

Diameter itself is request/answer based.

Each request expects a corresponding answer.

---

## Security
Diameter may use:

[[TLS]] or IPsec for encryption.

Security is often mandatory in production telecom networks.

---

## Diagnostic Clues

Result-Code ≠ success → authentication or policy failure  
Repeated requests → routing or timeout issue  
No answer → peer unreachable  
Capability-Exchange failure → incompatible peers  

---

## What Diameter Does Not Do

It does not:

- carry media traffic
- establish tunnels
- transport SIP or RTP

It authorizes and controls sessions at the core network level.

---

## Relationship

[[Diameter]] works alongside:

- [[S1-AP]] for control signaling
- [[GTPv2]] for bearer setup
- [[SIP]] in IMS environments
- [[SCTP]] as transport

It is a core policy and authentication engine.

---

## Used In

LTE EPC  
IMS  
VoLTE policy control  
Charging systems  
5G core (legacy interworking)

---

## Specification

RFC 6733 — Diameter Base Protocol  
3GPP TS 29.272 — S6a interface  
3GPP TS 29.212 — Gx interface