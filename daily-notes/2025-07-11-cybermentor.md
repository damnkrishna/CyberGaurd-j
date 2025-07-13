Enumeration 


there is specifically 4 stages of reconnesence 
-Target validation
-Finding subdomain
-Fingerprinting
-Data Breaches

# target validation
	whois , nslookup , dnsrecon

# Finding subdomains
	google fu, dig , nmap , sublist3r, Bluto, crt.sh

# Fingerprinting
	nmap, wappalyzer ,whatweb, builtwith , netcat

# Data breaches
	haveibeenpwned


so like enumeration is itself some big stuff main reason behind it is it helps  find domain open ports vulnerability and for that if u have pro version of burpsuite then it is more easy as it provides u active scanning too which actually release a lot of stuff


-so for basic enumeration u can see request and response of the website using burpsuite
-then for weak credentials or gaining access to website
	u can try for leaked password or stuff on
	-infoleak.io
	-intelx.io
	-hunter.io
	-weleakinfo

wealeakinfo is a good application but google doesn't support it might be related to some data breach or something or unsafe to use
and other data breach leak stuff 


-install waffalyzer 
	it tell u info about the website without even doing any scan and i actually very helpful download as a extension infirefox

-check for domain names and website page for info as much as u can find just in case u need it right 

-if we know website name which we do we can perform some basic vulnerability scan using nikto 

	`nikto -h https://<ip>`

this will tell u port website is hosted on vulnerability it have data that u can use and all the basic scan needed for a website

even nikto provide u with ip for the website which then u can use for nmap scan and stuff

- `nmap -p 443 --script=ssl-enum-ciphers <ip> `

this tells u the rating of security feature involved in the website like it will tell u the cipher security level by rating it from A-F important for enumeration tough to use 
involves great skill to hack using ciphers and stuff


-normal nmap scan

`nmap -p80,443 -A -T4 <ip>`

Scans ports 80 and 443 on the target IP and performs an aggressive scan to gather:
-OS information
-Service and version details
-Script-based detection (like SSL info)
-Traceroute info
-Uses fast timing for quicker results


