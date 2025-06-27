# OSINT Practice Report 1

## Target
**Username:** kal1_dr1ft

## Objective
I will be practicing and will be trying to find all the info I can find about this username.

## Process Planning
I will be taking the following approach:
- I got his username so I will be scanning username for connection with online platforms using Sherlock
- I was thinking first try using manual OSINT scanning platform like Google and other servers
- Then if I will try to access some email if possible
- Scan in holehe and maigret for email connection if any
- Use SpiderFoot or recon-ng to scan for email and username and phone number the details I found

Will be doing these things one by one so here I go.

## Investigation Steps

### Step 1: Manual OSINT - Google and Edge Search
I will be doing manual OSINT on Google and Edge.

So okay I scanned Google and Edge using "kal1_dr1ft" but found no result. As I got username there is no point of giving them broken tags as I got username that is enough to find if any stuff is available online or not.

### Step 2: Sherlock Username Scanning
I was thinking to scan his username on Sherlock so shifting to my Kali Linux virtual box.

So my old downloaded version of Sherlock was not working properly so I thought this might be the best opportunity to use some different way out and this time for OSINT I won't be using ChatGPT or any co-pilot and will do all I can find myself.

So I used:
```bash
pipx install sherlock-project
```

This enabled me to directly use Sherlock from my device. Yeah it is taking a lot of time to run but it scans a lot of device so for trial I scanned my own name and it provided output so I will be stopping it now and search for my target.

```bash
sherlock kal1_dr1ft
```

So Sherlock provided me with 13 results for the username but these tools also get accuracy problems sometimes. They just return output if that certain platform didn't stop it and didn't show 404 error so I have to check every result manually for existence of username.

#### Manual Verification Results
I manually checked 6 but got no website is responding correctly.

Yup x.com got connected but it too showed this account doesn't exist. Maybe not a real account maybe setup by some robot or ChatGPT tasked me that so I will remember this one.

So checked 5 more all fake.

But then I came across thread.com but there is a user named kal1_dr1ft but I don't have password so I can't sign in though for checking if the account actually exist I entered username and random password and it showed wrong password so this shows that username exists.

**Result:** thread.com and x.com showed a little result but not much.

### Step 3: Email Harvesting Attempt
Before scanning using powerful [tools] I thought there might be some tool that can scan web for email address using username available and got to know some famous tool like Hunter but it is paid now so now I will be using emailharvester which is a pre-installed Kali tool which searches different search engines for email address using username as input and put it into txt file which then I will have to scan manually for accuracy but though I never have used emailharvester so first looking at its step to install.

So this email finder is not helping me much and for trying email scanning I need his email that I don't have so now I will try the two most powerful tools and then end my OSINT for today.

### Step 4: SpiderFoot
Using SpiderFoot I can't find anything. This tool is great but requires API keys to access data breaches and stuff which is somewhat tough and I am not able to use it well till now.

### Step 5: Recon-ng
Tool is also used for finding info if you have email or domain name or stuff so I don't know it will be of any help either so I am stopping and check what stuff can I do.

## Conclusion
So all I did was just for practice. Just I got to know the target was fictional and actually doesn't even exist so next my target will be a real username.

## Findings Summary
- **Google/Edge Search:** No results found
- **Sherlock Scan:** 13 potential matches, all verified as false positives except:
  - x.com: Account doesn't exist (possible placeholder)
  - thread.com: Username exists but account is password protected
- **Email Harvesting:** Unsuccessful due to lack of initial email address
- **SpiderFoot:** Limited results without API keys
- **Recon-ng:** Not applicable without email/domain

## Lessons Learned
- Automated tools can produce false positives
- Manual verification is essential
- Some platforms may show username availability even for non-existent accounts
- Real targets are necessary for meaningful OSINT practice

What do you think?
