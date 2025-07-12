web pentest: notorious note 

so here we got a notes web app where u enter your note and it will show u the note down and also allow u to enter new note but 

here the catch I found we can submit only one note and if we enter new note the previously one get removed itself and also if u enter a note and refresh the page it will remain there for 1 minute 

but after that it will get removed itself after 1-2 minute time period this refers to 

core vulnerability 🔥 I found:

🧠 This app is vulnerable to a shared-state overwrite + admin bot timing issue — a CTF classic.

✅ What We Know
Admin bot posts a secret note (probably the flag) every ~1 minute.

Your note overwrites it temporarily.

If you refresh at the right moment, you can catch the admin's note before it disappears.

Now let's automate the attack so you don't miss it.


so the way out is to check the request and response of the web application after every one two minute for some flag or hash 

it might come in sometime so first way is to use console in inspect of the google 

using script

`setInterval(() => {
  location.reload();
}, 2000); // Refresh every 2 seconds`

but I think there is some problem coming up with this way as it should keep on giving output to me but it is refreshing completely after 2 sec and giving no output at all


this aint working I think as there has to be some hash or flag as output but it aint returning anything like that so I think I have to proceed with some other way out I checked all files in it and it stated that answer will be in note feature only 


Insecure temporary storage (like memory-based cache, Redis, or in-memory objects)

Note access via ID or secret token

Unprotected admin panels

XSS (Cross-site scripting — very common in note-taking apps)

SSTI (Server-side template injection)

IDOR (Insecure direct object reference, if there are note IDs or URLs)

so i found there is a /report page that allow xxs scripting or stuff in it so i dont know much xss but i will try to find flag anyway possible 


