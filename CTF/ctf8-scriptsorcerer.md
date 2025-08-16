# Web Exploitation CTF - Script Sorcerer

## Challenge: Renderer

### Overview
**Introducing Renderer!** A free-to-use app to render your images!

The task was there is an image upload and renderer website with somewhere a flag hidden in it, and we have been provided with the source code for website with an example secret flag for syntax of flag that might be found later.

### Initial Analysis
The basic website had nothing - it was just to showcase that it's a website. Everything was already written in the `main.py` file.

### Discovery Process

#### Step 1: Finding the Developer Endpoint
It was mentioned we can gain the secret flag only by using `/developer` as a URL, but here too it was not that easy. You have to first open `/developer`, but at first it will be empty.

#### Step 2: Hash Generation
As you open `/developer`, it will set up a random 64-bit hash that you can see on a different URL: `./static/uploads/secrets/secret_cookie.txt`

Here it will show the newly created hash that is nothing else - it is the `developer_secret_cookie` without which you can't get to the flag.

#### Step 3: Cookie Authentication
Our next task is to use this hash as a cookie in developer and get access to the `flag.txt` file.

For that, we have to use **Burp Suite**:
1. Edit the request while sending request
2. Create a new cookie attribute with `developer_secret_cookie:<64-bit hash>`
3. Enter it in the request

#### Step 4: Flag Retrieval
It was mentioned too in the `main.py` that:
- If the hash matched with `secret.txt` hash, it will return us a message with the flag
- If it doesn't match, it will return us "you are not a developer" message

### Solution
This way, as the `developer_secret_cookie` matched with `secret.txt`, and hence the flag was found successfully.


<img width="1536" height="728" alt="image" src="https://github.com/user-attachments/assets/b7cb9dbd-a5c0-4d67-98f0-c081846c2ac9" />
---

**Key Takeaways:**
- Always check for hidden developer endpoints
- Look for dynamically generated authentication tokens
- Use web proxies like Burp Suite to manipulate cookies and headers
- Source code analysis is crucial for understanding the authentication mechanism

