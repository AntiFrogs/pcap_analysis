# TLS — Transport Layer Security

## Definition
TLS is a cryptographic protocol that provides secure communication over an untrusted network. It ensures confidentiality, integrity, and authentication between two endpoints.

It is the successor to SSL and is the standard mechanism for securing application-layer protocols.

---

## Purpose
TLS protects data in transit by:

- encrypting payloads
- verifying peer identity
- preventing tampering
- detecting replay attacks

Without TLS, transmitted data can be read or modified by intermediaries.

---

## Layer Position
TLS operates between:

Application Layer  
Transport Layer

Example stack:

Application → [[TLS]] → [[TCP]] → [[IP]]

---

## Versions

SSL 2.0 — obsolete  
SSL 3.0 — obsolete  
TLS 1.0 — deprecated  
TLS 1.1 — deprecated  
TLS 1.2 — widely deployed  
TLS 1.3 — modern standard  

Modern systems should use TLS 1.2 or 1.3.

---

## Core Security Services

### Confidentiality
Data is encrypted so only intended recipient can read it.

### Integrity
Message authentication codes prevent modification.

### Authentication
Certificates verify server identity (and optionally client identity).

---

## TLS Handshake Overview

The handshake establishes secure parameters before application data is exchanged.

Typical sequence:

ClientHello  
ServerHello  
Certificate  
Key Exchange  
Finished  

After handshake completes, encrypted application data flows.

---

## Key Concepts

### Cipher Suite
Defines algorithms used for:

- key exchange
- encryption
- authentication
- hashing

---

### Session Keys
Temporary symmetric keys derived during handshake.

Used because symmetric encryption is faster than asymmetric encryption.

---

### Certificates
Digital documents binding identity to public keys.

Usually issued by a Certificate Authority (CA).

---

### Forward Secrecy
Modern TLS uses ephemeral keys so that even if long-term keys are compromised later, past sessions remain secure.

---

## Record Protocol
TLS transmits data in records.

Each record includes:

- encrypted payload
- authentication tag
- sequence number

---

## Transport
TLS typically runs over:

[[TCP]]

Variants exist:

DTLS — runs over [[UDP]] for real-time traffic

---

## Common Uses
HTTPS web traffic  
Secure email  
VPN tunnels  
VoIP signaling security  
API communication  
Authentication systems  

---

## Diagnostic Clues

Handshake failure → certificate issue or cipher mismatch  
Unknown CA → trust chain problem  
Repeated ClientHello → server not responding  
Alert messages → protocol or security error  

---

## Security Properties
TLS protects against:

- eavesdropping
- packet injection
- session hijacking
- MITM attacks (if certificates validated)

---

## Limitations
TLS does not protect:

- metadata (IP addresses, ports)
- traffic timing
- packet size patterns

It encrypts content, not network behavior.

---

## Relationship
[[TLS]] secures application protocols such as:

- HTTPS
- SIP over TLS
- IMAPS
- SMTPS

---

## Specification
RFC 8446 — TLS 1.3  
RFC 5246 — TLS 1.2