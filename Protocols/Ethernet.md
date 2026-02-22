# Ethernet

## Definition
Ethernet is a Layer-2 (Data Link) protocol that transports frames between devices on the same local network segment.

## Core Responsibilities
- framing data for transmission
- local delivery using MAC addresses
- error detection via FCS
- media access control

## Addressing
Ethernet uses 48-bit MAC addresses:

Format:
AA:BB:CC:DD:EE:FF

Structure:
- first 24 bits → vendor OUI
- last 24 bits → device identifier

## Frame Format
Destination MAC  
Source MAC  
EtherType / Length  
Payload  
Frame Check Sequence (FCS)

## EtherType Examples
0x0800 → IPv4  
0x86DD → IPv6  
0x0806 → ARP  

## Frame Types
Unicast — one device  
Broadcast — all devices  
Multicast — group  

## MTU
Standard Ethernet MTU = 1500 bytes

## Encapsulation Role
Ethernet carries Layer-3 protocols such as:
- [[IP]]
- ARP
- VLAN-tagged frames

## Diagnostic Insights
Frequent broadcasts → network noise or scanning  
Unknown OUIs → unknown devices  
CRC errors → physical layer problems