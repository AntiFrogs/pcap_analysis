# TCP — Transmission Control Protocol

## Definition
TCP is a reliable, connection-oriented transport protocol that guarantees ordered data delivery between hosts.

## Core Features
- reliability
- retransmission
- congestion control
- flow control
- sequencing
- acknowledgment

## Connection Lifecycle
1. SYN
2. SYN-ACK
3. ACK
4. Data exchange
5. FIN/ACK termination

This is called the three-way handshake + graceful close.

## Header Fields
Source Port  
Destination Port  
Sequence Number  
Acknowledgment Number  
Window Size  
Flags  
Checksum  
Options  

## Flags
SYN → open connection  
ACK → acknowledge data  
FIN → close connection  
RST → reset connection  
PSH → push data immediately  

## Flow Control
TCP uses a receive window to prevent sender overload.

Receiver advertises:
how much data it can accept.

## Congestion Control
TCP dynamically adjusts transmission rate using algorithms such as:

- slow start
- congestion avoidance
- fast retransmit
- fast recovery

## Reliability Mechanisms
Lost packet → retransmitted  
Out-of-order packet → buffered  
Duplicate packet → discarded  

## Guarantees
TCP guarantees:
- ordered delivery
- no duplication
- no data loss (if connection survives)

## Limitations
TCP does not guarantee:
- latency
- timing
- real-time delivery

For real-time traffic, protocols use [[UDP]] instead.