# Week 01 Lab — PC to Remote Server Packet Flow

## Objective

This lab was designed to verify how a host communicates with a destination on a remote IPv4 network.

The main objectives were to:

- determine whether a destination is local or remote,
- observe ARP resolution for the default gateway,
- verify Ethernet switch MAC learning,
- distinguish Layer 2 next-hop addressing from Layer 3 end-to-end addressing,
- observe router de-encapsulation and re-encapsulation,
- compare first and subsequent transmissions,
- test ARP state changes,
- and troubleshoot an intentionally incorrect default gateway.

The lab followed a:

> **predict → test → observe → troubleshoot → recover**

workflow.

---

## Scope

### Included

- IPv4 addressing
- Subnet mask interpretation
- Local vs. remote destination decision
- Default gateway behavior
- ARP Request and ARP Reply
- Ethernet source and destination MAC addresses
- Switch MAC learning and forwarding
- Basic router forwarding
- Layer 2 re-encapsulation
- ICMP Echo Request / Echo Reply
- ARP cache behavior
- Basic connectivity troubleshooting

### Not Included

- VLANs
- ACLs
- NAT
- Dynamic routing protocols
- Advanced subnetting
- Wireshark
- Production network troubleshooting

---

## Topology

```text
192.168.1.0/24                         10.0.0.0/24

PC-A -------- S1 -------- R1 -------- S2 -------- Server-B
                        G0/0/0
                        192.168.1.1

                        G0/0/1
                        10.0.0.1
