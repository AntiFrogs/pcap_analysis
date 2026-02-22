# UDP — User Datagram Protocol

## Purpose
UDP provides fast, connectionless transport.

## Characteristics
- no handshake
- no retransmission
- no ordering
- minimal overhead

## Header Fields
Source Port  
Destination Port  
Length  
Checksum  

## Why Real-Time Protocols Use It
Latency matters more than reliability.

## Common Protocols Using UDP
DNS  
SIP  
RTP  
DHCP  

## Diagnostic Clues
Loss → application artifacts  
Port mismatch → no communication  

## Relationship
Transport layer between [[IP]] and application protocols.

## Example Capture
See [[SIP Opus Call]]