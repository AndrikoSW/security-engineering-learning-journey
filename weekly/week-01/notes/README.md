# Week 01 Study Notes

These notes summarize the Week 01 lab discussion in original wording. Cisco course modules and activity files are not reproduced here.

## Local and remote destinations

PC-A uses its IPv4 address and subnet mask to decide whether the destination is on its own subnet. With `192.168.1.10/24`, the destination `192.168.1.1` is local, while `10.0.0.50` is remote. For this remote destination, PC-A sends through its default gateway, `192.168.1.1`.

## Keep the three tables separate

| Mechanism | Mapping or decision | Example from the lab |
|---|---|---|
| Host or router ARP cache | Local IPv4 address → MAC address | PC-A resolves `192.168.1.1` to R1's local MAC |
| Switch MAC address table | Source MAC learned on an incoming port | S1 learns PC-A and R1 on different ports |
| Router routing table | Destination IP → outgoing interface or next hop | R1 forwards toward the directly connected `10.0.0.0/24` network |

## Packet journey

1. PC-A resolves its gateway MAC with ARP.
2. S1 forwards the Ethernet frame toward R1.
3. R1 removes the incoming Ethernet frame and makes a routing decision.
4. R1 resolves Server-B's MAC on its outgoing network when required.
5. R1 creates a new Ethernet frame and forwards the IPv4 packet.

The first destination MAC belongs to R1, while the destination IPv4 address is `10.0.0.50`. After R1 forwards the packet, the source and destination MAC addresses belong to R1's outgoing interface and Server-B. The end-host IPv4 addresses stay the same in this lab, which does not use NAT. The captured TTL decreases from 128 to 127.

## State and troubleshooting

ARP cache entries belong to individual devices. Clearing PC-A's cache does not clear R1's cache. A repeated ping may reuse valid entries.

When PC-A uses the nonexistent gateway `192.168.1.254`, it repeatedly requests that gateway's MAC and receives no reply. Remote transmission cannot proceed normally, while a local ping to `192.168.1.1` can still work. Restoring `192.168.1.1` and testing again isolates and confirms the correction.

See the [lab report](../lab/README.md) for the detailed observations and [screenshots](../evidence/README.md) for the supplied evidence.
