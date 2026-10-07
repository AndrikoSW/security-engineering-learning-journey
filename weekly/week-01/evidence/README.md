# Week 01 Evidence

Supplied diagram and screenshots from the personal Packet Tracer lab. The diagram summarizes the packet flow; screenshots show the captured observations.

| File | What it shows |
|---|---|
| [Packet flow diagram](pc-to-remote-server-packet-flow.png) | Two networks, per-link MAC addresses, end-host IP addresses, and TTL |
| [Lab topology](lab-topology.png) | PC-A → S1 → R1 → S2 → Server-B |
| [Gateway ARP request](arp-request-gateway.png) | PC-A resolves `192.168.1.1` |
| [S1 MAC learning](s1-mac-learning.png) | Dynamic entries for PC-A and R1 |
| [Remote IP and local next hop](remote-ip-local-next-hop.png) | `Dst IP = 10.0.0.50`, Ethernet destination = R1 |
| [R1 ARP request](r1-arp-server.png) | R1 resolves `10.0.0.50` on the second network |
| [R1 re-encapsulation](r1-reencapsulation.png) | New Ethernet addresses, unchanged end-host IP addresses, TTL 127 |
| [Wrong gateway ARP fields](wrong-gateway-failure.png) | Target IPv4 address `192.168.1.254` |
| [Wrong gateway event list](wrong-gateway-event-list.png) | Repeated ARP attempts and failed ICMP events |
| [Recovery verification](recovery-verification.png) | Gateway resolution and successful ICMP request/reply path |

The filenames use lowercase kebab-case. Private-range IP addresses and MAC addresses shown here belong to the simulated lab. Course PDFs, Cisco `.pka` activities, and unrelated documents are excluded.

[Week 01 overview](../README.md) · [Lab report](../lab/README.md) · [Topology file](../lab/topology.pkt)
