# IP — Internet Protocol

## Purpose
IP delivers packets between hosts across networks.

## Version Types
IPv4 — 32-bit addressing  
IPv6 — 128-bit addressing  

## Core Responsibilities
- addressing
- routing
- fragmentation
- packet delivery

## Important Fields
Source address  
Destination address  
TTL — hop limit  
Protocol — next layer type  

## Fragmentation
Occurs when packet > MTU.  
May cause performance or delivery issues.

## Diagnostic Clues
Low TTL → routing loops  
Fragments → MTU problems  
Wrong source → NAT or spoofing  

## Layer Role
Foundation layer for all network protocols.

## Example Capture
See [[SIP Opus Call]]