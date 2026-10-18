# Simulator files and activity provenance

| Lab | Source format | Public availability |
|---|---|---|
| 01: DHCP | `.pkt` | Withheld because it derives from a Cisco learning activity |
| 02: NAT | `.pka` | Withheld because it derives from a Cisco learning activity |
| 03: Application troubleshooting | `.pkt` | [Original topology built from scratch](lab-03-application-troubleshooting.pkt) |

Lab 01 and Lab 02 used existing Cisco learning material. Reusing an activity for study does not establish permission to redistribute the activity or its derived simulator file. Those source files remain in the local learning archive. This repository contains my analysis, test results, and selected screenshots rather than copies of course PDFs or activity instructions.

The Lab 02 source retains its `.pka` extension. Renaming it to `.pkt` would not convert the format.

Open the Lab 03 project in Cisco Packet Tracer using File > Open. Work on a separate copy when repeating the failure sequence. The source was successfully reopened during the 18 October review in Packet Tracer 9.0.1; this is the review environment, not a verified minimum version requirement.

The [DHCP report](../lab-01-dhcp-connectivity.md) describes a small topology that can be recreated. The [NAT report](../lab-02-nat-packet-flow.md) explains how to repeat its packet comparison using an authorized copy of the activity; the external cluster is not fully specified by the screenshots.
