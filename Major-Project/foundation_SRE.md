# Aegis-SRE Learning Notes — Day 1

## Learning Approach

There are two ways to go about this: first learning everything and then building the project, or learning while building and testing if it works. I'm going to go with the second way — learn while building. That approach seems better.

But even for that, we should have some foundational knowledge, which is what I'm starting with today.

## 0.1 Foundation of Linux

This will be used for understanding how Docker works and how Linux finds what system is running and what process it is going to run — and what exactly runs in the background when we start or run something in Linux, step by step. We only know that when we type something, it "runs," but in assembly language and deep inside, a lot of things are actually working whenever you ask code to run. That is what we call **syscalls** — the calls that any operating system makes to run a certain process or execute a certain command. Today I'm going deep into this, understanding specific syscalls in Linux and what happens behind the scenes of any command running.

### Syscalls

There are around 300 syscalls in Linux, but only a few of them are the most important, and our project will most likely be using these specific ones:

- **execve** → running a program and replacing the old process with the new one
- **openat / open** → opens a file and returns its file descriptor
- **socket** → opens a new endpoint for network communication
- **clone / fork** → creates a new child process

### Falco & eBPF — Where This Connects to the Project

It seems like my major project is also connected to the Linux operating system, as the self-healing SRE we'll be building will use Falco to understand specific things running in the background — what exactly they are and how they control Docker — which will help us control our self-healing project.

Falco doesn't just see the main command; it observes the conversation happening between the kernel and the user — all the commands we're requesting the kernel of the operating system to execute.

This is where Falco sits for our project: **eBPF** is what it uses. Falco sits between the user requesting a command and the kernel processing it. Falco reads that command and inspects it before the kernel processes it.

### How This Powers the Self-Healing Project

This is where the main work of the project will happen. Whenever the site goes down, or an error causes something to stop, the command we send to fix it — after searching for the solution — will first be seen by Falco, which inspects it to check whether it's the right solution or not. Based on whether it's right, or whether the error is real or fake, we decide accordingly. This is where the magic of the project will happen, so I have to do this extremely well. The connection needs to be understood carefully and clearly. Also, the documentation of the project should be proper, so errors can be fixed without too much confusion.

## File Descriptors (FDs)

In Linux, there is a famous saying: "Everything is a file."
To the kernel, a text document, a keyboard, a USB drive, and an active internet connection are all treated the exact same way — as files.

When a process opens a file (via the `openat` syscall), the kernel gives the process a **File Descriptor** — a simple integer that acts as a ticket number for that open file.

Every process starts with three default FDs:

- **0 (Standard Input / stdin):** Where the program reads data from (usually your keyboard).
- **1 (Standard Output / stdout):** Where the program writes normal output (usually your screen).
- **2 (Standard Error / stderr):** Where the program writes error messages.

If a program opens a network connection, the kernel might assign it FD 3. If it opens a log file, it gets FD 4.

## Reflections After Practicing

I just tried running and watching the commands and processes that run in the background when we run something, and it was actually great to see. Now I understand what exactly the self-healing system we'll be building will do.

But this was for Linux — I think we'll be doing this on Docker or something, so I have to learn that next.

## Next Up: Docker

For my next task, I first have to learn how to use Docker and build a container — what access it has and how it works, plus the basic commands for it. Once I understand the basics, I'll build a pod that knowingly leaks data and RAM, so we can understand exactly how these things leak and what we have to do manually to fix it. After that, we'll be able to build a model that self-heals them itself, rather than needing manual intervention or an engineer. That's the idea of this project.

### Namespaces: The Illusion of Solitude (Limits what a process can SEE)

If you run a normal process on Linux, it can see everything — the whole hard drive, all the network interfaces, and every other running process.

A Namespace wraps a process in an invisible box and lies to it. It tells the process, "You are the only thing running on this computer."

There are several types of Namespaces, but here are the three most important for chaos engineering:

- **PID Namespace:** Isolates the process ID numbers. (This is the answer to my self-test — more on this below!)
- **NET Namespace:** Gives the process its own private network stack (its own IP address, routing tables, and firewall rules).
- **MNT Namespace:** Gives the process its own private filesystem tree. It thinks it has its own `/bin`, `/etc`, and `/usr`.

### cgroups: The Enforcer (Limits what a process can USE)

Namespaces stop a container from seeing other processes, but they don't stop a container from eating up all the server's RAM or burning 100% of the CPU.

That is what **cgroups** (Control Groups) do. They act as the accountant and the bouncer.

- **Memory cgroup:** "You only get 200MB of RAM. If you ask for 201MB, I will shoot you in the head." (This is exactly how I'll trigger an OOM (Out of Memory) Kill in the Chaos Pods!)
- **CPU cgroup:** "You are only allowed to use 10% of CPU core #2."

## Closing

That's it for the learning on Aegis-SRE for now. I'll try using Docker myself, run some commands on it, try to host something on it, and stuff like that.

---

## Extra (Claude's Addition)

Quick reference of what's covered today, so it's easy to jump back to at a glance:

| Concept | Role in Aegis-SRE |
|---|---|
| Syscalls (`execve`, `openat`, `socket`, `clone`/`fork`) | The actual kernel-level actions Falco will be watching |
| File Descriptors | How the kernel tracks anything a process has open (files, sockets, pipes) |
| eBPF / Falco | Sits between user and kernel — inspects commands before they execute |
| Namespaces | Controls what a container can *see* (PID, NET, MNT) |
| cgroups | Controls what a container can *use* (memory, CPU) — this is how you'll trigger your OOM chaos scenarios |

Suggested next checkpoint once you're into Docker basics: try triggering an actual OOM kill with a `--memory` limit on a container, then watch it with Falco to see what the syscall trail looks like right before the kill. That'll directly connect today's two halves (syscalls/Falco and namespaces/cgroups) into one working example.
