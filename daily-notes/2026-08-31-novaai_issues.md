so the website is not responsive the after creating new account when we fill more personal info 
the values gets cut off and words shrink out 
<img width="959" height="423" alt="image" src="https://github.com/user-attachments/assets/eb2a7e4f-5cea-43dd-a097-7aec01c94afd" />
this is what is visible when we zoom in a little 


and this is what it should have shown 
<img width="952" height="416" alt="image" src="https://github.com/user-attachments/assets/39c9edb4-442c-40f0-bd30-f02488a3d0f6" />
when it is at 80% zoom it is working perfectly when we zoom to 90-100% or more values gets cut out 




it is a very visionary thing 
basically the company is trying to build a whole security company that is completely automated
all the department all the services which a general security company gives to their customers 
they are trying to give it though one platform and one platform 
idea is visionary but have to get inside how it is handling its day to day task issue which arises and how exactly 


they are handlign those specific task like vapt 
24*7 soc 

cause ai is not that advance that it can think about the ideas that human can find in a any website by manual testing and ik 
that most of people dont even do these vapt work that seriously cause i have seen in my intern at c3ihub they are doing website testing and providing full report on how their website security posture is how secure their website is performaing vulnerbaility testing and also recommending suggestion to fix it 

and also a dedicated platform which provided 24*7 soc service to goverment companies and even for indian ports and nhai 
higways of india

so ik i have seen the work happening there 
and building a project that works upon removing all those human interaction and automating it is actually visionary idea 
with the growing power of ai it is possible one day but for now i want to see how exactly they are handlng all those thing on surface level what that ai will do when we put our company website and it do vapt or pentest on it 



<img width="959" height="416" alt="image" src="https://github.com/user-attachments/assets/d4c64541-a62e-47c6-9844-32a568d83470" />



this brand protection feature i am not sure what it is about i think it is something related to if someone want to keep any eye on any specific brand of their own 
like a instagram handle or youtube channel it even provides a platform to protect that form one place as well


<img width="959" height="413" alt="image" src="https://github.com/user-attachments/assets/fff00063-9727-4d93-af11-2d641212b196" />

even have a user role management thing
so security wise role based access control or something might be assigned for level of privilege and secuirty 
<img width="959" height="413" alt="image" src="https://github.com/user-attachments/assets/db261f20-be26-47a6-85ae-746a1595f6b9" />



wow the website is working really well like not gonna lie 
the basic recon on all the platform it did so well it found all the error 
of basic nmap and active scan from burpsuite 
and even did proper dark web searching itself 
and the best part it provided all the data in downloadable form i know it is risky but it worked and that too super fast like it took less than 1 min to run this 
i dont know maybe even less


<img width="959" height="415" alt="image" src="https://github.com/user-attachments/assets/81044901-3d09-48ab-9a1c-3ebac9e6b781" />


regarding other feature i think those are paid 
so far so good 
it was able to do proper active recon well
found everything 
it is like a good automated script that is running properly and providing data in the best posibile format and that too very quick

it was able to do full recon on my college email and found each and everything about it
Great work 
i do still have a doubt as my college is normal but if like it did recon this fast
it might have performed nmap of active scan on the back 
so wont it be triggered or the ip dropped when this type of scan thing we try to do on some website with good security posture and stuff
well it is stupid question to ask i know that 
but its fine 
the people working upon all this are way ahead of me 
atleast what i saw was a fast working recon that too was actually giiving me dark web data and not just blurring it out like virustotal and other open soruce website its good but dangerous as well

<img width="603" height="326" alt="image" src="https://github.com/user-attachments/assets/4d8cc962-3c36-42ac-8337-8c6dca2684df" />



## That's the real finding here, and it's a bigger deal than the zoom bug.

Think about what actually happened: you signed up with a personal college email address, and the platform inferred your institution's domain and then ran active scanning and dark web correlation against that institution's entire infrastructure — including pulling exposed credentials belonging to your professors, who never signed up for anything and never consented to any of this. There was no step where anyone checked "does this person have authorization to test this organization," no domain-ownership verification (like a DNS TXT record challenge or an email-to-a-registered-admin-address flow), nothing. Your college email just being @college.edu was treated as sufficient proof you're allowed to pentest the whole college.

That's a genuine authorization/access-control flaw in the platform itself, and it's arguably worse than most bugs you'd find in a VAPT engagement, because:

- It's giving away other people's PII by default. Your professors' exposed dark-web credentials are personal data about third parties who have no relationship with this platform. Handing that to any random student who signs up is a real privacy failure, not just a "cool but risky" feature.
- It puts users in legal jeopardy without them realizing it. In a real engagement, the client has to sign a scope/authorization document before anyone touches their infrastructure — precisely because running scans against a domain you don't own or have written permission to test can fall under unauthorized access provisions (IT Act in India, similar laws elsewhere). By letting you trigger this with zero verification, the platform effectively let you do something that could be legally questionable, without ever telling you that.
- It undercuts their whole pitch. A platform selling itself as replacing professional security services just skipped the single most basic thing every real security firm does first — confirming engagement scope and authorization — before firing off scans.
