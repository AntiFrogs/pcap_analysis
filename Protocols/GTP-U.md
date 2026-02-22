# GTP-U — GPRS Tunneling Protocol (User Plane)

## Definition
GTP-U is a tunneling protocol used in mobile core networks to transport user data between network nodes.

It carries subscriber traffic across the core while keeping the original packets intact.

---

## Layer
Runs over:
[[UDP]] → [[IP]]

---

## Purpose
- transport user traffic through mobile core
- separate user traffic from control signaling
- multiplex many sessions over one path

---

## Tunnel Identification
Each tunnel is identified by:

TEID — Tunnel Endpoint Identifier

This value maps packets to a specific subscriber session.

---

## Header Fields
Version  
Protocol Type  
Message Type  
Length  
TEID  
Optional fields (sequence number, extension headers)

---

## Standard Port
UDP port **2152**

---

## Encapsulation Model
Outer Packet:
GTP + UDP + IP

Inner Packet:
Original user packet (IP, IPv6, etc.)

---

## Core Network Role
Used between nodes such as:

- base station
- serving gateway
- packet gateway

---

## Diagnostic Clues
Wrong TEID → wrong user session  
Missing replies → broken tunnel  
Out-of-order packets → transport issue  

---

## Relationship
[[GTP-U]] transports full packets that themselves contain [[IP]] traffic.