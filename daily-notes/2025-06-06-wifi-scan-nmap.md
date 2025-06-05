# Scanning Devices Connected to WiFi and Open Ports

I was hoping to scan for connected devices to my WiFi network, so I scanned for my WiFi IP first. Using nmap, I planned to scan for IP or MAC addresses of connected devices using `nmap -sn` which reveals the IPs of devices. But as I scanned, I didn't have the WiFi setting changed to bridged adapter, so I wasted a lot of time scanning my VirtualBox WiFi which only revealed my VirtualBox connected VMs and returned two IPs - both were my created virtual machines.

Later I scanned my actual OS WiFi using `ipconfig` in my cmd.

## Step by Step Process

### Check if host is up:
```bash
sudo nmap -sn 10.0.2.15
```

As my scan wasn't returning any list of connected devices, I identified that I should be scanning the whole range of WiFi rather than just scanning my WiFi IP.

### To identify the range of my WiFi IP:
```bash
ip a
```
Check for `inet 10.0.2.15/24` - this means I should scan from range 15-24 for WiFi IP which should return all connected devices.

### Perform nmap on range:
```bash
sudo nmap -sn 10.0.2.15/24
```

This returned a list of devices connected. I had to select one at a time, and since I wasn't hoping it to be a device of someone I don't know or might harm me in future, I decided to try identifying whose device it might be using three ways:

- Identify hostname
- Identify device using MAC address
- Use nbtscan (for Windows NETBIOS name)

Sometimes just scanning or sending packets might return hostname while responding back, but it didn't work for me. I performed:
```bash
ping -a ip
sudo nmap -sP ip
```

Since my output in bash didn't have the hostname, I proceeded with the nbtscan method. But I didn't get much using that either because:

- The firewall didn't support reply or blocked the reply from the IP/device
- Device might not support NetBIOS
- Device might not be a real Windows system

```bash
sudo nbtscan ip
```

Since both ways didn't work, I proceeded with trying to identify the MAC address using a website which told me about the type of device using the MAC address I provided.

I identified it was actually my own laptop VirtualBox which I built and not someone else's device which I was worried about. I understood I was doing something wrong and also somehow checked for safety and established safe practice environment for tools like nmap. I might be proceeding in this same environment soon for:

- Logging into MySQL (port 3306)
- SMB enumeration (port 445)
- Metasploit exploration (port 445 or 3306 or 135)

But rather than doing these things, I decided to move on with my goal to scan connected devices and identify their open ports.

## Actual WiFi Scanning

For identifying my actual WiFi IP, I performed `ipconfig` on my actual OS and identified my WiFi IPv4 address - it was actually so easy. Here I was thinking my laptop doesn't support network checkup and I'd have to spend money buying a WiFi adapter that would allow scanning WiFi and send SQL injection, but it wasn't necessary.

So I proceeded and performed my scan using my actual WiFi IP and subnet mask. Performing the WiFi scan, I got around 100 IPs of devices - even ones I didn't know had my WiFi password. Though I didn't try to identify each one of them, I picked one up and performed a port scan on that device. But most of them had all ports closed as majority were mobile Android phones or something.

So I decided to end the night here as I solved a lot of problems and finally identified what is needed. I'll be doing more trials later, focusing solely on scanning open ports and identifying vulnerabilities in them and trying to enter their device if possible.
