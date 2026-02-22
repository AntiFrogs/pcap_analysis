# TCP Options

## Definition
TCP Options extend the standard [[TCP]] header to negotiate advanced capabilities during connection setup.

They are primarily exchanged during SYN packets.

## Common Options

### MSS — Maximum Segment Size
Defines largest payload size a host can receive.

Purpose:
Prevent fragmentation.

---

### Window Scale
Extends receive window beyond 65,535 bytes.

Formula:
Real Window = Advertised Window × 2^ScaleFactor

Required for high-bandwidth connections.

---

### SACK Permitted
Selective Acknowledgment support.

Allows receiver to report exactly which segments arrived successfully.

Improves performance on lossy networks.

---

### Timestamp
Adds timing information to packets.

Used for:
- RTT measurement
- PAWS protection (Protect Against Wrapped Sequence numbers)

---

## Why Options Matter
TCP options directly affect:

- throughput
- latency
- congestion handling
- compatibility

Misconfigured options can severely degrade performance.

## Negotiation Rule
Options must be agreed during handshake.

If not negotiated → cannot be used later.