# Attacking Session Management 

Sessions play a crucial role in any web application as they enable applications to uniquely identify a user across different requests like admin user, etc. Also, they are the prime target for malicious attacks to bypass authentication and access admin controls by using and modifying tokens issued by web applications.

Sessions are used for:
- Login pages
- Online shopping platforms
- Banking stuff

Vulnerabilities:
- Weak session tokens generation
- Weak handling of session tokens

Alternative to sessions:
- HTTP authentication
- Sessionless state mechanisms
  - If token issued is fairly long (100 or more bytes)

## Weakness in Session Tokens 

### Encoding Methods Used
Session tokens are usually encoded using:
- XOR 
- Base64
- Hexadecimal

These can be decrypted/decoded for private info like username, email, password, date, role, etc.

### Types of Weak Tokens

#### Predictable Tokens
Observed usually in e-commerce and official websites that use several tokens daily, so one can learn and understand these session tokens and decrypt and use them for their own goal or gaining admin role or stuff.

#### Concealed Sequence 
Contains sequence that reveal themselves when the tokens are suitably decoded or unpacked:
- Have to understand pattern 
- Try different pattern
- Decode them
- Use for your use

#### Time Dependency
Session tokens that are generated based on timestamps or time patterns can be predicted by analyzing the timing of token creation and finding correlations with system time.

#### Weak Random Number Generation 
Poor random number generators or pseudorandom functions make session tokens predictable, allowing attackers to guess or calculate future token values based on observed patterns.

#### Full Blown Tests for Randomness
Session tokens should be tested for true randomness using statistical tests to ensure they cannot be predicted or have detectable patterns that attackers can exploit.

## Weakness in Session Token Handling 

Hijacking of session is possible if one just knows the token - no need to decrypt it. You just need to replace it with normal user token and you are in as admin.

### Disclosure of Tokens on Network
- System logs of various kinds
- User browser logs, web server logs
- Using false email or web page to target person - if he clicks it he gets transferred to a webpage controlled by us and we can access all user data, hijack the session and gain sensitive info

### Vulnerable Mapping of Tokens to Session
Weakness in the way the application maps the creation and processing of session tokens to individual users sessions themselves:
- A token re-assigned to a user every time he login
- Same session token for logging from different browser or computer of the same user account

### Vulnerable Session Termination
Sometimes even when we have logged out from the server or page the website sometimes was unable to remove or terminate that session token that is accessed can be used by anyone even if u have logged out

### Client Exposure to Token Hijacking
- Cross-site scripting attack
- Session fixation vulnerability

### Cookie Restrictions

#### Cookie Domain Restriction
Cookie domain restriction is a security mechanism that controls which domains can access a cookie. When a cookie is set with a specific domain attribute, it can only be sent to that domain and its subdomains. For example:
- Cookie set for `.example.com` can be accessed by `www.example.com`, `api.example.com`, etc.
- Without proper domain restriction, cookies could be sent to malicious domains
- Attackers can exploit loose domain settings to steal session tokens across related domains
- Always set the most restrictive domain possible for your application's needs

#### Cookie Path Restriction
Cookie path restriction limits which URL paths within a domain can access the cookie. This adds another layer of security:
- Cookie set with path `/admin` can only be accessed by URLs starting with `/admin`
- Prevents session tokens from being sent to unnecessary parts of the application
- Reduces attack surface by limiting where cookies are transmitted
- For example, admin session cookies shouldn't be accessible to public user pages
- Always use the most restrictive path that still allows proper functionality

## Secure Session Management

### Generate Strong Token

- Extremely large set of possible values
- Contain a strong source of pseudo-randomness, ensuring an even and unpredictable spread of tokens across the range of possible values

#### Cryptographically Secure Algorithm Used for Randomness
- Introduce a source of entropy some info about the individual request → adding uniqueness → timestamp, userid, sessionid, user-agent string

#### For Randomness Use:
- **Java**: `java.util.Random`
- **Python**: `secrets.token_bytes`
- **Linux**: `/dev/random` or `/dev/urandom`

#### Token Properties
**Uniqueness**: Making ticket to an event have a random, unpredictable code

**Signature**: Stamping each signature with a secret-seal that only a ticket user can create → proving authenticity

### Protect Tokens Throughout Their Lifecycle

#### HTTPS Implementation
- Token should only ever be transmitted over HTTPS 
- HTTPS should be used for every page even for static pages: help page, images
- Session token never be transmitted in URL
- If doing use POST requests
- Store token in hidden field

#### Proper Session Management
- **Proper logout functionality**
- **Session expiration based upon inactivity time**
- **Concurrent logins should be prevented**
  - Each time a new login of same user happens
  - Logout from other devices should take place
  - Warning should be shown on currently old page that login have take place in another device

#### Security Measures
- Cross site scripting, XSS attack should be stopped
- Arbitrary token submitted by user should not be accepted
  - User should be returned to home page
- Two-step verification should never be displayed back to user

#### Per-Page Token
Also a great way to stop session token usage as every time u enter a new page or already known page your session token changes every time u change a page and also terminate the old token so that it can't be used again ever

> **Cost Consideration**: Tell me one thing as people find vulnerabilities in session token so people install per page token or stop different vulnerability by using https pages only doesn't all these stuff cost them money like shifting from one token to per page token won't it take more computer storage and all?

**Answer**: Yes, adding per-page/request tokens and HTTPS introduces some cost, but:
- Storage/CPU impact is minimal
- HTTPS is free and standard now
- Security benefits far outweigh the tiny performance or code cost

## Monitoring and Attack Prevention

### Log, Monitor and Alert

Generally when attacked multiple automated request are entered that can be observed in application logs and the requester IP can be blocked stopping any future attempt to attack application.

**Bypass Methods**: 
- Can be surpassed using a proxy or VPNs or a firewall performing network address translation

### Attack Slowdown Techniques

You can also slow down any attack attempt by establishing a script that every time someone tries to edit request they have to re-authenticate slowing down attack and can even terminate that person's session who trying to modify requests.

**Bypass Methods**:
- Can be bypassed using Burp Intruder + IBurpExtender to automate a login each time logged out
