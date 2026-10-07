# Week 01 — Networking Foundations

**Period:** 1–7 October 2026  
**Focus:** Network communication fundamentals and packet delivery  
**Status:** Completed — hands-on verification passed  
**Primary Lab:** [PC to Remote Server Packet Flow](lab/README.md)  
**Files:** [Packet Tracer topology](lab/topology.pkt) · [Evidence index](evidence/README.md)

---

## 1. Weekly Overview

The goal of Week 01 was to build a foundational understanding of how devices communicate across local and remote IPv4 networks.

The week focused on protocols, Ethernet switching, ARP, IPv4 addressing, routing, default gateways, network segmentation, and the relationship between Layer 2 and Layer 3 addressing.

The main practical objective was to predict and then verify the journey of traffic from a host on one network to a server on another network through a router.

Rather than treating successful connectivity as sufficient evidence, the lab followed a **predict → test → observe → troubleshoot → recover** workflow.

---

## 2. Learning Completed

| Topic | Material | Status |
|---|---|---|
| Protocols, TCP/IP, OSI, and encapsulation | Cisco Networking Basics — Module 5 | Completed |
| Ethernet frames and switching | Cisco Networking Basics — Module 7 | Completed |
| IPv4, ARP, and local vs. remote communication | Cisco Networking Basics — Module 13 | Completed |
| Routing, default gateway, and network segmentation | Cisco Networking Basics — Module 14 | Completed |

Supporting study notes are available in [`notes/`](notes/README.md).

---

## 3. Skills Demonstrated

| Demonstrated capability | Evidence |
|---|---|
| Determine whether an IPv4 destination is local or remote based on the host address and subnet mask | [Lab Report](lab/README.md) |
| Explain and verify ARP resolution for a default gateway | [ARP Gateway Evidence](evidence/arp-request-gateway.png) |
| Verify Ethernet switch MAC learning and forwarding behavior | [MAC Learning Evidence](evidence/s1-mac-learning.png) |
| Distinguish final Layer 3 destination from the Layer 2 next hop | [IP vs. Next-Hop Evidence](evidence/remote-ip-local-next-hop.png) |
| Verify router de-encapsulation, forwarding, and Layer 2 re-encapsulation | [Router Forwarding Evidence](evidence/r1-reencapsulation.png) |
| Diagnose and recover from an incorrect default gateway configuration | [Lab Troubleshooting](lab/README.md) |

---

## 4. Practical Work

The Week 01 practical exercise was built in Cisco Packet Tracer using two IPv4 networks connected by a router.

PC-A (`192.168.1.10/24`) communicated with Server-B (`10.0.0.50/24`) through R1. Simulation Mode was used to inspect ARP and ICMP traffic at multiple points in the topology.

Before observing the simulation, I predicted the expected ARP targets, Layer 2 source and destination addresses, IPv4 endpoints, switch behavior, and router forwarding process.

The observations were then compared against those predictions.

![Packet Flow Diagram](evidence/pc-to-remote-server-packet-flow.png)

Detailed topology, observations, predictions, and reproduction steps are documented in the [lab report](lab/README.md).

---

## 5. Validation Results

| Test | Expected Result | Actual Result | Status | Evidence |
|---|---|---|---|---|
| Initial remote communication | PC-A resolves the default gateway MAC before sending remote traffic | ARP for `192.168.1.1` occurred before ICMP forwarding | Pass | [Evidence](evidence/arp-request-gateway.png) |
| Layer 2 / Layer 3 forwarding | Destination IP remains Server-B while the first Ethernet frame targets R1 | Observed `Dst IP = 10.0.0.50` and `Dst MAC = R1` | Pass | [Evidence](evidence/remote-ip-local-next-hop.png) |
| Router forwarding | R1 creates a new Layer 2 frame on the second network | Source and destination MAC addresses changed while end-host IP addresses remained | Pass | [Evidence](evidence/r1-reencapsulation.png) |
| Subsequent communication | Existing ARP information prevents unnecessary ARP resolution | Later ICMP traffic proceeded without repeating the initial ARP process | Pass | [Lab Report](lab/README.md) |
| ARP-state variation | Clearing only PC-A's ARP cache should trigger only local gateway resolution | PC-A repeated gateway ARP while R1 retained its Server-B mapping | Pass | [Lab Report](lab/README.md) |
| Wrong default gateway | Local communication remains available while remote communication fails | R1 remained locally reachable while remote traffic failed at gateway resolution | Pass | [Failure Evidence](evidence/wrong-gateway-failure.png) |
| Recovery verification | Restoring the correct gateway should restore remote connectivity | ARP resolution succeeded and ICMP reached Server-B again | Pass | [Recovery Evidence](evidence/recovery-verification.png) |

---

## 6. Troubleshooting and Corrections

One intentional fault was introduced by changing PC-A's default gateway from `192.168.1.1` to `192.168.1.254`.

Local communication with R1 still succeeded because the destination was inside PC-A's own subnet. Remote communication failed because PC-A attempted to resolve the MAC address of the incorrect gateway.

Simulation Mode showed repeated ARP requests for `192.168.1.254` with no ARP reply. This demonstrated that the failure occurred before the remote ICMP traffic could be forwarded by the router.

The gateway was restored to `192.168.1.1`, the host ARP state was cleared, and remote communication was tested again. ARP resolution succeeded and end-to-end ICMP connectivity was restored.

Several conceptual corrections were also identified during review, particularly the distinction between switch MAC learning, ARP resolution, and router forwarding.

---

## 7. Assistance and Limitations

AI assistance was used for technical questioning, prediction review, terminology correction, and post-lab discussion.

The Packet Tracer topology, device configuration, predictions, testing, fault injection, observations, and recovery verification were performed as part of the hands-on exercise.

This week demonstrates foundational IPv4, Ethernet, ARP, switching, and basic routing behavior only. It does **not** demonstrate proficiency with VLANs, ACLs, NAT, dynamic routing protocols, advanced subnetting, packet analysis with Wireshark, or production network troubleshooting.

---

## 8. Review and Next Steps

The strongest outcome from Week 01 was developing a clearer mental model of the separation between Layer 2 and Layer 3 forwarding.

The main area that required correction was terminology precision, particularly:

**Switch:** learns `Source MAC → Port`  
**ARP:** resolves a known local IPv4 address to a MAC address  
**Router:** removes the incoming Layer 2 frame, makes a forwarding decision using the destination IP, and re-encapsulates the packet for the next link.

Future exercises should continue using prediction before observation so that successful tool output is not mistaken for actual understanding.

Week 02 will build on these foundations with deeper IPv4 addressing, subnetting, and core network protocol practice.
