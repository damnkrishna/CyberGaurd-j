# Active Reconnaissance

Collecting information about target web application through direct engagement with target or connection.

**Tools used:** ping, traceroute, telnet, nc

## Web Browser

You can find a lot about a web application from its web browser and nowadays every company or startup have their web application.

- **Port 80** => used for website accessed over HTTP
- **Port 443** => used for website accessed over HTTPS

These two are the default ports that are used but it depends upon the developer on which port they want to host the website on.

### Extensions

- **Foxyproxy**: used for accessing the request response data using burp suite on target website
- **User-agent switcher manager**: to let user make a website think they are accessing the site from a different browser, device or operating system  
- **Wappalyzer**: tells insight about the technologies used by website

## Ping

Checks for connection or remote system if online.

- **Packet send, Packet received**: confirms the network is working between two systems
- **ICMP echo packet**

```bash
ping -c 5 <machine_ip>
```

Checks for packet loss, verify if connection is done properly or not.

## Traceroute

Tracks your packet while connecting and reveals info about number of hops required to reach target and IP of routers or hops and info about number of router between two systems.

**TTL (Time to Live)**: indicates the maximum number of hops that a packet can pass through before being dropped.

**How it works:**
TTL -> ttl=1 -> Reaches Router -> ttl-1 -> TTL=0 (packet will be dropped) => returns IP address where the packet is dropped

So this interface actually works in such a way that to reach certain machine we send several packets with different TTL value so it can reach different levels and return the IP of these routers or hops done to reach the target.

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/b2f6cec2-a2ac-458c-bf02-9e8306abc792" />

## Telnet

Network protocol that enables users to remotely access and control devices over a network.

```bash
telnet <machine_ip> <port>
```

**Commands:**
- Send/enter => `GET / HTTP/1.1`
- `host: example`

**Note:** Press double ENTER to run this

## Netcat

Functions as a client that connects to a listening port.
- Supports both TCP and UDP

### Basic Syntax:
```bash
nc <machine_ip> <port>
```

**Commands:**
- `GET / HTTP/1.1` => SHIFT + ENTER
- `host: netcat`

### When you want to open a port and listen to it:
```bash
nc -vlnp <port>
```
or
```bash
nc -v -l -n -p <port>
```
(order doesn't matter)

### Key Notes for Netcat:
- `-p` should appear just before port number you want to listen on
- `-n` avoid DNS lookups and warnings  
- Port number less than 1024 requires root privilege to listen on

### Common Issues

There can be several reasons behind not being able to listen to specific port like:
- Port closed (will be unable to connect)
- Require root access for port below 1024
- Wrong IP or machine address entered
- Stopped by certain firewall



