Our project is Aegis-SRE, an autonomous self-healing system for Kubernetes. think of it as an adaptive immune system for the cluster.
mainly the problem we are trying to solve here is that company like amazon runs multiple microservese on cluster
and these cluster
Kubernetes already has basic self-healing: if a container fails a liveness probe, it gets restarted. But that treats every failure the same, and containers actually fail for two very different reasons.

The first is operational: a memory leak, an OOM kill, CPU throttling. Restarting or scaling is the right fix there. The second is a security attack, for example an attacker getting a reverse shell inside a container. Restarting is the wrong response, because the attacker can simply get back into the fresh pod, and we've destroyed the RAM and socket state that forensics would need.

So Aegis first asks one question: is this a bug or an attack?

Here's how it works. Prometheus and Loki collect metrics and logs, and Falco watches the Linux kernel for suspicious activity. An AI model, backed by a knowledge base of SRE runbooks and security notes, diagnoses the incident and suggests an action. If it's a bug, our Go controller restarts or scales the service. If it's an attack, we don't restart. The controller applies a Cilium network policy that cuts the pod off from the network, and the container stays alive so investigators can study what happened.

The next question is: what if the AI makes a mistake? That's why the AI only suggests, and fixed safety rules decide. Some actions, like deleting a namespace, are never allowed, no matter what the AI says. And if the AI isn't at least 70% sure, the case goes to a human engineer.
