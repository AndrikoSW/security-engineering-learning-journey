# Week 02 Networking Fundamentals

[Learning journey](../../README.md) | [Previous week: Networking foundations](../week-01/README.md)

This week documents three Cisco Packet Tracer labs within my Security Engineering Learning Journey. I configured DHCP clients, compared a request before and after NAT, and tested a controlled HTTP failure while checking IP connectivity and DNS resolution separately.

The scheduled learning period was **8 to 14 October 2026**. Evidence collection and review continued through **18 October 2026**. The exercises took place in simulation.

Week 01 focused on Ethernet, ARP, and packet forwarding between networks. Week 02 extends that foundation with automatic client configuration, source address translation, and separate tests for IP connectivity, DNS, and HTTP.

## Lab reports

| Lab | Work and supported result |
|---|---|
| [01: DHCP and local connectivity](labs/lab-01-dhcp-connectivity.md) | Three clients held unique addresses within the configured pool. PC0 received 12 replies across three local ping tests. The failure/recovery captures include a pool discrepancy that limits a single-cause conclusion. |
| [02: NAT packet flow](labs/lab-02-nat-packet-flow.md) | The observed HTTP request changed source address from `192.168.1.101` to `209.165.200.227`. PC0 displayed the simulated external server's page. |
| [03: DNS and HTTP troubleshooting](labs/lab-03-application-troubleshooting.md) | Ping and DNS still succeeded when HTTP was deliberately disabled. The page loaded again after HTTP was restored. The stored project also passed a fresh HTTP check when reopened. |

## Selected evidence

### DHCP configuration and connectivity

![Three local ping tests with four replies each](evidence/lab-01-dhcp/06-connectivity-test.png)

The [topology](evidence/lab-01-dhcp/01-network-topology.png), [working pool](evidence/lab-01-dhcp/02-dhcp-server-configuration.png), [failed request](evidence/lab-01-dhcp/08-dhcp-request-failed.png), and [recovered request](evidence/lab-01-dhcp/10-dhcp-request-recovered.png) are linked in the full report. The disabled-service capture also shows a different pool; it should not be presented as a test with every other variable held constant.

### NAT request comparison

| Field | Before forwarding | After forwarding |
|---|---|---|
| Source IPv4 | `192.168.1.101` | `209.165.200.227` |
| Destination IPv4 | `209.165.200.228` | `209.165.200.228` |
| TCP source / destination | `1027` / `80` | `1027` / `80` |
| TTL | 128 | 127 |

Inspect the [topology](evidence/lab-02-nat/01-nat-topology.png), [inbound PDU](evidence/lab-02-nat/02-before-nat-pdu.png), [outbound PDU](evidence/lab-02-nat/03-after-nat-pdu.png), and [HTTP result](evidence/lab-02-nat/04-nat-verification.png). Port preservation is an observation about this request, not a rule for all NAT behavior.

### HTTP failure with working IP and DNS checks

![Browser reports Server Reset Connection](evidence/lab-03-application/08-http-access-failed.png)

Compare the [topology](evidence/lab-03-application/01-lab-topology.png), [baseline](evidence/lab-03-application/05-http-baseline.png), [successful ping and DNS during failure](evidence/lab-03-application/07-connectivity-dns-during-failure.png), and [recovered page](evidence/lab-03-application/10-http-recovery-verified.png). The report explains why the browser error alone does not establish the exact TCP failure sequence.

## Study notes

The supporting notes distinguish reference concepts from results tested in the labs:

- [IPv4 addressing and network boundaries](notes/networking-fundamentals.md)
- [DHCP, gateways, and NAT](notes/dhcp-and-nat.md)
- [Transport and application services](notes/transport-and-applications.md)
- [Testing utilities and evidence limits](notes/network-testing-utilities.md)

The reviewed private course notes cover Modules 08, 09, 11, 12, 15, and 16. Completion of Module 17 is recorded in the supplied learning record, but its detailed notes were not found in the reviewed PDF. The testing reference identifies supplementary material accordingly. Course PDFs are not redistributed here.

Assessment sources, practical review coverage, development areas, and planned Week 03 work are recorded in the [weekly review](assessment/week-02-review.md).

## Reproduction and source files

Use Cisco Packet Tracer and follow each lab report's procedure. The reports describe which values can vary between runs and where the supplied evidence does not specify a complete activity configuration.

The [Lab 03 project](labs/packet-tracer/lab-03-application-troubleshooting.pkt) is available as a `.pkt` file. I built its topology from scratch. Lab 01 and Lab 02 derive from Cisco learning activities, so their simulator files are withheld from public distribution. See [simulator availability and provenance](labs/packet-tracer/README.md). The Lab 02 source is a `.pka` activity, and has not been renamed or represented as a `.pkt` project.

Work on copies when reproducing failures. The original evidence records specific test runs; new runs should be documented separately.

## Findings and limits

DHCP acquisition, IP reachability, DNS resolution, and HTTP page loading answer different questions. A successful result at one stage does not establish application health at every other stage. Dynamic lease assignments can differ between recorded states without proving a configuration fault. NAT changes observed addressing; it does not provide encryption or a complete security policy.

Lab 03 was a guided controlled-failure exercise with a known injected cause. These labs do not establish independent production troubleshooting, enterprise deployment experience, a security assessment, or complete knowledge of every packet exchange. Observed results, reasonable inferences, verified tests, and unverified details are identified in the reports.

AI assistance supported technical discussion, evidence review, and documentation. The reports distinguish my configuration and test work from later documentation checks and supplementary explanation.
