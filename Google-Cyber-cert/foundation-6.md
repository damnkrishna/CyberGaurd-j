# Detection and Incident Response

## Core Security Systems

### IDS (Intrusion Detection System)
A passive monitoring system that analyzes network traffic and system activities to identify suspicious patterns and potential security threats. It alerts administrators but does not take automatic action to block threats.

### IPS (Intrusion Prevention System)
An active security solution that monitors network traffic in real-time and can automatically block or prevent detected threats. Unlike IDS, it sits inline with traffic and can take immediate action to stop attacks.

### EDR (Endpoint Detection and Response)
A security solution that continuously monitors and collects data from endpoint devices (computers, servers, mobile devices) to detect and respond to cyber threats. It provides visibility into endpoint activities and enables rapid threat investigation and remediation.

## Network Traffic Analysis

### Network Traffic Flows
The movement of data packets across a network between source and destination. Analyzing traffic flows helps identify normal patterns, detect anomalies, and understand network behavior for security monitoring.

### Packet Sniffer (Network Protocol Analyzer)
A tool that captures and analyzes data packets traveling across a network. It allows security professionals to inspect packet contents, decode protocols, and troubleshoot network issues or investigate security incidents.

### IOC (Indicator of Compromise)
Observable artifacts or evidence that suggest a system has been breached or compromised. Examples include unusual network traffic patterns, suspicious file hashes, malicious IP addresses, or unauthorized access attempts.

## Network Analysis Tools

### Wireshark
A popular open-source packet analyzer with a graphical interface that captures and displays network traffic in detail.

**Key Features:**
- **Filters**: Allow users to display specific traffic based on protocols, IP addresses, ports, or other criteria (e.g., `http`, `tcp.port == 443`, `ip.addr == 192.168.1.1`)
- **Follow Streams**: Enables viewing complete TCP, UDP, or HTTP conversations between hosts, making it easier to reconstruct communication sessions

### tcpdump
A command-line packet analyzer commonly used on Unix/Linux systems for capturing and analyzing network traffic.

**Key Features:**
- **Filters**: Command-line expressions to capture specific traffic (e.g., `tcp port 80`, `host 192.168.1.1`, `icmp`)
- **Flags**: Options that control capture behavior such as `-i` (interface), `-w` (write to file), `-r` (read from file), `-n` (no name resolution), `-v` (verbose output)
