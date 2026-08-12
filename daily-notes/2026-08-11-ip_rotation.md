# IP Hopping / Proxy Chaining — Study Notes

So today we are going to study how we can hop our IP, or proxy chaining — how to hide or try to hide your IP.

I know no one can hide their IP completely, as anyone/everyone is traceable. What I want to learn is how to hide my IP from general, normal, non-hacker people — like hide the IP at least one layer below, so it's not visible at the front layer.

As I know, no one is completely anonymous, but I can still try to cover up as much as possible. Right?

So let's go.

**Plan:**
1. First, theory basics
2. Then a little deeper theory, then video watching to master it
3. Then hands-on practice

As I want to write a script or use a tool that can actually hop or hide my IP, and build it in such a way that every time I start my laptop or virtual machine, it itself starts changing my IP in the background — so that I don't have to keep worrying about that.

I know it will put unwanted pressure on my device, but at least on my command if it can start, that would be great. Don't you think?

So let's begin.

---

## Theory: The Primary Ways This Is Achieved

**Rotating Proxies**
Instead of connecting to a single proxy server, you connect to a proxy gateway. This gateway has access to a massive "pool" of IP addresses. Depending on how it's configured, the gateway will automatically route your traffic through a different IP address every few minutes, or every time you make a new request.

**Proxy Chaining**
This involves routing your traffic through a sequence of multiple proxy servers (e.g., Proxy A → Proxy B → Proxy C → Target). If you periodically swap out the proxies in your chain, your final IP address changes.

**The Tor Network (Onion Routing)**
Tor routes your traffic through three randomized volunteer nodes (Entry, Relay, and Exit). Your IP address appears as the IP of the Exit node. Tor automatically builds new "circuits" (paths through the network) every 10 minutes, effectively giving you a new IP address automatically.

---

## The Problem With Constant Hopping

You just discovered the exact reason why professionals rarely use Tor for persistent work.

That is the frustrating reality of automated IP hopping: when your IP suddenly changes from Germany to Romania in the middle of a task, the server you are talking to sees a completely different machine trying to hijack the session and drops your connection. On top of that, half the internet outright blocks Tor exit nodes because of malicious traffic, which means endless CAPTCHAs and broken services.

---

## My Reasoning So Far

So what you are saying is that instead of continuous hopping, people either:
- Set their IP to a specific, different IP for the duration of their work and manually change it using proxy chaining, or
- Just host a free-tier or cheap cloud service (laptop, OS, or Linux server) and send their whole traffic through it.

So whatever you do or search, the whole traffic goes through that specific cloud data center's IP rather than our own IP.

But I think — if I'm using a specific cloud service, then they must record who accessed it and from where. So if I do something fishy, they will get to know about it, definitely, sooner or later, and I will be caught.

I know no one is hidden always, and this will definitely buy some time, as getting access to user data is a complex process for anyone, and some people won't even be given that kind of data — but it is technically present online, and people will use it to get to the bottom of the issue. So it is technically not an answer.

The only technical and proper way I can think of is:
- Proxy chaining — finding certain IPs of people or places that are public, and using those IPs as the source of your outgoing traffic, since a public IP location might be tougher for them to trace.

But wait — what am I even saying? A public IP is temporary. At the end, the host or the tracker will somehow get access to that person's permanent address or MAC address, and they will get caught too. I'm a little confused how they do that.

But currently, the only valid way I can think of is using proxy chaining — hopping your known IP and changing it manually.

Because using Tor or other tools, they will keep hopping my IP and I won't be able to do anything. What I'm saying is: I'm doing work on something, and all of a sudden the IP changes, and maybe that new location doesn't have the info/session I need.

---

## Three Possible Approaches

### 1. Tor Node "Pinning" (The Best Legal Way)
You actually can use Tor without it constantly hopping. Tor hops by default, but it is highly customizable. You can edit the Tor configuration file (`torrc`) and define strict rules for your circuits.

You can tell Tor: "Only use this specific Exit Node IP address, and never change it until I restart the service."

**Result:** You get the untraceable, encrypted anonymity of the Tor network, but your final IP address remains perfectly static, so your session doesn't drop.

### 2. Bulletproof Hosting (The Gray Area)
Instead of using mainstream cloud providers, people buy servers from "bulletproof hosts." These are hosting companies located in jurisdictions that refuse to cooperate with international law enforcement (often in Eastern Europe or offshore islands).

**Result:** Paid for using untraceable cryptocurrency like Monero (XMR) over a VPN. This provides a fast, dedicated, non-hopping IP address with zero billing trail linking back to a real identity.

### 3. Compromised "Jump Boxes" (The Illegal Way)
Actual threat actors rarely pay for infrastructure. They scan the internet for vulnerable, unpatched servers (like a forgotten corporate web server or an IoT device). Once they break in, they install a proxy on that machine and route their traffic through it.

**Result:** They get a completely stable IP address. If investigators trace the traffic, it leads to the innocent company whose server was hijacked, not the attacker.

---

## Where I Landed

These are all the possible solutions I can find, and two of them are actually pretty illegal.

The only one — Tor node pinning — could be legitimate, but I don't know how good it really is. It too might have some loophole, since I'd be trusting Tor completely for something it might not even guarantee. I don't know what its internal process actually looks like.

So let's first go deep into that, then we'll talk further.
