# Transport and application services

[Overview](../README.md) | [NAT request evidence](../labs/lab-02-nat-packet-flow.md) | [HTTP troubleshooting](../labs/lab-03-application-troubleshooting.md)

These supporting notes synthesize relevant material from the reviewed Module 15 and Module 16 notes. They are not additional test results.

## Transport protocols and endpoints

TCP provides an ordered byte stream with acknowledgements and retransmission mechanisms. Sequence and acknowledgement numbers track positions in that stream, not simply packet numbers. TCP can recover from some loss, but a connection can still fail.

UDP sends datagrams without built-in delivery, ordering, or retransmission guarantees. Applications may add their own mechanisms. Its smaller protocol machinery does not guarantee that an application will always be faster or free of delay.

TCP and UDP headers contain source and destination ports. Ports help identify application endpoints together with addresses and the transport protocol. A socket pair describes the two address-and-port endpoints of a conversation within its protocol context.

The NAT capture provides one concrete TCP request example:

| Endpoint before translation | Value |
|---|---|
| Client | `192.168.1.101:1027` |
| Server | `209.165.200.228:80` |

Port `1027` is an observed client source port. It is not a required source port for HTTP or a claim about the source-port range used by all operating systems.

## Selected conventional ports

| Service | Conventional transport and port | Reference meaning |
|---|---|---|
| DNS | UDP/TCP 53 | Name queries and other DNS exchanges |
| DHCPv4 | UDP 67 server, 68 client | Configuration acquisition |
| HTTP in these labs | TCP 80 | Web request and response |
| HTTPS over TCP | TCP 443 | HTTP protected using TLS |
| SSH | TCP 22 | Encrypted remote access |
| Telnet | TCP 23 | Remote terminal access without built-in encryption |
| FTP control | TCP 21 | File-transfer commands |
| SMTP | TCP 25 | Mail transfer between servers |

This is a reference table, not a list of services tested in Week 02. Port numbers are useful clues, but do not by themselves prove which application generated traffic. FTP data connections are separate from the control connection; their behavior should not be reduced to a universal assumption that every transfer uses the same data port.

## Name resolution, web exchange, and rendering

DNS supplies records such as an address associated with a hostname. In Lab 03, an A record maps `www.training.test` to `192.168.50.20`. A lookup result does not prove that an HTTP service is available at that address.

For the HTTP-over-TCP examples studied, the client needs a destination address, transport communication, and an HTTP response before it can display the returned content. A fresh DNS query is not required every time if suitable information is already cached.

HTTP governs request and response exchange. HTML describes document structure and content. A browser displaying a simple test page supports application-level success for that request; it does not expose every underlying exchange or verify every possible resource on the server.

HTTPS protects communication using TLS. It does not guarantee that the site is trustworthy or that its content is harmless. Lab 03 shows HTTPS enabled in the configuration, but does not contain an HTTPS access test.

## Applying the distinctions

The controlled Lab 03 failure illustrates three separate questions:

1. Did the tested ICMP exchange succeed?
2. Did the DNS query return the expected record?
3. Did the browser obtain and display the HTTP page?

The first two remained successful while the third failed after HTTP was disabled. The cause is supported by the injected setting and the comparison with baseline and recovery. Detailed TCP error behavior remains unverified without suitable packet evidence.

The private notes also discuss FTP, email, and remote access. Those discussions are study material; the three published reports do not establish successful FTP transfers, email delivery, or SSH administration.
