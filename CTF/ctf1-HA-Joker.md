# HA JOKER CTF

## What I'm Doing Today

So today I am doing a penetration testing CTF which involves using:
- Enumerate services
- Brute force
- Hash crack
- Exploitation
- Privilege escalation

These stuff.

## Starting with Enumeration

Starting with enumerating the target machine using nmap:

```bash
nmap -sV 10.10.30.151
```

Command to find open ports and device running as I needed to find the apache version running on the device.

**Found:** Apache 2.4.29

**Open port that doesn't need authentication by user and password:** Port 80

So port 80 is used to provide admin access so it has to be the port that doesn't require authentication.

## Finding Files with Secrets

So next I have to find the file that was stored in that port that might have secret kept in it.

Actually I didn't know how to do that so I took help of ChatGPT. I know it stops me from thinking or doing stuff on my own but I need the answer. I am doing these CTF and stuff only today and tomorrow.

So it told me to use some in-built function.

## Using dirb

Ok so this dirb stuff works this way - it has saved a list of common files that usually is used to store stuff like secret stuff and scanned that on the website with port giving as input and it will scan and return the finds with similar name as output which we require. We need two files: one that stores our secrets, other that stores the backend password.

**Command used:**
```bash
dirb http://<TARGET_IP>:<PORT>/ /usr/share/dirb/wordlists/common.txt -X .txt,.php,.bak
```

Here I entered target_ip and port which was vulnerable that was port 80.

## Finding Username and Password

So now I need to identify username for the authentication regarding later authentication that is needed on port 8080 login page.

So now I did identify **username: joker** from secrets.txt file but now I also need password for username joker.

Fucking hell I was thinking how will I find the password but ChatGPT is good no doubt it is taking jobs. It told me to use hydra and find the password using custom build list for answer.

```bash
hydra -l joker -P /usr/share/wordlists/rockyou.txt -s 8080 10.10.30.151 http-get /
```

**Found:**
- Username: joker
- Password: Hannah

## Using Nikto

So next we have to use nikto for finding possible directory. For that I used this command as I know the credentials:

```bash
nikto -h http://<IP>:<PORT> -id joker:hannah
```

## More Directory Finding

Next we again used dirb for finding directory available so got to see there is an administrator directory and there is some file stored in it. Again using dirb I have to find the files.

So found a backup.zip file in it which have the same password as that of port 8080 which was "Hannah".

## Finding Another User

So next I have to find the another super duper user that is available. For that I opened db file inside backup.zip file. There I found the other username:

**User: admin**

Now I have to find the password for it. For that I will be using john the ripper.

**Password: abcd1234**

## Where I Got Stuck

So next all the stuff is related to reverse shell and I don't think I am that good to do it or even understand it at this place so I stopped and watched YouTube video for further learning.

## My Realization

I understood one thing - I am not yet ready to attend CTF challenges and clear CTF rooms on my own. I need practice and have to learn basics first. I can't just enter into cyber this way. I have to do some work on myself to enter these stuff. It's high level.

