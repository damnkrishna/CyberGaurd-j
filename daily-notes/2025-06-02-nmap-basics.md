# Nmap Basics – June 2, 2025

nmap is basically used for scanning networks available or connected to the same Wi-Fi network. It is used a lot by hackers in cafés and open places to scan for connected devices, then identify their open ports and find vulnerabilities in their laptops, and exploit those vulnerabilities to own them.

## What I learned today:
- How to use `nmap` to scan for open ports on a local network.
- The command `nmap -sT 192.168.1.0/24 -p 3306` scans port 3306 on all devices.
- To scan for OS of connected devices.
- To scan for OS, viruses, passwords.
- To use decoy while scanning Wi-Fi to keep yourself anonymous.
- To scan the whole network using `sudo nmap --script vuln IP` and find all the vulnerabilities in the IP and through scripts.

## Key commands:
- `-sT`: TCP Connect scan
- `-p`: Specify ports
- `-sS`: To scan using stealth mode (not forming complete TCP connection with the device)
- `-O`: To scan for OS of device
- `-A`: For OS, virus, etc.
- `-D`: To use decoy by giving some IPs of other devices to scan target Wi-Fi or devices
- `sudo nmap --script vuln IP`: To scan the whole IP script, basically a complete scan for vulnerabilities (might take time)

## Notes:
- Make sure you are on the same network.
- Some devices may not respond if firewalled.
- Use decoy while scanning unknown devices or Wi-Fi like café Wi-Fi (can also use Tor or some tool to not give actual IP).
- Use stealth mode even while scanning known devices or websites. This will stop complete 3-way connection with it and just give us what we need without connecting.
- If you have time and a decent laptop, you should run a complete vulnerability scan on IP (also if you don’t know the vulnerability).
