# Pentesting Journey — Day Update

So here we go, actually — work has been a little crazy lately.

## SQL Injection Notes

Starting off as a pentester: for the SQL injection room on PortSwigger, I think I remember the exact syntax and where to put it to clear that specific room. Writing:

```
' OR 1=1--
```

This specific command will remove any further WHERE clause conditions, and since `1=1` is always true, it will easily return what I'm searching for without even asking the question twice. So yeah, I get it.

Other than that — if you know other ways to find out if a website is vulnerable to SQL injection, that would be great.

I've started watching the "Pentesting for Beginners" 14-hour YouTube video — I've watched 3 hours out of it. I've also photocopied the next 100 pages of the Web Application Hacker's Handbook, so first I'll complete that side by side, then think further. So let's go.

## Other SQL Injection Detection Methods (Reference)

Other ways to spot SQL injection besides the classic `OR 1=1` tautology:

- **Error-based detection**: Throw in a single quote `'` or a broken syntax character and see if the app throws a DB error (e.g. MySQL syntax error messages). That alone often confirms the input isn't sanitized.
- **Boolean-based blind**: Compare responses between a true condition (`' AND 1=1--`) and a false one (`' AND 1=2--`). If the page content/behavior differs, it's injectable even without visible errors.
- **Time-based blind**: When there's no visible difference in output, use something like `'; WAITFOR DELAY '0:0:5'--` (or `SLEEP(5)` for MySQL) and check if the response is delayed. Confirms injection when nothing else does.
- **UNION-based**: Once you confirm injectability, use `UNION SELECT` to pull data from other tables — this is the one PortSwigger leans on a lot for the "retrieve hidden data" labs.
- **Out-of-band (OAST)**: For cases where there's no visible or timing feedback at all, trigger a DNS/HTTP callback (Burp Collaborator is built for exactly this).

Since I'm already on PortSwigger, their SQL injection topic page walks through all five of these with labs for each — worth doing in order since blind/OOB techniques build on the error-based intuition I already have.

## Random Thoughts

While I've got some doubts... well, why the hell should I waste my whole day for others? I spent my whole day yesterday figuring out colleges for my cousin, visiting several colleges, and in the end I liked none of them. I ended up with a headache, body pain, and lack of sleep. But not today — I won't be doing these things today. I just want to study a little and work a little. I know this will go on for the next 2–3 days, but still, I can't spend my whole day on someone else. That's what I'm saying.

## Cousin's Admission & Job Security

Well, the thing is quite different, as for the last 2 days I have solely been spending my two whole days on my cousin's admission and everything. Cause I really don't know what to do now. I finally got their admission, but this bad feeling of "what will I be doing when I get the job, and if I didn't get the job then what will I do" is there.

Cause I really want job security. Though my dad is there to provide me job security, I have to be sure that I get the job — I don't give a shit what the work is about, I have to be an expert in the field. I have to get back on track. Well, it's not that tough, though — I've got to start my work again and not stop until it's completely done.

## Today's Task List

For task I am going to do today:

- Read ethical hacking book, at least 10 pages
- Try one PortSwigger room
- Watch one TCM video for 30 min minimum

And before I do all this, first I have to submit all college assignments for MOOC — first I'll do that.

## Yesterday's Recap

Well, yesterday went great — I was able to sit from morning 8 am to evening 5 pm and completed almost all the work I had to do, and it was good. Also, we finished what we had to and what I wanted to do, except reading the book — and that too I tried, but sometimes it happens, I am unable to understand a thing, and that happened. I tried reading one research paper, understood that. Next tried to read the book, but was unable to read it — so what can I do, it's fine.

So for my goal of today: I'm gonna do pentest today, read 20 pages of the book, then try the PortSwigger room of the topic — try the PortSwigger room and try to clear that room on my own — and then watch a TCM video on the basics of pentest for 30 min.

That's what I will do today.
