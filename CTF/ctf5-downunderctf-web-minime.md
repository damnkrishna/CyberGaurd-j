# MINI Me CTF Writeup

## Initial Discovery

Its a website which has simple authentication page where u have to enter email and password and with that u can enter the website and there is a video and audio saved that keeps on playing itself but also on the basis or code there is a admin page where the flag is saved admin/flag location but it is unauthorised for me so I have to pass a way out for it.

## Reconnaissance Phase

I scanned whole website using burp but found nothing that I can use for myself so for now will proceed next with nikto and nmap:

- `nikto -h <ip>` is still running and giving some idea which i will see later but for now i know there is a admin page that can be opened using specific url that i have to find for the flag
- nmap scan for ciphers returned and it has good strength but ya few strength too
- next a normal nmap scan is also running in the background that will be providing open port details etc that can be useful

## Code Analysis

So based upon what i found till now the flag is stored in environment and will only be returned in a specific domain that is using:

```python
@app.route("/admin/flag", methods=["POST"])
def flag():
    key = request.headers.get("X-API-Key")
    if key == API_SECRET_KEY:
        return FLAG
    return "Unauthorized", 403
```

## Finding the API Key

So next i will try so next i found in the source code that there is a map of the file structure stored in code which have path `/static//js/main.min.js` which revealed a text file that have very important data stored that can be used if done properly so using chatgpt i found the api key.

That lmsvdt is the API key!
key:lmsvdt

## The Real API Key Discovery

TUNG-TUNG-TUNG-TUNG-SAHUR

Bro craxy i found the api key it was this:
**TUNG-TUNG-TUNG-TUNG-SAHUR**

And here i used burp suite for the seeing all response and request and there i found that there is a filed named `.map` that have same data stored which provided a python script that is giving a list of details that if u put in console of that web application it provides u with x-api-key.

## Exploitation

That when used by intercepting request and posted again with new `/admin/flag` tag and correct api key it will return u the flag which actually i did somehow.

## Flag Captured

And the flag is:
**flag: DUCTF{Cl13nt-S1d3-H4ck1nG-1s-FuN}**

## Victory!

Lmao best day of my life bro i successfully cleared one ctf on my own on my fucking own crazy bro crazy this is so exciting i am gonna die man
