# SDP — Session Description Protocol

## Purpose
SDP describes multimedia session parameters. It does not transport media and does not control sessions. It only describes them.

## Used By
[[SIP]], WebRTC, RTSP

## Structure Fields
v — version  
o — owner/session ID  
s — session name  
c — connection info  
t — time  
m — media description  
a — attributes  

## Media Line Format
m=< media > < port > < protocol > < payload types >

Example meaning:
audio 6000 RTP/AVP 99

## Attributes
rtpmap — codec mapping  
fmtp — codec parameters  
ptime — packet duration  
sendrecv — bidirectional media  
sendonly — transmit only  
recvonly — receive only  

## Negotiation Model
Offer/Answer

Caller sends offer → Callee returns answer

## Relationship Chain
[[SIP]] negotiates  
[[SDP]] describes  
[[RTP]] carries  

## Diagnostic Clues
Wrong codec → no audio  
Port mismatch → no media  
Direction mismatch → one-way audio  

## Example Capture
See [[SIP Opus Call]]