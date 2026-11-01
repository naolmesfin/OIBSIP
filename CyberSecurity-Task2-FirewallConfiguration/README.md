# Task 2: Firewall Configuration Using UFW

## Internship
Oasis Infobyte Security Analyst Internship (OIBSIP)

## Objective
The objective of this task is to configure and manage a basic firewall using UFW (Uncomplicated Firewall) on Ubuntu Linux. The exercise demonstrates how firewall rules control incoming and outgoing network traffic and help protect a system from unauthorized connections.

## Tools and Environment
- Operating System: Ubuntu 24.04 LTS
- Firewall: UFW (Uncomplicated Firewall)
- Environment: Ubuntu Virtual Machine (VirtualBox)
- Terminal: Linux command line

## Methodology

### 1. Checking Firewall Status
The initial firewall status was checked using:

```bash
sudo ufw status verbose
```

The firewall was initially inactive.

### 2. Configuring Default Policies
The following policies were configured:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Incoming connections were denied by default, while outgoing connections were allowed.

### 3. Allowing HTTP and HTTPS Traffic
Rules were added to permit incoming web traffic:

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

- Port 80: HTTP traffic
- Port 443: HTTPS traffic

### 4. Enabling the Firewall

```bash
sudo ufw enable
```

The firewall was successfully activated.

### 5. Blocking an Unwanted Port

```bash
sudo ufw deny 8080/tcp
```

This rule explicitly blocks incoming TCP traffic on port 8080.

### 6. Configuring Firewall Logging

```bash
sudo ufw logging medium
```

Firewall logging was configured to medium level.

### 7. Verifying the Configuration

```bash
sudo ufw status verbose
sudo ufw status numbered
```

The commands confirmed that the firewall was active and the configured rules were present.

## Final Firewall Configuration

| Traffic / Port | Configuration |
|---|---|
| Incoming connections | Denied by default |
| Outgoing connections | Allowed by default |
| TCP port 80 | Allowed |
| TCP port 443 | Allowed |
| TCP port 8080 | Denied |
| Routed traffic | Denied by default |

The rules were applied to both IPv4 and IPv6.

## Security Analysis

The configured firewall provides a basic layer of host-based network protection.

- Denying incoming connections by default reduces exposure to unsolicited network access.
- Allowing outgoing connections supports normal communication initiated by the Ubuntu system.
- Allowing ports 80 and 443 permits incoming HTTP and HTTPS traffic.
- Explicitly denying port 8080 demonstrates how unwanted services can be blocked.
- Firewall logging helps administrators monitor network activity.

Allowing a port through the firewall does not mean a service is running or listening on that port. It only means UFW permits matching traffic.

## Conclusion

This task provided practical experience configuring a Linux firewall using UFW. I learned how to establish default traffic policies, allow specific services, block unwanted ports, enable firewall logging, and verify firewall rules.

The exercise demonstrated the importance of firewall configuration as part of a system's overall network security.

## Screenshots

The `screenshots` directory contains evidence of the firewall configuration:

1. `firewall_status.png` – Active firewall status, logging level, and default policies.
2. `firewall_rules.png` – Numbered ALLOW and DENY firewall rules.

## Ethical Considerations

All configuration and testing were performed on my own Ubuntu virtual machine in a controlled environment.
