# Breach Investigation (OSINT)

## Target
**What was the password for the computer used to run the U.S. Air Force Academy's public address system Sound Scheduler in 2019?**

## Background
So there was a data breach that happened in 2019 in US Air Force Academy that happened because a computer had low security and some hacker or not - now till now who hacked it and whether they even used the info they received from the device for some criminal work or not.

So in this CTF we have to find the password of the computer that was hacked that had low security or some people even say had no password at all. So that's our task - we have to find the password and check for CTF answer in the format: `cube{password}`

## Initial Analysis
So for that first I tried to identify as much info I can so I broke the stuff and tried to analyze the data and found that in April 2019, US Air Force Academy was rewarded for having the best cybersecurity trainers for cadets.

As soon as this info got leaked I think - this is my thinking - someone took it personally and decided to hack into US Air Force Academy to prove that they can't even keep themselves protected and degrade their reputation. I am assuming this because they never used that info they found in the data breach as there was no cyber crime reported that used these information so it was more like just a show and not act stuff.

## Key Terms
Enough about what I think, this is what I find out from the terms:

- **Sound Scheduler**: someone who keeps track of flight schedules, creating and managing flights time
- **Public Address System**: used by air force to communicate in high noise area for clear communication with large group of people at distance or stuff

So based upon these terms I think the hack happened because a computer that was responsible for keeping track of sound scheduler and public address system of US Air Force Academy in 2019.

## About the Breach
So in 2019 a security breach took place in the academy computer involving Blackbaud, a third party company.

- Exposed personal information of individuals associated with academy
- **Timeframe**: May to July, 2019

### July 2019:
A system controlling public address system was:
- Exposed to internet
- Required no authentication
- Ran with weak/default credentials

## Research Findings
So after learning all this I find out one more most important thing that once there was a writer who wrote about all this in his report on:

**Platform**: TechCrunch.com

I tried a lot to access that platform and open the link for the blog but it was removed by US Air Force Academy for safety purpose as he stated and showed how even he was able to enter the computer and find info about individuals himself, showing the vulnerability and he also stated there was no password or default password in the device which he was easily able to enter into the computer causing all this data breach of this lot of people.

## Challenge Progress
So now to the target I have to find the password of that device.

I thought this would be easy but it wasn't this easy to be truthful. It is a 3 day CTF challenge but I am already exhausted at day 1 though the creator said that if no person was able to find password of that challenge they will provide hint after 24 hours, which is now 3 hours left only.

So I am reporting all I have done till now maybe after hint I will be able to find account password.

## OSINT Attempts
So first I manually tried to find info about the hack using manual OSINT on several services but didn't find much info as no one was talking about the password of the device because in reality who cares how the hack happened - they just only care about what data was leaked, are their personal info released or not and how find out about that and who was responsible, not how they were able to do that.

So no report, no blog actually wrote anything about how it happened except TechCrunch.com website. Even I think the person who wrote it was:

**Avinash Jain**  
**Date**: 2019/07/17

This is the date of report published on TechCrunch.com.

## Data Breach Analysis
So now I know a date and a website so as I know that the data was present once but is now removed so there must be some data still safe anywhere so I will try to find it on data breaches stored like:
- intelx.io
- dehashed

And stuff I actually scanned a lot of files, a lot of leaks for password and somehow anything related to so I found 3 data leaks on the date nearby to the date of hack happened:
- 21-06-2019
- 23-06-2019
- 24-06-2019

So I scanned all three for info but found nothing - not a single thing that can bring me close to the password.

I even set some domain name list to check for:
- usafa.edu
- airforce.mil
- blackbaud.com

But all resulted in no leak password.

## Default Password Attempts
So then I realized a thing which too was wrong - the reporter stated that the person whose device got breached was either not using password or was using default password.

So I tried to find the default password for sound scheduler and normal computer used in US and nearby area based upon Windows, Mac or anything else but none worked.

So now I will wait till 3:50 AM for the hint.

## First Hint
So the hint came - it was not any useful hint it just said use acronyms and u will know when u get the password so no guessing is required and it should be just 3-4 click away and he also stated that people are overthinking on this challenge - it ain't this tough at all, it is something that is no brainer but somehow no one is able to clear the task.

So one more hint will arrive at 3:50 AM tomorrow I will stay up for that and try to solve it in the night itself.

## Additional Findings
So here what I found more:
In 2019 there was also a DISA attack on Department of Defense during the exact same time leading to kind of same leakage but it was worldwide famous attack and leaked personal info of about 200,000 individuals during the time May-July 2019. It also leaked social security number of these individuals but later I find out it is not related to USAFA so I stopped digging in any more.

## TechCrunch Report Discovery
Later I told u I was searching for a report posted on TechCrunch.com about a person who gave a step-by-step guide about how the hack happened written by **Chris Vickery**.

He stated that the machine used for public address at that time was **Primex Event Scheduler Pro software** which have a default password.

But it didn't even work and also that the machine have port 80 open without any authentication required - that was a great leak and can be used by anyone somehow.
