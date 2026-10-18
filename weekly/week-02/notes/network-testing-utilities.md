# Testing utilities and evidence limits

[Overview](../README.md) | [HTTP troubleshooting report](../labs/lab-03-application-troubleshooting.md)

The reviewed private PDF contains Module 15 material on `netstat`, Module 16 material on `nslookup`, and DHCP/ping examples. It does not contain a detailed Module 17 section. This file therefore combines those reviewed concepts with the actual lab evidence. Items explicitly marked supplementary are a reference for planned Week 03 work, not a claim to summarize missing Module 17 notes or completed tests.

## Commands visible in the lab evidence

| Tool | What to inspect | What success does not establish |
|---|---|---|
| `ipconfig /all` | Assigned address, mask, gateway, DHCP server, and DNS settings | That the gateway, DNS server, or application is reachable |
| `ping` | Replies and loss for the tested ICMP exchange | That DNS or HTTP works, or every protocol is allowed |
| `nslookup` | Responding DNS server and returned records | That a web service accepts connections or serves a page |
| Packet Tracer Web Browser | Requested URL and displayed page or error | Every TCP exchange, all resources, or the general health of the network |

The reports link the actual outputs. This reference does not generate sample command output or substitute course demonstrations for my own results.

The Lab 03 commands were:

```text
ping 192.168.50.20
nslookup www.training.test
```

The browser test used `http://www.training.test`. During the injected HTTP failure, the first two tests still succeeded. That pattern helps separate the affected service from the functions that the tests show remained available.

## Reading netstat

The reviewed Module 15 notes describe `netstat` and `netstat -n`. The numeric option makes addresses and ports easier to compare with configuration and packet fields.

- Local Address describes the endpoint on the host running the command.
- Foreign Address describes the remote endpoint, not a foreign country.
- State describes a TCP connection state in the relevant output.
- ESTABLISHED indicates a formed connection, not proof of active data transfer at the instant of observation.

No `netstat` capture is included in these three lab evidence sets. An unfamiliar connection can justify further investigation, but is not by itself evidence of malware.

## Supplementary preparation for Week 03

The following tools are planned references. No output from them is claimed as a completed Week 02 practical test here.

| Tool | Intended question | Interpretation limit |
|---|---|---|
| Windows `tracert` | Which hops respond while probing the path? | Missing replies do not alone identify a failed forwarding device |
| `arp -a` | Which IPv4-to-MAC cache entries exist on the local host? | It is not a complete inventory of all reachable devices or remote hosts |
| Windows `netstat -ano` | Which connections/listeners and process IDs are visible? | A PID or port alone does not prove the application's legitimacy |

These are supplementary command references. Availability and detailed behavior can differ between Windows and Packet Tracer's simulated clients.

## Record conclusions at the level the test supports

Use these evidence labels in the reports:

- **Observed:** a value or outcome is directly visible in a capture.
- **Inferred:** an explanation follows reasonably from the available evidence.
- **Verified:** an appropriate test confirms the particular result being claimed.
- **Not verified:** the evidence is insufficient or the relevant test was not performed.

Record baseline, changed setting, repeated checks, and recovery separately. State which variables were held constant. Lab 01's mismatched pool limits isolation of a single cause, while Lab 03 provides a clearer service-specific comparison. Preserve that difference instead of making both experiments sound equally conclusive.
