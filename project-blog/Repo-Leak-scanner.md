# RepoLeak Scanner 

## Introduction

Ever wondered how secure your GitHub repositories really are? What if I told you that your API keys, database passwords, and secret tokens might be sitting right there in plain sight for anyone to find? 

This is the story of how I discovered the world of repository scanning and built my own tool to hunt for leaked secrets. From a curious full-stack developer to building RepoLeak Scanner - here's my complete journey, step by step.

## How It All Started

Actually I was studying about web application safety and there I came across the importance of .env files in any web application project, but as I entered deep into it I got to know how important it is to keep env files safe and how unsafe GitHub repositories are if proper procedures are not used while building any project.

As I am myself a full stack developer and while studying, my professor told me the importance of hiding .env files and not writing hardcoded passwords in your project, but I thought it was just preferred syntax but now I understand its importance.

## The Discovery

Hence I decided to dive deep into .env files. So while studying I got to know I can scan anyone's git repo and find leaks if there are any in their project like api-keys, db-passwords or auth secrets, etc. using open source tools like gitleaks and trufflehog, which are famous tools.

## My Testing Approach

So I studied them and practiced them by trying to scan for vulnerabilities. I started by:
- Scanning my own repo using git token 
- Scanning repo using url link
- Scanning local repo

### Setting Up Git Token Access

So before using my own repo I googled and found out that I have to set certain permissions and create a fine grained token:
- Settings->tokens->fine grained tokens
- Set token name, description, time, repository access
- Permission enabled:
	- Repository contents: Read only
	- Metadata: Read only
- Generate token
- Copy and save it for future access of repo

### Different Scanning Methods

**Using url link:** You can directly copy url link from github profile and provide it while using the tool.

**Using local repo:** You can copy the repo by writing 
`git clone https://github.com/damnkrishna/practise-leak-repo.git`

After doing that you can just perform your scan. Now you have this repo in your local laptop and can scan it without any problem.

### Is This Safe?

You might be thinking what if someone catches you using these things, but that's not how it works. GitHub provides you open-source which means you can copy anyone's code and no action will be taken against you because you are the one who provided access to copy code before pushing it on git. Hence yes, it is safe. Just don't scan repos of other people - they might have some security setup to track people who try this with a bad mindset.

## Working with Gitleaks

Now I will be proceeding with scanning my own repo and my own projects using gitleaks. First you have to setup gitleaks on your kali Linux.

### Installation and First Scan

Install gitleaks on kali and scan your repo:

```
┌──(damnkrishna㉿kali)-[~]
└─$ gitleaks detect --source=./e-commerce-website --report-format=json --report-path=gitleaks-report.json

    ○
    │╲
    │ ○
    ○ ░
    ░    gitleaks

2:42PM INF 5 commits scanned.
2:42PM INF scan completed in 68.9ms
2:42PM INF no leaks found  
```

Using this command it will scan the whole repo of yours and return the number of leaks in your repo. It will also show the number of commits you did in the project.

### Understanding the Results

So basically now you know there are leaks. You must be wondering now how will you know them. So gitleaks either prints leaks directly after running code, but here I used it to save that data in a json file I named gitleaks-report.json.

You can see that in the above code.

Print the saved report by using cat and here you get all the passwords that leaked and can use them.

## The Problem: No Vulnerabilities Found

So obviously as anyone who gets to know such cool things must try to find vulnerabilities or leaks in their own repo and projects, I did that but got to know that my projects have no vulnerabilities or you can say I coded clean from the starting. But not everyone does that.

I also got little discouraged as any beginner hacker - I need quick results, I want passwords, I want them to boost my interest and my confidence, which was not possible in my own projects.

## Creating a Test Repository

So I decided to build a public repo with known password leaks or vulnerabilities. I established myself for that - I built a repo named practise-leak-repo and performed all the scanning again, but this time I don't want you to go the long way of generating tokens and changing permissions. 

Basically you don't need anything to scan anyone - you just need their username to enter into their repo. So now I will be using local repo.

### Testing with Vulnerable Repo

So as I built a repo named practise-leak-repo:

```
┌──(damnkrishna㉿kali)-[~]
└─$ git clone https://github.com/damnkrishna/practise-leak-repo.git
```

### Success! Finding Real Leaks

And now I used gitleaks which returned me the leaks:

```
┌──(damnkrishna㉿kali)-[~/test-leak-repo]
└─$ cat gitleaks-report.json                                                           
[
 {
  "Description": "Generic API Key",
  "StartLine": 2,
  "EndLine": 2,
  "StartColumn": 2,
  "EndColumn": 25,
  "Match": "api_key=ABCd-1234-SECRET",
  "Secret": "ABCd-1234-SECRET",
  "File": "config.txt",
  "SymlinkFile": "",
  "Commit": "96ff75fda4f91873126314c44a3394287d1381b5",
  "Entropy": 3.625,
  "Author": "TEST user",
  "Email": "test@example.com",
  "Date": "2025-06-08T09:32:52Z",
  "Message": "ADD fake secret keys for testing",
  "Tags": [],
  "RuleID": "generic-api-key",
  "Fingerprint": "96ff75fda4f91873126314c44a3394287d1381b5:config.txt:generic-api-key:2"
 }
]
```

This was actually very important for me to gain confidence. This might help you too to gain energy and actually it gave me ideas too.

## Exploring TruffleHog

So I knew there is one more tool trufflehog which works kind of similar but is not user friendly as it returns leaks in a format not easily readable.

So I decided why not build a project which uses both the tools and scans any repo that is public and finds leaks in it. So both the tools have different algorithms for finding leaks, so why not use both - maybe it will return the leaks that the other can't find. 

And at last I can summarize both of them and provide a summary of both tools, also storing the result of individual tools in a file each.

Hence the idea got into my mind and I started building my project.

### Installing TruffleHog

So as I have completed the gitleaks and somewhat learned enough to try other tools, hence next I tried finding leaks using trufflehog.

How to use:
- Install trufflehog

```
┌──(damnkrishna㉿kali)-[~]
└─$ sudo apt update             
Hit:1 http://http.kali.org/kali kali-rolling InRelease
1285 packages can be upgraded. Run 'apt list --upgradable' to see them.
                                                                                            
┌──(damnkrishna㉿kali)-[~]
└─$ pipx install trufflehog
  installed package trufflehog 2.2.1, installed using Python 3.13.2
  These apps are now globally available
    - trufflehog
done! ✨ 🌟 ✨
```

### Using TruffleHog

- Scan a git repo locally using trufflehog
- Save report in trufflehog-report.json
- Read report 

The majority of the process is the same for both the tools but output is quite different.

### The Output Problem

Example:
```
┌──(damnkrishna㉿kali)-[~]
└─$ trufflehog git --repo_path ./practise-leak-repo --json > trufflehog-report.json
                                                                                            
┌──(damnkrishna㉿kali)-[~]
└─$ cat trufflehog-report.json
{"branch": "origin/main", "commit": "Create outputgitleak.txt", "commitHash": "458566d6bb3fac543108f390fe397ef532923d88", "date": "2025-06-08 15:43:35", "diff": "@@ -1,89 +0,0 @@\n-┌──(damnkrishna㉿kali)-[~]\n-└─$ git clone https://github.com/damnkrishna/practise-leak-repo.git\n-\n...
```

This is how the output of trufflehog looks - quite tough to read and find leaks. So one more idea came into my mind: why not write a script which will convert this output into a human readable form and easy to understand too.

## Building the Combined Solution

I gave this thought a lot of time and tried too, but it is a little tough though I succeeded in doing it, but it is something I will be targeting in its future scope.

I had one more thought in mind which suited better for now - I decided to write a script which will run both tools and return its summary. I know it sounds easy but doing it is little bit tricky as you will be provided repo link or local repo root. Once you have to use it for both simultaneously and provide output, save them in separate files, then also while summarizing it, not to just print the whole file.

### The Challenge

You have to show only key points, only leaks, not extra stuff. So writing that script was also difficult for me so I took help from Google. Hope I will be able to do it myself soon, but it was quite interesting to do.

### The Result

With proper help I was able to convert 100s of lines of not important info into a short summary of leaks. Here is an example:

```
Leak #5:
  File: outputgitleak.txt
  Description: Generic API Key
  Commit: 458566d6bb3fac543108f390fe397ef532923d88
  StartLine: 75
  EndLine: 75
  Secret: ABCD-1234-SECRET
```

This is how summarized and clear it looks now. Isn't it also how cool it is? For someone not from cyber background they will be in shock with this project, don't you think?

## Final Thoughts

This is all for the working of the project. If you want to see the code and script you can check out my repo. Leaving a link here:
https://github.com/damnkrishna/RepoLeak-Scanner.git
