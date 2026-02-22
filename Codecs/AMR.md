# AMR — Adaptive Multi-Rate Codec

## Definition
AMR is a speech audio codec designed for efficient voice compression and transmission over constrained or variable-quality networks.

It is optimized for real-time voice communication, especially in mobile and VoIP environments.

---

## Variants
Two main versions exist:

AMR-NB — Narrowband (8 kHz audio)  
AMR-WB — Wideband (16 kHz audio)

Wideband provides higher clarity and natural sound quality.

---

## Purpose
AMR compresses speech into low bit-rate streams while preserving intelligibility and robustness against packet loss and transmission errors.

---

## Key Characteristics
- adaptive bitrate selection
- error resilience
- low latency
- packet loss tolerance
- optimized for speech (not music)

---

## Bitrate Modes

### AMR-NB bitrates
4.75 – 12.2 kbps

### AMR-WB bitrates
6.6 – 23.85 kbps

Lower bitrate → lower bandwidth but reduced quality  
Higher bitrate → better quality but more bandwidth

---

## Adaptive Rate Switching
The codec can dynamically change bitrate during a call.

Network or radio conditions determine which rate is used.

This allows stable audio even when bandwidth fluctuates.

---

## Transport Usage
AMR is typically transported inside:

- [[RTP]] streams
- VoIP media sessions
- mobile voice channels

Payload type is negotiated using [[SDP]] during session setup.

---

## Frame Structure
AMR audio is transmitted in frames representing small segments of speech.

Typical frame duration:
20 milliseconds

Each frame contains encoded speech parameters rather than raw audio samples.

---

## Error Resilience
AMR includes built-in mechanisms to survive packet loss:

- frame interpolation
- redundancy bits
- error concealment

This prevents voice dropouts during network instability.

---

## Common Use Cases
- mobile voice calls
- VoLTE / VoNR
- SIP softphones
- IMS networks
- radio voice links

---

## Diagnostic Clues

Robotic audio → bitrate too low  
Choppy speech → packet loss  
Metallic sound → frame loss concealment active  
Silence gaps → RTP loss or jitter buffer underrun  

---

## Negotiation
AMR capability is negotiated during session setup.

Typically appears inside SDP as:

codec-name / sample-rate

Example format:
AMR-WB/16000

---

## Why AMR Matters
AMR is the dominant speech codec in cellular networks because it balances:

quality  
bandwidth efficiency  
robustness  

It is specifically engineered for real-time speech under imperfect network conditions.

---

## Summary
AMR is a speech-optimized adaptive codec that dynamically adjusts its bitrate to maintain intelligible audio across changing network conditions. It is a foundational technology for modern voice communication systems.