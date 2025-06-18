# Mapping the Application

## Getting Back on Track

So I was making a project and I kind of got off the path from the last few days, so I thought why not get back by reading some topics related to the web application hacking handbook. So my today's target is mapping the application.

## What is Application Mapping?

It's basically before getting into any web application, you should have knowledge about the application like the structure, the forms, the pages available, the procedure and stuff. Usually you can find out about a website by just going through it and checking it out yourself - the login page, about page, and other functionality.

## Automated Tools (Web Spidering)

Also there are some built-in tools that can do this work for you and this thing is also called web spidering:

- **Paros**
- **Burp Spider** (part of Burp Suite)  
- **WebScarab**

These tools do a decent job of enumeration application content and functionality.

## The robots.txt File

So there is a file stored in each web application in the root server, usually named `robots.txt`. This file stores a list of URLs that the website doesn't want search engines to index and also to keep safe from web spiders.

That's exactly what we should be targeting first in any website and maybe it is stored by some other name, so scanning this might be the first way.

## That Mr. Robot Scene

Wtf, so have you watched Mr. Robot? In it there is a scene where the hacker somehow gains access to the website by some colleague's username or by having a job at that company and then with that signs into the website, then sets up a spider inside that listens to every login and gives all info it can gain with that listener. How cool is that!

I was wondering if I can do the same on my college website, so like in my college there is a student login and teacher login. So for now if I can just login into my page and set up a listener then gain access to the grades of the other students through that page. Hope so one day I would be able to do so.

## Access Levels Matter

So the tools and manual search for secrets depend upon the level of access you have gained. For example:

- A person who is not a user of some website has minimum access to anything
- But a person who has login has higher or more access to that application  
- But someone who has bought the paid version of that website has access to more features
- But whereas someone who is admin has access to all the features available in a web application

So based upon this, if you somehow gain access to higher and higher levels, you can control more and more stuff.

## Key Locations to Pay Attention To

The key locations to pay attention to are:

- Every URL string up to the query string marker
- Every parameter submitted within the URL query string
- Every parameter submitted within the body of a POST request
- Every cookie
- Every other HTTP header that in rare cases may be processed by the application, in particular the User-Agent, Referer, Accept, Accept-Language, and Host headers

## Identifying Server Side Technology

- Banner grabbing 
- HTTP fingerprinting
- File extensions
- Directory names
- Session tokens
- Third party code components

## How You Can Detect and Exploit Problems

Here's how you can detect and exploit each of these problems:

- **Client-side validation** — Checks may not be replicated on the server
- **Database interaction** — SQL injection
- **File uploading and downloading** — Path traversal vulnerabilities
- **Display of user-supplied data** — Cross-site scripting
- **Dynamic redirects** — Redirection and header injection attacks
- **Login** — Username enumeration, weak passwords, ability to use brute force
- **Multistage login** — Logic flaws
- **Session state** — Predictable tokens, insecure handling of tokens
- **Access controls** — Horizontal and vertical privilege escalation
- **User impersonation functions** — Privilege escalation
- **Use of cleartext communications** — Session hijacking, capture of credentials and other sensitive data
- **Off-site links** — Leakage of query string parameters in the Referer header
- **Interfaces to external systems** — Shortcuts in handling of sessions and/or access controls
- **Error messages** — Information leakage
- **Email interaction** — Email and/or command injection
- **Native code components or interaction** — Buffer overflows
- **Use of third-party application components** — Known vulnerabilities
- **Identifiable web server software** — Common configuration weaknesses, known software bugs

## Why System Knowledge is Important

So before hacking into any web application, the importance of the system knowledge is very important as there are many ways to hack into any web application. For different software there are different types of hacks possible.

So if you know the application is using something like SQL then you can do SQL injection and hack it, and that will be your choice based upon other choices you have.

## Legal Stuff (Important!)

And we can't just hack into any website online because it might backfire, causing problems to your career and future. Hence always remember to practice on some safe environment and take access before cracking any web application - preferred!

## Practice Environment

So as we are beginners, we need to practice somewhere, so I am establishing a DVWA locally for practice.

**DVWA**: Damn Vulnerable Web Application
