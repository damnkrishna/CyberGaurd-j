
# Day 7: Mastering the Wazuh Dashboard & Custom Filtering

Yo! Today was all about getting hands-on with the **Wazuh SIEM interface**. Reading the docs is one thing, but actually seeing the logs fly in is where the real fun starts[cite: 3]. Here’s a breakdown of what I did to set up custom filters and how I actually "attacked" my own lab to test them[cite: 3].

## The Goal
The mission for Day 7 was to navigate the **Kibana-based Wazuh Dashboard** and create a custom filter that only shows high-severity alerts (**Level 10 or higher**)[cite: 3].

## Step 1: Navigating the Dashboard
I headed over to the **Security events > Events** tab[cite: 3]. This is basically the "Matrix" view where every single log from my Windows agent (`DESKTOP-H1U0I0G`) shows up[cite: 3]. It's super noisy at first because Windows loves to log every tiny thing[cite: 3].

## Step 2: Creating the "Critical" Filter
To cut the noise, I used the **+ Add filter** tool[cite: 3]:
* **Field:** `rule.level`[cite: 3]
* **Operator:** `is between`[cite: 3]
* **Values:** `10` and `15`[cite: 3]
* **Label:** I named it "critical alert" so I don't have to remember the numbers next time[cite: 3].

Initially, my dashboard was totally empty. **"No results match your search criteria"**[cite: 3]. This was actually a good thing—it meant my Windows machine wasn't under active attack[cite: 3]! But I needed data to prove the filter worked[cite: 3].

## Step 3: Triggering "Level 10" Alerts
I had to play the "attacker" to generate some high-priority logs[cite: 3]. I tried a few things:
1.  **Clearing Security Logs:** I went into Windows Event Viewer and nuked the security logs[cite: 3]. Wazuh caught it immediately[cite: 3]! Interestingly, it showed up as **Rule 63103**, but in my lab, it was only a **Level 5**[cite: 3]. Not high enough for my filter[cite: 3]!
2.  **The Brute Force Attack:** This was the winner[cite: 3]. I went to the Windows login screen and spammed a bunch of wrong passwords[cite: 3].
    * Wazuh first logged these as individual **Rule 60122 (Level 5)** alerts.
    * Once I did enough of them, the manager realized it was a pattern and triggered the **"Multiple failed logins"** rule, which hits the **Level 10** threshold.

## Lessons Learned
* **Patience is Key:** Logs don't always appear instantly. Sometimes the agent and manager need a minute to sync up.
* **Watch the Filters:** I got stuck for a second because I had a `manager.name` filter active that was conflicting with my results. In a SOC, you have to be careful that your filters aren't *too* specific, or you'll miss the real threats.
* **Rule Levels Matter:** Not every "suspicious" thing is a Level 10
* . You have to understand how Wazuh ranks threats to build a good monitoring setup.

## Next Steps
Now that I've got the dashboard under control, I'm ready to look into **Active Response**—basically teaching Wazuh how to fight back automatically when it sees these Level 10s

---
