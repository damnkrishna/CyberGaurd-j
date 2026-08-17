# Journal Entry — August 17, 2026

## Personal Reflections

Yesterday wasn't exactly wasted — I spent it with mom, chilling and relaxing. We thought my cousins would be visiting today, but that plan fell through. They're not coming anymore, and honestly, I'm still a bit confused about what to do with myself now.

To add to that, this HR call has been messing with my head lately. I'm finding it hard to decide on things right now.

## Today's Plan

I'm heading to IIT Delhi today with a friend — he has a meeting with a professor there, and since I'm free, I figured why not tag along and check the place out.

That said, I've been off my studies for 7+ days now, and it's time to get back into it. I'm finally starting to plan things out again — looking into what I should actually be doing instead of wasting time chilling on the sofa or rotting in my room.

## The Career Decision

Leaving a 27 LPA offer for what I actually want to chase has given me a strong sense of direction. It's reinforced how important it is to keep moving toward what I really want — because for it, I'm walking away from everything else being offered to me.

I know it sounds like leaving the biggest opportunity at the gate for the one I actually want. It might seem like a dumb decision to some, but I've made my choice. I know I can survive as a security engineer — but not as a software development engineer, not for sure. So I'm going to keep pushing.

## Restarting the Pentesting Journey

I'm restarting my journey as a pentester:

- Reading *The Web Application Hacker's Handbook*
- Practicing on PortSwigger labs
- Getting hands-on with fuzzing and automated online tools

My next goal is to become good enough at this to start earning on the side as a bug bounty hunter. I'm making it happen now.

## The Technical Journey So Far

It's been a wild path:

1. Started with **Docker**
2. Moved to **Kubernetes**
3. Got fascinated by how a single machine can be simulated and run across multiple platforms simultaneously, with minimal resources — controlling a pod that self-heals, repairing itself the moment it dies by spinning up a replacement

Who even thought of building something like that? But we're in the age of AI now, where anything feels possible.

And it didn't stop there — K8s, which already used relatively modest resources, got an even lighter alternative: **K3s**. This constant push toward improvement and new technology is genuinely what's inspiring me right now — I can't stop thinking about it.

### Why K3s Stands Out

- Doesn't need close to 1GB of RAM to run
- Around 500MB storage and 500MB RAM is enough
- Uses lightweight components throughout
- Uses **SQLite** by default
- Uses **Kine**, which translates directly between these tools without requiring a heavy connection layer — it can run without a heavy load on servers

## Project Vision: A Better Self-Healing Kubernetes Engine

This is what I'm building next — a Kubernetes self-healing engine from scratch, designed to be more reliable than the standard approach.

Instead of just replacing a pod after it dies, the engine will:

- Identify the *real* root cause behind the failure
- Attempt to fix the issue **before** the pod actually dies
- Diagnose the underlying reason for the failure
- Run the necessary commands itself to resolve the issue

---

### Today's Docker Goal

Run specific Docker commands and build out the pod for the main project — the one that's currently leaking memory and throwing RAM-related issues — as a step toward this larger self-healing system.
