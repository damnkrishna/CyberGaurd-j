# Nmap Live Host Discovery

To check whether certain target is open and online or not:

- When a privileged user tries to scan targets on local network, nmap uses ARP requests
- When a privileged user scan target outside local network, nmap uses ICMP echo requests  
- When an unprivileged user tries to scan target outside local network, nmap resorts to TCP 3-way handshake to port 80 and 443

## Using ARP

- When on the same subnet as target system
- Same ethernet/wifi

**ARP scan:** 
```bash
nmap -PR -sn machine_ip/24
```
To discover all the live systems on same subnet

**arp-scan:** A tool built only for ARP scan queries
```bash
arp-scan --localnet
```
To scan all valid IPs on local network

## Using ICMP

- Many MS Windows firewalls block ICMP echo request by default

**ICMP Echo Request:** To use ICMP Echo request to discover live hosts
```bash
nmap -PE -sn target
```
- Doesn't return MAC address
- If returning MAC address then it might not be result of ICMP, it must be of ARP same subnet

**ICMP Timestamp Requests:** As most ICMP requests are blocked, you can try ICMP Timestamp Requests
```bash
nmap -PP -sn target
```

**ICMP Address Mask Queries:** We can also try ICMP Address Mask queries
```bash
nmap -PM -sn target
```

## Using TCP & UDP

### TCP SYN Ping
Send SYN flag set to TCP. An open port should reply with SYN/ACK
```bash
nmap -PS -sn target
```
- You can specify port otherwise it will take default port 80
- Example: `nmap -PS21 -sn target` for port 21

### TCP ACK Ping
Send packet with ACK flag set
```bash
nmap -PA -sn target
```
- Default port 80
- `-PA21` for port 21

**Note:**
- Privileged user: no need of TCP 3-way handshake
- Unprivileged user: must do TCP 3-way handshake

### UDP Ping
UDP packet to an open port is not expected to lead to a reply
```bash
nmap -PU -sn target
```
- Open UDP port => no response
- Closed UDP port => leads to ICMP destination unreachable -> port unreachable

### Masscan
Masscan is aggressive with rate of packets it generates:
- Finishes its network scan quickly
- Uses similar approach as TCP/UDP

```bash
masscan machine_ip/24 -p443
```

## Summary Table

### Scan Types

| **Scan Type** | **Example Command** |
|---------------|---------------------|
| ARP Scan | `sudo nmap -PR -sn MACHINE_IP/24` |
| ICMP Echo Scan | `sudo nmap -PE -sn MACHINE_IP/24` |
| ICMP Timestamp Scan | `sudo nmap -PP -sn MACHINE_IP/24` |
| ICMP Address Mask Scan | `sudo nmap -PM -sn MACHINE_IP/24` |
| TCP SYN Ping Scan | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30` |
| TCP ACK Ping Scan | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30` |
| UDP Ping Scan | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` |

Remember to add `-sn` if you are only interested in host discovery without port-scanning. Omitting `-sn` will let Nmap default to port-scanning the live hosts.

### Additional Options

| **Option** | **Purpose** |
|------------|-------------|
| `-n` | no DNS lookup |
| `-R` | reverse-DNS lookup for all hosts |
| `-sn` | host discovery only |
