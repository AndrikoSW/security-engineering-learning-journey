# DHCP, gateways, and NAT

[Overview](../README.md) | [DHCP report](../labs/lab-01-dhcp-connectivity.md) | [NAT report](../labs/lab-02-nat-packet-flow.md)

Reference basis: the reviewed private Week 02 notes for Modules 09, 11, and 12. The lab reports contain the test-specific observations. The explanations below are a concise synthesis rather than reproduced course text.

## DHCP assigns configuration

DHCP can supply an IPv4 address, mask, gateway, and additional options such as a DNS server. A server allocates addresses from its configured pool using leases. Dynamic assignment reduces repetitive manual configuration, but still depends on correct server settings and communication with clients.

The introductory acquisition sequence is:

| Message | Purpose |
|---|---|
| Discover | Client looks for a server |
| Offer | Server proposes configuration |
| Request | Client requests the selected allocation |
| ACK | Server confirms the allocation |

This DORA sequence is a reference concept. Lab 01 screenshots show service configuration, client results, and connectivity; they do not capture all four messages at packet level.

A lease is not necessarily a permanent reservation for one device. Assignment can depend on prior leases, availability, requests, and server policy. A device disconnecting does not necessarily release its address immediately. Lab 01's PC2 recovery and later inventory show different addresses and should be kept as separate states.

The Lab 01 configured pool contains 20 addresses, from `192.168.40.100` through `.119`. The router's `.1` address is outside that pool. The recorded DNS value of `0.0.0.0` does not demonstrate a usable DNS service.

## Gateway and DHCP roles

For a remote destination in these basic host configurations, the client sends traffic through its configured default gateway. On Ethernet it resolves the local gateway's MAC address when needed, while the IP destination remains the final host.

A home router can act as a DHCP server on the LAN and a DHCP client on the WAN. These are separate roles. A configured LAN DHCP pool does not prove that the router has working upstream connectivity.

## NAT changes packet addressing

Routing selects how to forward traffic; NAT translates addressing as part of the configured forwarding behavior. They are different functions. NAT does not permanently replace the private address configured on the client.

For the captured outbound HTTP request in Lab 02:

```text
Before: 192.168.1.101:1027 -> 209.165.200.228:80
After:  209.165.200.227:1027 -> 209.165.200.228:80
```

The source address changes and the ports remain the same in that observation. Some NAT behavior includes transport-port translation; this capture does not establish that ports are always preserved. The TTL decrement is associated with router forwarding and should be distinguished from address translation.

Theoretical reverse translation can direct replies to the corresponding internal endpoint. The Lab 02 evidence does not include a complete return-path inspection or a NAT table export, so it does not support inventing a specific mapping table or every packet in the response.

NAT does not encrypt communication and does not replace access-control policy. Its presence does not establish that a host, application, or network is secure.
