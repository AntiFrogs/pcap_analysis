# RTP — Real-time Transport Protocol

## Purpose
RTP transports real-time media such as audio or video.

## Layer
Application-layer media protocol (runs over UDP)

## Characteristics
- real-time delivery
- sequence numbers
- timestamps
- jitter handling

## Header Fields
Version — protocol version  
Sequence Number — packet order  
Timestamp — timing reference  
SSRC — stream identifier  
Payload Type — codec used  

## Why UDP
Real-time traffic prefers speed over reliability. Lost packets are better than delayed packets.

## Companion Protocol
RTCP monitors quality and reports statistics.

## Dependency Stack
[[RTP]] → [[UDP]] → [[IP]]

## Diagnostic Clues
Sequence gaps → packet loss  
Timestamp jumps → jitter or clock issues  
Wrong payload type → decoding failure  

## Example Capture
See [[SIP Opus Call]]