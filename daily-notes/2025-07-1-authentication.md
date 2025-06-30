# Attacking Authentication

A system authentication is the first layer of defense across any website or application. There are several ways for authentication:

## Authentication Methods

### Username Password
Most commonly observed and used everywhere.

### OTP Authentication
OTP sent to your email or phone number which is stored in the database and when you enter that OTP and it is same as the database OTP then authentication is approved.

There are more ways of authentication but for now I will study how to attack this authentication - not actually attacking but learning how to do that.

## Basic Authentication Vulnerabilities

So 90% of the web application uses basic username password method for their security interface but they don't know someone with skills can crack it easily.

And those web applications that have very important info like money, credit card details and stuff they use multiple layer of authentication and even more for high-level customers like billionaire accounts - for that they use OTP authentication, finger and retina scanning or stuff for verification which makes their account tough to crack and tough to gain access to.

Sometimes he can become a different person - he got split personality disorders. The personality of Mr. Robot make him a hacker but the personality of Elliot make him a protector, a guy who wants to save world but doesn't have enough courage to take the step needed for doing it. Mr. Robot is a personality that is evil, harsh, rude but is capable of taking steps that can save the world.

## Bad Password Practices

Usually web application doesn't focus much on safety so they don't set up limit and conditions on username and password to be used so people use simple password and easy password that they can remember but they forget that they are ignoring the safety of their account which should be remembered.

So using brute force approach one can try to crack password and enter but hackers use brain - they know tools, they find enough about the person they are targeting like name, DOB, nickname, likes, dislikes, pet name etc and setup custom list of passwords in text file and then using these tools run a command and let the tool scan for password and tell you the password. No need of you to crack it or something and spend time so you this too takes a lot of time sometime but it is saving tons of time and power for you.

I know all this because I have used these tools myself though I got no practice of it but I am thinking of why not try to learn a little about it too - obviously with permission and safe environment.

## Information Disclosure Issues

Sometime while entering username and password the code returns what is incorrect instead of just returning "user not found" or any error. This makes the user somewhat tell about whether the username actually exist or not and sometimes it returns "incorrect password" which means that username exist and might be correct but the password you entered is wrong - that is very useful for checking if the user exist or not or the username they entering is correct or not.

## Password Change Functionality

Developer while creating a username password format they sometime also add a feature of password change which is both necessary for a website but also opens the application for vulnerabilities. Sometime developer might make their login page safe but leave vulnerability in their password change page which is most commonly observed in new developers and should be treated before anyone try to use their account for bad purpose.

## Forgotten Password Functionality

This is observed as the most weakest link at which to attack in web application for login as here we don't need to crack password - sometime we just need to give answer to the personal info he gave like favourite colour, mothers name, memorable dates and stuff.

As this have much smaller set of potential answers then a 8-9 digit or alphabet password, don't you think?

And usually people think that this question will only be answered by him if he forget password so he keep it as simple as he can remember like: "Do I own a boat?"

This type of question got way less potential answer than cracking password.

And you might have observed that they make their login page so safe that you can't attempt password multiple time or stuff but when you use forgotten password they let the no of attempts open - hence this is considered the weakest link in gaining access to application.

### Modern Improvements

But this was of past time - now developer got skilled as I always said. Now they send a URL which is time limited directly to your email if you want to do some password change or forgotten related stuff which makes it secure nowadays but still there are developer who using old means and not thinking about account safety.

You might have used Instagram or other tools which are considered most secure nowadays because they sent URL to the already logged in email which you used to register to send OTP or URL for forgotten password.

But some are dumb - they ask you to give a email address to send that URL to and openly give you access to the account - not safe at all.

### TIP
Even if the application does not provide an on-screen field for you to provide an email address to receive the recovery URL, the application may transmit the address via a hidden form field or cookie. This presents a double opportunity: you can discover the email address of the user you have compromised, and you can modify its value to receive the recovery URL at an address of your choosing.

Yeah sometime they don't give your everything in hand but use your brain - collect some list of pattern they are using to send data, try to decrypt it and use it for your wish.

## Remember Me Function

I even myself have used this functionality a lot knowing that it too was vulnerable and can be exploited if known by person how to exploit.

This remember me function works in this way - when user enter their username password they submit remember me which in back end setup a cookie of the user that stores his info and everytime you login again and use that remember me it pass to server that already existing user came and bypass all the authentication and provide you entry without any problem.

This is a very good feature saving a lot of time of people but also have several flaws in it.

As I knew we can read the communication between backend and server using tools like Burp Suite so we can see the message sent and if we find enough message to identify how it is working we can use it as we wish by sending request directly to server and again gain access.

Man there is tons of ways to gain access to server - I know it just sound easy and doing this will be very tough but at least I know that web application have flaws that can be used.

## Common Authentication Issues

- Incomplete validation of credentials
- Non-unique username
- Predictable username
- Predictable initial passwords
- Insecure distribution of credentials

## Implementation Flaws in Authentication

- Insecure storage of credentials
- Securing authentication
- Use strong credentials
- Handle credentials secretively
- Validate credentials properly
- Prevent information leakage
- Prevent brute force attacks
- Prevent misuse of the password change function

## Conclusion

Authentication functions are perhaps the most prominent target in a typical application's attack surface. By definition, they can be reached by unprivileged, anonymous users. If broken, they grant access to protected functionality and sensitive data. They lie at the core of the security mechanisms that an application employs to defend itself, and are the front line of defense against unauthorized access.
