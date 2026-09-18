# CVE-2025-32433 — Erlang/OTP SSH (Pre-auth RCE, CVSS 10.0)

## Backstory

So, listen — the assignment finally arrived for an R&D cybersecurity job and internship opening, and it was shared with only 7 students out of my entire college. I think I might have a shot here.

I know I have the knowledge and hands-on experience to build this at the very best level, and I'm deciding everything step by step with a proper write-up and documentation so it can be explainable to anyone out there. I am capable of building this lab — I just need to plan each step properly and implement it in such a way that there is minimum chance of mistakes.

I'll be using Antigravity to help build the lab. But before that, I have to decide which CVE I'll take for this assignment — because I know everyone who got this assignment will be asking ChatGPT/Claude the same question to help them build it and write it up. So I've decided carefully, keeping the conditions in mind — picking one that is actually reproducible and that I can actually build.

So let's first do some recon on possible CVEs and their fixes.

So, I've decided which CVE I'm going with:

## The Technical Root Cause

The SSH protocol has a strict order of operations: you connect → negotiate encryption → authenticate → only then can you open a "channel" (a session) and run commands. This is defined in RFC 4254. Message types numbered 80 and above are supposed to be post-authentication only — the server is required to reject them if they arrive before login succeeds.

The bug is that Erlang/OTP's SSH server fails to properly reject `SSH_MSG_CHANNEL_OPEN` and `SSH_MSG_CHANNEL_REQUEST` messages when they're sent before authentication is complete. Because of a missing check, the server mistakenly processes these messages as if the user were already verified — an attacker sends a "channel open" message, follows it with a "channel request" containing a shell command, and the server executes it as if it came from a logged-in user.

So it's not a memory corruption bug, not a buffer overflow — it's a missing state check. The server's internal state machine simply forgot to ask "wait, has this connection actually authenticated yet?" before honoring a request that should only be valid post-login. If the SSH daemon runs as root — common in embedded/test/IoT setups — this gives full remote code execution with zero credentials.

### The "Stupid Layman" Example

Imagine a bank. To open a safety deposit box, you're supposed to: (1) walk in, (2) show ID at the counter, (3) get verified, (4) then the guard lets you into the vault room, (5) then you can open your box.

This vulnerability is like a bank where you can walk straight up to the vault door and say "I'd like to open box #47 and take the contents" — and the vault door swings open, no ID check happened, nobody asked who you are. The guard's job was to say "hold on, you haven't shown me your ID yet" before letting that request through — but that check simply isn't there. A threat actor could compromise the target system simply by initiating a connection and sending malicious data, even before authentication completes — effectively becoming an unauthorized system admin.

### The "Explain to an Executive" Version

"Our SSH login process has a logic gap — the server accepts and runs certain commands before it has actually confirmed who's connecting. That means anyone on the network, with zero credentials and zero passwords, can potentially run arbitrary commands on the server — and if that server process runs with admin/root privileges, they get full control of the machine. This isn't a 'stolen password' problem, it's a 'the lock doesn't actually check the key' problem. Patching means upgrading the software; the fix closes that specific processing gap."

This flaw lets an attacker break out of the key-exchange state machine and open an arbitrary channel before credentials are verified — over nothing more than a standard TCP connection to port 22.

### In Tech Terms

When a computer connects to an SSH server, they are supposed to have a strict "conversation" where they prove who they are before they can ask the server to open up a command channel. Because of this flaw, a total stranger can send a "channel open" message out of order, right at the very beginning of the conversation. The Erlang server gets confused, accepts the message anyway, and lets the attacker run commands on the system without needing a username or password. Because it gives outsiders full control over the computer without needing to log in, it received the maximum severity rating of 10 out of 10.

### My Own Analogy

It's like those hidden, on-purpose-hidden web page dashboards that are only shown to users who have admin access — normal people who have no idea this hidden page exists can never open it. But if someone knows the specific page exists, and can enter it just by giving the correct phrase or path, they'll be able to get in — because there was no check on the system for whether it was a valid or invalid user. It never went through the normal steps; it went straight to the final result, the admin dashboard. That used to be a very common vulnerability in earlier websites.

Obviously this is different from a web vulnerability, since it's an SSH protocol issue — it gives the attacker complete access to the system, not just the dashboard of a website. But I felt it was identical in spirit to the web server vulnerability that's usually found.

## The Fix

The fix was implemented by adding a strict state check in the SSH message-handling logic to immediately reject out-of-order commands before authentication completes.

### How SSH Protocols Normally Work

In network protocols like SSH, every message has an assigned ID number defined by internet standards like [RFC 4254](https://www.rfc-editor.org/rfc/rfc4254):

- IDs below 80: messages used for setting up encryption, key exchanges, and verifying user identity (logging in).
- IDs 80 and above: messages for opening terminal channels and running terminal commands (such as `SSH_MSG_CHANNEL_OPEN` at 90 and `SSH_MSG_CHANNEL_REQUEST` at 98).

These higher-numbered messages should strictly only be allowed after a user is completely authenticated.

### What Was Broken

Erlang's SSH server works as a state machine (moving from Connecting → Handshaking → Authenticating → Connected/LoggedIn).

The message router was missing a guard rule for connection messages. If an incoming packet had a message ID ≥ 80, the server passed it directly to the channel subsystem to execute, entirely ignoring whether the connection was still in the Authenticating phase.

### How the Developers Fixed It

In the patched versions ([GitHub Advisory GHSA-37cp-fgq5-7wc2](https://github.com/erlang/otp/security/advisories/GHSA-37cp-fgq5-7wc2)):

- **State verification guard**: the developers added explicit pattern-matching checks to the handler. When an SSH connection message arrives, the server explicitly inspects the connection status:
  - If status = authenticated → process the command as usual.
  - If status ≠ authenticated → reject the packet and disconnect the client immediately.
- **Message ID filtering**: the pre-authentication listener now drops or returns an SSH protocol error for any high-numbered packet (codes ≥ 80) sent during the handshake.

By enforcing this gatekeeper check at the packet-parsing layer, an attacker can no longer jump straight to the "open channel" phase.

<img width="959" height="412" alt="image" src="https://github.com/user-attachments/assets/68273139-6916-426b-8e0e-f76d772b9451" />

### References

1. [https://github.com/0xBlackash/CVE-2025-32433](https://github.com/0xBlackash/CVE-2025-32433)
2. [https://www.keysight.com/blogs/en/tech/nwvs/2025/05/23/cve-2025-32433-erlang-otp-ssh-server-rce](https://www.keysight.com/blogs/en/tech/nwvs/2025/05/23/cve-2025-32433-erlang-otp-ssh-server-rce)
3. [https://unit42.paloaltonetworks.com/erlang-otp-cve-2025-32433/](https://unit42.paloaltonetworks.com/erlang-otp-cve-2025-32433/)
4. [https://www.youtube.com/watch?v=19X1TFUE5TY&t=662](https://www.youtube.com/watch?v=19X1TFUE5TY&t=662)
5. [https://www.keysight.com/blogs/en/tech/nwvs/2025/05/23/cve-2025-32433-erlang-otp-ssh-server-rce](https://www.keysight.com/blogs/en/tech/nwvs/2025/05/23/cve-2025-32433-erlang-otp-ssh-server-rce)
6. [https://www.picussecurity.com/resource/blog/cve-2025-32433-erlang-otp-ssh-remote-code-execution-vulnerability-explained](https://www.picussecurity.com/resource/blog/cve-2025-32433-erlang-otp-ssh-remote-code-execution-vulnerability-explained)
7. [https://socura.co.uk/threat-alerts/cve-2025-32433-critical-erlang-otp-ssh-vulnerability](https://socura.co.uk/threat-alerts/cve-2025-32433-critical-erlang-otp-ssh-vulnerability)

## The People, the Story, and the Disclosure

**Who found it**: Four researchers from Ruhr University Bochum in Germany — Fabian Bäumer, Marcus Brinkmann, Marcel Maehren, and Jörg Schwenk. This isn't their first SSH-related find either — the same core team (Bäumer, Brinkmann, Schwenk) previously discovered the Terrapin Attack (CVE-2023-48795), a cryptographic downgrade attack against SSH implementations including OpenSSH. So this group specifically does deep protocol-level research on SSH implementations — they weren't randomly fuzzing, they're SSH specialists who go implementation by implementation looking for places where the protocol spec isn't actually enforced correctly.

**What they were likely doing**: Their pattern of research (visible from the Terrapin work and this one) is auditing how different SSH server implementations enforce the ordering rules of the protocol state machine — i.e., "does this implementation actually reject message X if it arrives before authentication, like RFC 4254 says it must?" Erlang/OTP ships its own from-scratch SSH implementation (not OpenSSH-based), which made it a natural target — independent implementations of a protocol spec are exactly where these state-machine enforcement bugs tend to hide, because every implementer has to correctly re-derive "which messages are allowed when" on their own.

### The Disclosure Timeline

- **April 16, 2025** — the researchers disclosed the flaw to the Openwall oss-security mailing list, and an official advisory was published simultaneously on Erlang/OTP's GitHub. The bug was responsibly disclosed by researchers at Ruhr University Bochum and patched within 48 hours of being reported to the maintainers.
- Fixed versions released the same day: OTP-27.3.3, OTP-26.2.5.11, OTP-25.3.2.20.
- Within a day of public disclosure, Horizon3.ai's attack team reproduced the exploit and called it "surprisingly easy," demonstrating a PoC that writes a file as root on affected systems — no memory corruption, no fuzzing needed, just correctly sequenced protocol messages.
- **June 9, 2025** — CISA added it to the Known Exploited Vulnerabilities (KEV) catalog, confirming it was being exploited in the wild, not just theoretical.

### How It Was Actually Fixed — The Real Diff

I found the actual code change (in `ssh_connection.erl`, the module that handles incoming SSH connection-protocol messages). Here's what changed, in essence:

Before the fix, the message-handling function only had a specific pattern-match for `#ssh_msg_disconnect` — any other message type that arrived, at any stage of the connection, fell through to normal processing logic. There was no clause anywhere in that function saying "wait — has this session actually finished authenticating yet?"

The fix added a new clause that runs before any other message gets processed: something like "if the message is anything other than a disconnect, AND this session's authenticated flag is still false, AND we're acting as the server → don't process it, log it, and terminate the connection." In effect, they inserted the missing guard clause: an explicit checkpoint that says "stop — check credentials before doing anything else with this message," which is precisely the check RFC 4254 always required but the implementation never actually coded in.

**Layman version of the fix**: imagine the vault-door example from before. The fix isn't "install a smarter lock" or "rewrite the whole vault system" — it's literally adding one guard standing at the door whose only job is "check ID first, everything else waits." A one-clause addition that intercepts every request and asks the one question that was never being asked. That's why the patch shipped in 48 hours — once you know the specific gap, the fix is small and surgical, not a redesign.

For my detection section, the natural angle given the root cause: a detection script can open a raw TCP connection to port 22, complete the SSH version exchange and key exchange, then send a channel-open request without ever sending a successful auth response — and check whether the server accepts it (vulnerable) or terminates the connection (patched). That's a legitimate low-risk protocol probe (it demonstrates the state-machine gap exists without necessarily executing an actual command), and it maps cleanly to what an Nmap NSE script or a Zeek/Suricata signature watching for "channel-open before auth-success" in a session would flag behaviorally.

## CVE Research Checklist

| Field | Detail |
|---|---|
| CVE ID | CVE-2025-32433 |
| Affected product | Erlang/OTP `ssh` application (built-in SSH server) |
| Affected versions | OTP-27.0-rc1 to < OTP-27.3.3; OTP-26.0-rc1 to < OTP-26.2.5.11; all versions < OTP-25.3.2.20 |
| Fixed versions | OTP-27.3.3, OTP-26.2.5.11, OTP-25.3.2.20 |
| CVSS v3.1 | 10.0 Critical — `AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H` (network, low complexity, no privileges, no user interaction, scope changed, full C/I/A impact) |
| CWE | CWE-306: Missing Authentication for Critical Function |
| Attack prerequisites | Network access to the SSH port (commonly 22) of a vulnerable, exposed Erlang SSH daemon. No credentials, no user interaction. |
| Attack surface | Any product embedding Erlang/OTP's SSH server — RabbitMQ, CouchDB, ejabberd, embedded/IoT/OT gear (e.g. the Nerves project), telecom infra. Widely deployed at companies like Ericsson, Cisco, WhatsApp per the underlying tech's usage. |
| Impact | Commands run with the SSH daemon's privileges — often root in embedded/lab setups → full remote compromise |
| Exploited in the wild | Yes — CISA KEV, added June 9, 2025 |
| Primary advisory | GitHub Security Advisory GHSA-37cp-fgq5-7wc2 (erlang/otp repo) |
| Disclosure channel | Openwall oss-security mailing list, April 16, 2025 |
| Fix commits | `0fcd9c5` (OTP-25.3.2.20), `b1924d3` (OTP-26.2.5.11), `6eef041` (OTP-27.3.3) — all in erlang/otp on GitHub |
| Related research | Same research group's earlier Terrapin Attack (CVE-2023-48795) on SSH — worth noting as context on the researchers' track record |

## Closing

Well, let's begin the beginning — this is everything about the info for the project. Now I've started building the lab from scratch.

So there has been some issue while building the labs. Actually, AI agents can't help with the exploit and payload process — that part I have to do myself to get the detection or proof of compromise myself. And also, how to fix this.

Other than that, I am right now working on bringing back the compromised version of the service, and automating the process of at least opening both the client and the attacker device and opening their secure shell, and first trying to do normal access. Then trying to do the compromise myself, and trying to automate the log-finding thing. And then working further, because I have to build this lab at any cost — even if it means I have to do the script writing and full configuration myself.

## What you personally must build: one exploit/reproduction script

**Functionally, here's what it needs to do:**

1. **Open a raw TCP connection** to your target container on port 22.
2. **Complete the SSH version-string exchange** — both sides announce their SSH protocol version (e.g. `SSH-2.0-...`) as plain text lines. This part is *not* the vulnerability, it's just normal protocol setup that has to happen before anything else can.
3. **Complete SSH_MSG_KEXINIT and key exchange** — the client and server negotiate encryption/MAC algorithms and establish an encrypted, integrity-protected channel. Again, normal and required — the SSH connection has to be "up" (encrypted) before you get anywhere near the bug. This is the part where using a library like `paramiko` or `asyncssh` will save you from hand-rolling crypto — you generally want the library to handle the transport layer for you.
4. **Stop before completing authentication** — this is the crux. Normally at this point you'd send `SSH_MSG_USERAUTH_REQUEST` and wait for `SSH_MSG_USERAUTH_SUCCESS`. Your script deliberately does **not** get that success response.
5. **Send SSH_MSG_CHANNEL_OPEN anyway** (channel type `"session"`) — this message is only supposed to be legal post-auth. Your script sends it while the session is still unauthenticated, and observes whether the vulnerable server accepts it.
6. **Send SSH_MSG_CHANNEL_REQUEST with type `"exec"`** carrying a command string, on that same channel — again, something that should require an authenticated session.
7. **Read back the response** — on the vulnerable target, this should return command output through the channel, proving you ran something with zero credentials. On the patched target, the connection should be forcibly terminated at step 5 or 6.

**Success criteria for your own testing:** on the vulnerable container, a benign command like `id` or `whoami` returns actual output over the unauthenticated channel. On the patched container, the same sequence gets a disconnect. That comparison *is* your evidence for the "Successful reproduction" and "Verify remediation" deliverables.

## What to study before you write it (this is the "research" part of the assignment, and it's meant to be yours)

- **RFC 4254** (SSH Connection Protocol) — defines exactly what CHANNEL_OPEN/CHANNEL_REQUEST look like on the wire and confirms they're meant to be post-auth only.
- **The official advisory**: `github.com/erlang/otp/security/advisories/GHSA-37cp-fgq5-7wc2` — has the maintainers' own description of the flaw.
- **Public PoC writeups to read (not copy) for technique**: there's a detailed one at `platformsecurity.com/blog/CVE-2025-32433-poc`, and a public repo at `github.com/ProDefense/CVE-2025-32433` — read how they structure the connection sequence, understand *why* each message is placed where it is, then write your own implementation with your own variable names, your own comments, your own error handling.
- **Whichever SSH client library you pick** (`paramiko` and `asyncssh` are the two realistic choices in Python) — read its docs on the transport layer specifically, since you'll likely need to hook into it at a lower level than the "just log in normally" API, since the whole point is deliberately *not* completing the normal login flow.

## What you do NOT have to build yourself

The vulnerable server, the fix, Docker/compose, the detection script, README, blog, logging setup — all of that is legitimately automatable and I (or Antigravity) can help fully. The one deliverable that's yours alone is this single client-side script.

---

Well, I guess it's not that easy as it looks. It sure sounds easy in mind till now, but doing this — building a Docker with an old Erlang/OTP version, trying to figure out how to write the exploit for it, then seeing where the logs are being stored for the detection thing, then updating to the fixed version and showing whether this still works or not — well, I am still repeating the first thing till now: building the lab with the vulnerable version of Erlang/OTP.

As for now — one of the videos said there are two ways possible for detection. One is network-based, as in you might not find something in the SSH log, but you can detect or check for any unusual network traffic, or access with/without authentication, or an exec command or something like that being run. Or you can have host-based detection by observing if a new file is created, or some file is modified, or other abnormalities like that.

Also, you wrote a script to detect whether it is vulnerable or not. What exactly — how are you doing the detection? Are you just checking the code for the detection part, or what is happening here? Can you explain it to me?

And also, as I just saw — when we even run the payload, it will create a file or run something, but it won't show us anything. We just know it wrote or ran something because we sent the payload — but until we have access to the device or SSH, how are we supposed to see if it worked or not? So we have to think of that aspect as well.

So I have got the payload — just have to modify it for the specific needs of my lab. And then have to try this out for the system and the devices and labs, to see if it is working properly or not. And also I have to explain each and every thing, why this specific script will run — as we already know that this all happened because there was no authentication check on whether the user can send more than 80 requests, and the user can jump directly to the message that authentication is done when the authentication was still under process. And as there was no authentication or anything, the system just assumes it has access and runs the command and lets the user have access to it.

This allowed a remote, unauthenticated attacker to:
- Open a TCP connection to the SSH server.
- Send a valid SSH_MSG_KEXINIT,
- then: skip authentication completely,
- and: send a channel_request with exec and payload.

So the last thing left is to run the payload and get the access, then test whether the system is able to detect it or not, and see whether the lab is ready and built or not.
