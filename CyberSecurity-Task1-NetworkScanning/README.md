# Task 1: Basic Network Scanning with Nmap

**Internship:** Oasis Infobyte – Security Analyst  
**Intern:** Naol Mesfin  
**Tool:** Nmap 7.94SVN  
**Operating System:** Ubuntu Linux (VirtualBox VM)  
**Target IP:** `10.0.2.15`

## 1. Introduction

Nmap (Network Mapper) is an open-source network scanning tool used to discover hosts, identify open ports, detect running services, and gather information about operating systems.

Network scanning is important in cybersecurity because it helps security analysts understand which services are exposed on a network and identify potential security risks.

## 2. Objectives

The objectives of this task are to:

- Perform a basic network scan using Nmap.
- Identify open and closed TCP ports.
- Perform service version detection.
- Attempt operating system detection.
- Analyze the scan results from a security perspective.

## 3. Tools and Environment

| Component | Details |
|---|---|
| Operating System | Ubuntu Linux |
| Virtualization | Oracle VirtualBox |
| Scanner | Nmap 7.94SVN |
| Target | Local Ubuntu VM |
| Target IP | 10.0.2.15 |

### Nmap Installation

On Ubuntu, Nmap can be installed using:

```bash
sudo apt update
sudo apt install nmap
```

Verify the installation:

```bash
nmap --version
```

##
