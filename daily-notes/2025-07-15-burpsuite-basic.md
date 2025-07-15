# Burp Suite Basics

So Burp Suite is a tool used for web pentesting and it is the best and most famous tool used by web pentesters. Basically whatever you do for web exploitation you can do it with Burp Suite if you have enough mastery of Burp Suite and its usage. So based upon my recent goal I will be doing only web pentesting and will master it and will try to do stuff without using ChatGPT or Copilot so that I can do things myself and handle stuff myself.

So before using you have to remember you have to setup your browser for letting us read all the request and response. So for that I am using Firefox and have changed its settings to manual HTTP proxy setting with my own localhost IP and port 8808 so that I can listen to anything and everything on my own.

So here I go with basics:

## Target:
It is used to show every single thing you do on browser. If you think you search something then it runs only that website, well that's not the case. Actually when you run some link it also runs a lot of browser personal sites and also the needed website for running that specific website you want to browse. Also when you just do a normal authentication like putting username or something, in reality there takes places a lot of steps in the back that if observed can reveal a lot about a website which we need.

So basically Target shows us everything and also provides an option where you can choose some website or link and add it to the scope for future which shows only the website you added into the scope and none other stuff.

That is very helpful in narrowing down the search.

## Proxy:
This is so far the most important tool I think I found in Burp. It gives you option to intercept the request. Basically it creates a stoppage that asks you to forward what you like, even edit it if you want, then pass it to the browser. Basically it's like a checkup done by police for stuff and letting them pass according to our will.

So every request we pass do stuff in the browser and web application. Also the Proxy tab stores each request we forwarded and stores it in HTTP history tab that is useful to keep track of everything you did.

So basically this is how you do these stuff. Like I have participated in some web pentest related CTF so we first read the source code and stuff and try to find info as much as possible but if we do all that without using Burp Suite we just doing reconnaissance like normal people but we ain't that. So we open our Burp Suite and on the intercept and then as we do every page scanning we are also storing their request and response for everything we do.

That is very helpful as sometimes we find data in these response and request though I am unable to identify it yet but will soon be doing it myself.

Also there is some small feature not that much used but good to know about them too like match and replace to interchange some words you want.

## Intruder:
So this is too a unique feature but it is used in some special cases where you have to upload payload like for vulnerability where you can sometime access database or storage by using searching tab or HTML entry tab or something where you can enter input to the web application. This is most commonly observed vulnerability as sometime people leave their web application vulnerable to XSS or vulnerability which hacker can use by entering certain payloads as the input.

Actually in my last CTF there was this notorious note web page where we had to do this specific thing and I never knew that I had to this. We have to enter payload as there is a XSS vulnerability observed.

So it allows you to send multiple payload as input which is automated where you can even control the time and type of input to send. Even you can provide a list of inputs to enter for that which is obviously a time taking process but very useful as it shows request and response for each input which we can read and understand the vulnerability.

## Repeater:
This too is a specific tool but so far the most experienced and creative guy can use it so well that I am not able to control right now as this is something you do to check the request and update it according to our need and check for response of each modification. This help too in understanding vulnerability. This allows modification of request resending them and allows individual requests that is quick and great if you are skilled for identification.

## Scanner:
The Scanner tab is a key feature of Burp Suite Professional. It provides automated vulnerability scanning capabilities, allowing users to identify security flaws in web applications and APIs. This feature helps streamline the testing process by automating repetitive tasks, enabling security professionals to focus on more complex manual testing aspects.

## Sequencer:
The Sequencer in Burp Suite is used to analyze the randomness and predictability of tokens such as session IDs, CSRF tokens, or any other values meant to be unpredictable. It helps determine if these tokens are generated securely or if they can be guessed or predicted by an attacker. By collecting a large number of tokens and running statistical tests, Sequencer identifies patterns, character distributions, and entropy levels. If a token shows weak randomness, it could lead to serious vulnerabilities like session hijacking or authorization bypass.

## Collaborator:
Burp Collaborator is a feature available only in Burp Suite Professional, not in the Community Edition. It's used to detect out-of-band vulnerabilities like blind XSS, SSRF, and XXE by generating unique payloads that trigger external DNS, HTTP, or SMTP requests. These interactions are then logged by the Collaborator server to confirm vulnerabilities that don't show up in direct responses. While Burp Community Edition doesn't include this feature, users can use tools like Interactsh or external services like webhook.site as alternatives to perform similar tests.

## Decoder:
this is a very useful tab as is lets us decode and encode text from one format to another even gives us many option for the type of encoding or decoding u want to do 
allows hash conversion but obviously decoding of hash is not possible we have to calculate it or compare it so solve that 

useful tab very useful.
