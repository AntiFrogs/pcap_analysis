# ICMP — Internet Control Message Protocol

## Definition
ICMP is a network diagnostic and error-reporting protocol used by IP devices.

---

## Purpose
- report delivery errors
- test connectivity
- measure latency
- provide routing feedback

---

## Common Message Types
0 → Echo Reply  
3 → Destination Unreachable  
8 → Echo Request  
11 → Time Exceeded  

---

## Echo Mechanism
Echo Request → sent to target  
Echo Reply → returned by target  

Used by the "ping" utility.

---

## Behavior
ICMP does not carry application data.  
It carries control or diagnostic information.

---

## Transport
ICMP is carried directly inside [[IP]] packets.

It does not use TCP or UDP.

---

## Diagnostic Value
Missing replies → connectivity issue  
High RTT → latency problem  
TTL exceeded → routing loop  

---

## Security Note
ICMP is sometimes filtered by firewalls to prevent network probing.