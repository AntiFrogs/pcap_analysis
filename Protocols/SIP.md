# SIP — Session Initiation Protocol

## Purpose
SIP is a signaling protocol used to establish, modify, and terminate multimedia sessions such as VoIP calls, video calls, and conferencing.

## Layer
Application layer

## Transport
[[UDP]], [[TCP]], [[TLS]]

## Default Ports
5060 — standard  
5061 — TLS

## Core Functions
- session establishment
- capability negotiation
- call routing
- call teardown
- user location

## Message Types
### Requests
INVITE — start session  
ACK — confirm success  
BYE — end session  
REGISTER — register user  
OPTIONS — capability query  

### Responses
1xx — provisional  
2xx — success  
3xx — redirection  
4xx — client error  
5xx — server error  
6xx — global failure  

## Important Headers
Via — routing path  
From — caller identity  
To — callee identity  
Call-ID — unique dialog ID  
CSeq — transaction counter  
Contact — return address  

## Dialog Concept
A SIP dialog is identified by:
Call-ID + From tag + To tag

## Relationship to Other Protocols
Uses [[SDP]] to describe media  
Controls [[RTP]] streams  
Runs over [[UDP]] or [[IP]]

## Diagnostic Clues
Repeated INVITEs → retransmissions  
Missing ACK → session failure  
Wrong Contact → routing error

## Example Capture
See [[SIP Opus Call]]