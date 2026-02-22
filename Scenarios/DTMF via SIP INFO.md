# DTMF via SIP INFO

## Description
This scenario represents a SIP dialog where DTMF digits are transmitted using SIP INFO requests rather than RTP events or audio tones.

---

## Sequence

1. Client sends INVITE
2. Server processes request
3. Dialog established
4. Client sends INFO requests
5. Server acknowledges INFO
6. DTMF digits delivered successfully

---

## DTMF Transport Method
DTMF is carried inside SIP messages with:

Content-Type: application/dtmf-relay

Message body format:

Signal=< digit >
Duration=< ms >

---

## CANCEL Behavior in This Scenario
CANCEL requests appear in the trace and are acknowledged by the server with:

200 ok -- no more pending branches

This indicates the server accepted the cancel request but had no active branches left to terminate.

---

## What This Scenario Demonstrates
- SIP transaction independence
- Mid-dialog signaling
- DTMF delivery methods
- Proxy routing effects
- CANCEL handling logic

---

## Evidence
[[SIP DTMF INFO Session]]