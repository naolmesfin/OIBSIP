# Wireshark Network Traffic Analysis Report

## 1. Introduction

This report documents practical network traffic analysis performed using Wireshark on an Ubuntu 24.04 virtual machine. The purpose was to observe network communication and understand the behavior of common protocols from a network security perspective.

## 2. Environment

- Operating System: Ubuntu 24.04 LTS
- Virtualization: Oracle VirtualBox
- Network Interface: `enp0s3`
- Local IP Address: `10.0.2.15`
- Analysis Tool: Wireshark

## 3. DNS Traffic Analysis

**Display filter:**
```text
dns
```

A DNS query for `connectivity-check.ubuntu.com` was observed.

The query requested an AAAA record, which is used to obtain an IPv6 address.

**Response filter:**
```text
dns.flags.response == 1
```

DNS responses containing IPv6 addresses were observed.

**Security observation:** DNS traffic can reveal the domain names a device attempts to resolve. This information can be useful for network monitoring and identifying unusual domain lookups.

## 4. TCP Traffic Analysis

**Display filter:**
```text
tcp.port == 80 && tcp.port == 51568
```

The capture showed:

- Source port `51568` sending a SYN packet to destination port `80`.
- Port `80` responding with an RST, ACK packet.

The RST flag indicates that the connection attempt was reset. The three-way TCP handshake was therefore not completed in this observed exchange.

**Security observation:** TCP flags provide useful information about connection behavior. Unexpected connection resets can be investigated during network troubleshooting and security monitoring.

## 5. HTTP Traffic Analysis

**Display filter:**
```text
http
```

An HTTP GET request was inspected.

Observed packet details:

- Source IP: `10.0.2.15`
- Destination IP: `142.250.151.102`
- Host: `clients2.google.com`
- Method: `GET`
- Request path: `/time/1/current`

The request demonstrated how HTTP headers and request paths can be inspected in a packet capture.

**Security observation:** HTTP does not encrypt application data. Request details and query parameters may be visible to someone who can capture the traffic. Sensitive values should not be exposed in publicly shared packet captures or screenshots.

## 6. TLS Traffic Analysis

**Display filter:**
```text
tls
```

The capture contained TLS Client Hello and Server Hello messages.

### 6.1 Client Hello

The Client Hello included a Server Name Indication (SNI) extension.

Observed server name:

`clients2.google.com`

SNI indicates the hostname the client is attempting to reach.

### 6.2 Server Hello

The Server Hello contained a `supported_versions` extension.

Observed negotiated version:

`TLS 1.3 (0x0304)`

The legacy version field displayed TLS 1.2 (`0x0303`), but the supported_versions extension confirmed TLS 1.3.

### 6.3 Application Data

TLS Application Data packets were also observed.

These records indicate encrypted application traffic. The application contents were not inspected or decrypted.

**Security observation:** TLS 1.3 protects application data through encryption. However, some connection metadata, including conventional unencrypted SNI, may still be visible.

## 7. Summary of Findings

| Protocol | Observation |
|---|---|
| DNS | Ubuntu connectivity-check query and IPv6 responses |
| TCP | SYN followed by RST, ACK |
| HTTP | GET request to `clients2.google.com` |
| TLS | Client Hello and Server Hello |
| TLS version | TLS 1.3 confirmed through supported_versions |
| TLS Application Data | Encrypted application traffic observed |

## 8. Conclusion

The practical exercise provided experience in capturing and analyzing network traffic using Wireshark. It improved my understanding of DNS resolution, TCP connection behavior, HTTP communication, and TLS encryption.

The analysis also demonstrated how packet inspection can help network security analysts understand communication patterns, identify potential exposure of sensitive information, and investigate unusual network behavior.

## 9. Disclaimer

All traffic was captured in my own Ubuntu virtual machine environment for educational and defensive network analysis purposes.
