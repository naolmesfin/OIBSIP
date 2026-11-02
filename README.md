# Task 8: Wireshark Network Traffic Analysis

## Overview
This project focuses on capturing and analyzing network traffic using Wireshark to understand how devices communicate over a network and identify important security observations.

## Objectives
- Capture live network traffic.
- Analyze DNS queries and responses.
- Examine TCP connection behavior.
- Inspect HTTP requests.
- Understand TLS handshakes and encrypted application traffic.
- Identify potential network security and privacy concerns.

## Tools and Environment
- **Tool:** Wireshark
- **Operating System:** Ubuntu 24.04 LTS
- **Network Interface:** `enp0s3`
- **Capture Environment:** Ubuntu virtual machine running in VirtualBox

## Analysis Performed

### 1. DNS Analysis
Examined DNS queries and responses, including a query for `connectivity-check.ubuntu.com`.

Observed an AAAA query, which requests an IPv6 address.

### 2. TCP Analysis
Inspected TCP connection behavior, including:
- SYN packet from source port `51568` to destination port `80`.
- RST, ACK response from port `80` to port `51568`.

The response indicated that the connection attempt was reset.

### 3. HTTP Analysis
Inspected an HTTP GET request with the following observations:
- Source IP: `10.0.2.15`
- Destination IP: `142.250.151.102`
- Host: `clients2.google.com`
- Request path: `/time/1/current`

This demonstrated how HTTP request metadata can be visible in an unencrypted capture.

### 4. TLS Analysis
Inspected TLS Client Hello and Server Hello messages.

Findings:
- Server Name Indication (SNI): `clients2.google.com`
- Negotiated TLS version: TLS 1.3 (`0x0304`)
- TLS Application Data packets were observed.

This demonstrated how TLS protects application data while some connection metadata, such as the hostname in a conventional SNI extension, may remain visible.

## Security Observations
- DNS traffic can reveal the domains a device attempts to access.
- TCP flags help identify connection establishment and reset behavior.
- Unencrypted HTTP traffic can expose request information.
- TLS 1.3 provides encryption for application data
