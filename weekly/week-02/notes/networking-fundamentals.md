# IPv4 addressing and network boundaries

[Overview](../README.md) | [DHCP lab](../labs/lab-01-dhcp-connectivity.md) | [Application lab](../labs/lab-03-application-troubleshooting.md)

These are reference notes, not a record of additional tests. They summarize relevant concepts from the reviewed private Week 02 notes, particularly Modules 08 and 09 and the gateway discussion in Module 12. The course document is not redistributed.

## Address and subnet

An IPv4 address contains 32 bits, conventionally written as four decimal octets. An address belongs to an interface. The configured subnet mask or prefix identifies its network portion.

For the Lab 03 client:

| Item | Value |
|---|---|
| Address | `192.168.50.10` |
| Mask / prefix | `255.255.255.0` / `/24` |
| Network | `192.168.50.0/24` |
| Server | `192.168.50.20/24` |

These two configured hosts share a subnet and can communicate over the depicted switched LAN without a default gateway. For a general local-versus-remote decision, apply the host's mask to its own address and to the destination, then compare the resulting network portions. Comparing the first three octets works for these /24 examples, not for every possible mask.

Hosts in the same subnet need distinct usable addresses. A correct address alone is insufficient if the mask, link, or other required configuration is wrong.

## Private and special-use addresses

| Purpose | IPv4 block |
|---|---|
| RFC 1918 private space | `10.0.0.0/8` |
| RFC 1918 private space | `172.16.0.0/12` |
| RFC 1918 private space | `192.168.0.0/16` |
| Loopback | `127.0.0.0/8` |
| IPv4 link-local | `169.254.0.0/16` |

The private block prefix describes the reserved block, not a mandatory mask for every subnet within it. For example, a /24 subnet can be selected from `192.168.0.0/16`. Only `172.16` through `172.31` belongs to the listed 172 private block.

Private addresses can be routed between internal networks. They are not globally routed through the public Internet. Private addressing by itself is not a security guarantee.

Loopback communication stays within the host. A successful loopback ping does not verify a cable, switch, gateway, or remote server. IPv4 link-local self-assignment can occur when normal address acquisition is unavailable. The failed DHCP screenshot in Lab 01 does not show an assigned `169.254` address, so this reference concept must not be reported as an observed lab result.

## Delivery and broadcast boundaries

- Unicast addresses one recipient.
- Limited broadcast uses destination `255.255.255.255` on the local network.
- Multicast addresses a group, rather than every host on a subnet.

Ethernet broadcast forwarding occurs within the relevant Layer 2 domain. Routers do not simply forward the original Ethernet broadcast across routed interfaces. Dividing an address block into subnets does not, by itself, create separate Layer 2 broadcast domains; the topology must provide the corresponding separation.

The Week 02 reports do not include multicast tests, VLAN configuration, or an advanced subnetting exercise. Those concepts should remain distinct from the DHCP, NAT, DNS, and HTTP observations.
