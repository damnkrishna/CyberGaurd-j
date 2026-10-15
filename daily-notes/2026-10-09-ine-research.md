# INE Internship Prep Notes

## 1. Where I Stand

Well, as you know, I got selected for the INE internship, and if God wills, I will join them as a full-time Cybersecurity R&D (fully remote).

My joining date is in the last week of October, so I have time. I want to use this time to properly research:

- The INE company and its website
- Every single piece of work they have done to date, and the meetings they attend
- Partnerships they have made
- Their top projects
- Their top certifications and top courses for industry experts

I am going to research all of it.

---

## 2. New Update: Competition for the PPO

A new update has occurred: a new guy has just been selected for the same role as me (INE intern, Cybersecurity R&D). Till now I was standing alone, but now I know there will be someone I have to compete with for the PPO. That is how it works in every company.

All my friends at top companies are in the same situation. They learn and grow together, and they are also each other's rivals for the PPO position.

Well, let's see how it goes. There is a whole 1 year of internship ahead of me first.

- Let's handle one day at a time, because that is what matters right now.
- I will focus on growing myself and not worry about my competition.
- I will try to learn new things and be better than I was yesterday.

---

## 3. Research Status

I was able to complete the other part of my dad's task, but I did not get time for the research part. I will do it today, after finishing the technical prep for the exam.

---

## 4. INE Company (Internetwork Expert)

### 4.1 Overall Direction

INE is progressing very strategically. It acquires companies that help it grow both name-wise and product-wise, and it keeps targeting bigger areas:

- It started from core cybersecurity (eJPT and other certs).
- It is now shifting more toward AI security, identity, and other areas, as it is being acquired by ISMG.

The company is nice. Now I need to get into its products and services, find out what its best services are, and find out which companies it provides services to. I know it is a private-equity-owned company, so these things might not be released publicly, but let's find what we can.

### 4.2 What INE Got from Its Own Acquisitions

| Year | Acquisition | What INE Gained |
|------|-------------|-----------------|
| 2019 | **eLearnSecurity** | A ready-made cybersecurity training business with its certifications and students, so INE didn't have to build one from scratch. |
| 2021 | **Pentester Academy** | Mostly labs and videos: 2,200+ labs and 1,500+ videos, plus a founder with a strong reputation in security training. |
| 2022 | **CloudSkills.io** | Cloud training content. |

### 4.3 ISMG Acquisition and Expansion

As ISMG is acquiring INE, these are the fields INE will expand into. The press release talks about expanding into **identity, AI and OT security**.

- Most of the tasks they allocate to me will probably be around these areas.
- HR even told me to keep an eye on these fields, as ISMG is acquiring them.
- AI lab content will likely increase, as the area is expanding for the company.
- Meetings and summits: there is a possible increase, but I am not sure whether they will send an intern. They might send full-time employees.

---

## 5. Lead R&D at INE: Ashish Bhangale

### 5.1 Read His Bios in Order (1 hour)

- [ ] InfoconDB presenter page for Ashish Bhangale (`infocondb.org/presenter/ashish-bhangale`)
- [ ] Black Hat Asia 2017 presenter page (earliest bio: 4+ years of experience, Python tool automation, source code review)
- [ ] Black Hat Asia 2020 speaker page (latest bio I found: 7+ years, WiFi and AD interest)
- [ ] Write down how his described focus changed from 2017 to 2020

### 5.2 Study His Talks

- [ ] DEF CON China 1.0 (2019), "VoIPShark: Open Source VoIP Analysis Platform" (co-presented with Nishant Sharma and Jeswin Mathai). Find the slides, video, or tool repo.
- [ ] Black Hat Asia 2017: find the session title and abstract from the official schedule
- [ ] Black Hat Asia 2020: find the session title and abstract from the official schedule
- [ ] Look for his Wireless Village, IoT Village, and DEF CON Demo Labs appearances (his bio mentions them)
- [ ] For each talk, write 3 lines: the problem, the approach, and what I would ask him

### 5.3 Review His Projects

For each project: read the description, find the source or download, note the vulnerabilities it teaches, and try it in an isolated VM if available.

- [ ] Command Injection and Arbitrary File Upload Vulnerable Web Application OS (his 2017 bio says it is on SourceForge)
- [ ] Vulnerable Router Project
- [ ] Damn Vulnerable WordPress
- [ ] Other vulnerable web application OSes in his bio
- [ ] **Chigula** (WiFi forensics framework): read what I can find; he is credited with developing and testing it
- [ ] **Chellam** (described as the first pure WiFi firewall): same as above
- [ ] **VoIPShark** (open-source VoIP analysis platform)

### 5.4 Understand His Lab and Content Context

- [ ] Look at Pentester Academy and Attack-Defense lab styles: how labs are structured, and what the objectives and hints look like
- [ ] Pick 2 INE or Skill Dive labs and note what makes them good or weak (clear goal, realistic target, reliable environment, hints)
- [ ] Note common complaints from reviews, like lab connection timeouts, so I can think about reliability

### 5.5 Skills to Brush Up (His Areas)

- [ ] Web application vulnerabilities: command injection, file upload, WordPress issues
- [ ] Linux and networking basics, VM setup, and snapshots
- [ ] Python scripting for automation and tooling
- [ ] WiFi security basics (WPA, monitoring, deauthentication concepts) and basic packet analysis in Wireshark
- [ ] Active Directory fundamentals (his stated interest)
- [ ] Digital forensics basics: evidence handling, and log or packet analysis

### 5.6 His Published Code

His code is published under the Pentester Academy organization, and these repos credit him:

| Repo | Link | Details |
|------|------|---------|
| **VoIPShark** | `github.com/pentesteracademy/voipshark` | Lists Nishant Sharma, Ashish Bhangale, and Jeswin Mathai as authors, under Vivek Ramachandran's guidance. |
| **Vulnerable OS Collection** | `github.com/pentesteracademy/vulnoscollection` | Four Ubuntu-based OSes with real-world vulnerable web apps (command injection, arbitrary file upload, XSS, SQL injection). He is credited as author. |
| **Airodump Scan Visualizer** | `github.com/pentesteracademy/airodump-scan-visualizer` | A tool that presents Airodump-ng WiFi scan results in a searchable, sortable, visual form. Credited to him and Vivek Ramachandran. |

**Online presence:**

- His handle in those READMEs is `@Hax0rGuy`, and his Medium page links to LinkedIn and Twitter accounts under that name.
- His Medium profile is `medium.com/@ashish771`. It has Pentester Academy "Premium Lab" write-ups from 2020 and 2021 on Navigate CMS remote code execution, OpenNetAdmin command injection, and ElasticSearch script execution.
- I would search GitHub for "Hax0rGuy" to check for a personal account, but I haven't confirmed that one exists.

This is all I could find about my boss. He is quite something. Crazy, actually.

---

## 6. Reflection: Certs vs. Real Depth

Well, this is going to be tough.

I talked with Claude, and it kind of opened my eyes: doing certs without serious lab work might backfire. I might end up with a lot of certs but without the depth needed.

All my seniors, like Ashish sir and Nishant sir, became famous because of their work in lab development and R&D, not because they have a lot of certs. I know I can't be like him from the start. He has 13 years of experience in the field, and he is probably very passion-driven. Where they stand at the moment is crazy-level work and expertise in the security field. I can see that they are driven by something bigger than themselves, and both of them have done so well and built their names in the security field.

And here I am, 1 year into security, thinking about making a jump bigger than theirs by learning from them, and side by side getting certs and chasing money. Security is not about chasing money. It is about chasing a name for yourself and building a name of your own.

A mentor like Ashish sir can take me to another level, so I will stick close to him. He has my utmost respect. He built his own name from nothing by focusing on what he likes and building so many things from scratch. He is crazy.

---

## 7. INE Certifications

### 7.1 My Question

There are a total of 15 certs that INE has. If I want to get all of them, will I just be collecting certs, or will I gain deep expertise as well? Or will this be a waste of time?

I am not saying I will do only this. I will work my very best as a Cybersecurity R&D and lab content creator at INE. But in my free time, should I prep for these certs rather than learning, building new projects, or gaining deep expertise in R&D?

If I want to get all 15 certs, I need to find out:

- [ ] How tough they can be
- [ ] How many paths these 15 certs have (some must be SOC, some pentester, some AI and cloud security)
- [ ] How tough each cert is
- [ ] How much time it will take to prep using INE's own learning material

### 7.2 Certs I'd Target from INE

I'd skip **eJPT**, **eSOC**, and **eEDA**. They're below my current level, so they'd cost time without proving much.

| When | Cert | Why |
|------|------|-----|
| Months 3–5 | **eAIS** | The job lists AI/LLM security. It's a novice-level exam, so it's quick, and it's an area INE is investing in. |
| Months 7–11 | **eWPT** | Web and API work is core to the role. |
| Full-time, year 1 | **eCPPT** | Active Directory is 30% of it and my biggest offensive gap. I already know how to detect AD attacks. |
| Full-time, year 1 | **eCTHP** | A natural fit for my strengths, so a quick win. |
| Full-time, year 2 | **eIAMA** or **eWPTX** | eIAMA if identity work comes my way, since the job lists identity and authentication and ISMG named identity as a push. eWPTX if web is my lane. |



well gotta do a lot of work and learn in such a way to understand the stuff rather than just use ai to build it as my mentor has asked me to understand the whole process in to out rather than just understanding ai and building labs
so will do that as he stated to me

so the offer letter finally landed with 35k stipend and remote.com access and verification from ine as well
So it is done with the banking stuff for the money to deposit in stuff
so that is good as for the joining date is 26/10/2026
which is perfect cause my end sem exam is going to end on 24/10/2026 so giving me two days time to relax and recover for the intern and prep for it great timing
