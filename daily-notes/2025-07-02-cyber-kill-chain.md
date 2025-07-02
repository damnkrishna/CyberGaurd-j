# CYBER KILL CHAIN

it is a military concept which involves discovering the target, its identification, then taking decision, attack the target, and finally destruction of the target.

cyber kill chain help u understand and protect against ransomware attacks, security breaches as well as advanced persistent threats.

---

## Reconnaissance

it is the phase where u find info about your target as much as possible  
also it is the planning phase for the attack  
u decide everything in advance, the strategy and stuff which includes osint too. (which I have quite a little of experience by now)

it includes studying your target company name  
company info and employee info  
emails address  
phone numbers publicly available

it told us three tools to use but as I have read a little more ik that there are a lot of tools which use different methods and sometime provide unqiue result and scans different database so its important to use multiple tools and not stick to one or two

but these 3 are most imp for now  
- hunter.io  
- theHarvester  
- OSINT framework

some of these tools are now paid earlier it used to be free but it is better to keep this stuff paid as if anyone can read and see such stuff it will be harmful for everyone to read publicly available breaches data and info about someone.

---

## Weaponization

so this is the most harmful step and also the step which can get u caught so whenever u decide to target someone u don't just directly hack him because that would be difficult I would have said no way but as I know everything is possible in cyber everyone leaves vulnerability so. ya u dont directly hack into someone u need malware to inject into his device to gain access to it either u can code it yourself but this usually takes time and require great skills  
and also it is the safest as u know your code no website have that code available and neither anyone can use that malware for themself somehow as it is purely yours and new

i am saying this because beginner hackers they cant write such malware themselves so they buy it bro other website or hackers for price  
usually using darkweb which is itself not safe as it tracks what u do and sometime secret agency set up honeypot on these website which can result in revelaing your identity this is one of the biggest reason hackers career end early as they dont think that much

and there is one more problem in using others script of malware they might have injected some code in the malware that not even provides the buyer access to the target he will be hacking but also providng the seller access to it

and i think sometime seller do this for their own safety as they sold that malware to someone for money reason but if that hacker performed some high level hack he should somehow have info about the buyer to frame or get him caught rather than getting caught himself

i know this much about hacking now that never trust other hacker he will sell u for his own safety

it is the rule of hacking to trust yourself and keep yourself anonymous always

**In the Weaponization phase, the attacker would:**

- Create an infected Microsoft Office document containing a malicious macro or VBA (Visual Basic for Applications) scripts. If you want to learn about macro and VBA, please refer to the article "Intro to Macros and VBA For Script Kiddies" by TrustedSec.
- An attacker can create a malicious payload or a very sophisticated worm, implant it on the USB drives, and then distribute them in public. An example of the virus.
- An attacker would choose Command and Control (C2) techniques for executing the commands on the victim's machine or deliver more payloads. You can read more about the C2 techniques on MITRE ATT&CK.
- An attacker would select a backdoor implant (the way to access the computer system, which includes bypassing the security mechanisms).

---

## Delivery

it refers to deciding the method for transmitting the payload or the malware into the target device

a hacker have several ways to deliver the malware and three of the most used and observed ways are

### Phishing email

so hacker based upon osint find out that a person from company 1 likes the post of some guy in company 2 on social media platform and linkedin

so they might be even communicating with each other through emails so hacker knew this info so he can use this info

by creating a mail similar to that of person 2 using his first name and last name and similar to his domain and send person 1 email with a file attached to it  
ex. invoives so

as person 1 might be curious of the email and opens it but he doesn't know that hacker installed a malware in that with some fake info and as person 1 think it is fraud or something hacker already got the info he needed about the person that's how phising email attack work

cool right!

### Distributing infected usb drives

An attacker might decide to conduct a sophisticated USB Drop Attack by printing the company's logo on the USB drives and mailing them to the company while pretending to be a customer sending the USB devices as a gift.

it is a common attack where hacker distribute usb drives for free in public either by saying that his music is in it pls try or something and target takes it  
and inject it into his device and boom u have been hacked.

### Watering Hole Attack

this attack too use osint skills as u can find out which website the user usually use and logins on daily basis or frequently and based upon hacker skill he can exploit that website and make the user go to his personally controlled website and end up gaining access to that user device

i know all these way feels quite easy except the last one it requires web application hacking skills  
but method 2 i have seen in movies and series and people dont give a shit about safety if they are getting something for free dont u think.

---

## Exploitation

These are examples of how an attacker carries out exploitation:

- The victim triggers the exploit by opening the email attachment or clicking on a malicious link.
- Using a zero-day exploit.
- Exploit software, hardware, or even human vulnerabilities.
- An attacker triggers the exploit for server-based vulnerabilities.

---

## Installation

This is the stuff that i seriously have interest in as in my last blog i wrote i told u that i found a malware in my brother laptop that leaked his personal info but the malware injector didn't deleted it or something after using it to gain info

it is still present in my brother laptop which is not good ik.

but as sometimes people find that there is some malicious malware in his laptop or device present so they remove it or delete it and sometime it gets disconnected because of nay problem

so hacker have to maintain a backdoor to regain access of the device which is very important for a hacker to do.

**The persistence can be achieved through:**

- Installing a web shell on the webserver. A web shell is a malicious script written in web development programming languages such as ASP, PHP, or JSP used by an attacker to maintain access to the compromised system. Because of the web shell simplicity and file formatting (.php, .asp, .aspx, .jsp, etc.) can be difficult to detect and might be classified as benign. You may check out this great article released by Microsoft on various web shell attacks.
- Installing a backdoor on the victim's machine. For example, the attacker can use Meterpreter to install a backdoor on the victim's machine. Meterpreter is a Metasploit Framework payload that gives an interactive shell from which an attacker can interact with the victim's machine remotely and execute the malicious code.
- Creating or modifying Windows services. This technique is known as T1543.003 on MITRE ATT&CK (MITRE ATT&CK® is a knowledge base of adversary tactics and techniques based on real-world scenarios). An attacker can create or modify the Windows services to execute the malicious scripts or payloads regularly as a part of the persistence. An attacker can use the tools like sc.exe (sc.exe lets you Create, Start, Stop, Query, or Delete any Windows Service) and Reg to modify service configurations. The attacker can also masquerade the malicious payload by using a service name that is known to be related to the Operating System or legitimate software.
- Adding the entry to the "run keys" for the malicious payload in the Registry or the Startup Folder. By doing that, the payload will execute each time the user logs in on the computer. According to MITRE ATT&CK, there is a startup folder location for individual user accounts and a system-wide startup folder that will be checked no matter what user account logs in.
  You can read more about the Registry Run Keys / Startup Folder persistence on one of the MITRE ATT&CK techniques.

In this phase, the attacker can also use the Timestomping technique to avoid detection by the forensic investigator and also to make the malware appear as a part of a legitimate program. The Timestomping technique lets an attacker modify the file's timestamps, including the modify, access, create and change times.

---

## Command and Control

- command and control

---

## Actions on Objectives (Exfiltration)

- actions on objectives (exfilatration)
