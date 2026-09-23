Good morning ma'am. Our project, Aegis-SRE, is an autonomous self-healing site reliability system for Kubernetes environments.

The problem we're solving is this: many companies, like Spotify and Airbnb, run their platforms as multiple microservices and rely on Kubernetes' liveness probe to keep downtime to a minimum. But the liveness probe has just one response to any pod failure — restart it.

This works fine for a lot of operational bugs. But they forget that the reason behind a pod failure can also be a security intrusion or attack, and restarting the pod doesn't fix that. It just restarts the pod with the same flaw still there, and worse, it deletes the evidence of the attack.

So Aegis-SRE brings a solution: instead of directly taking action, we first analyze the root cause behind the pod failure using our AI engine, and classify it as either an operational bug or a security attack.

If it's an operational bug, we simply restart or rescale the pod. But if it's a security attack, we isolate that pod, freeze its state, and stop all incoming and outgoing traffic — preserving the digital evidence, so a human or AI can fully analyze and fix the issue afterward.



this is the final viva intro i am going to give for this project
