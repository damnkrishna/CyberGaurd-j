so i am trying to solve this port swigger room 
i have some hints to solve the issue 
i manually tried to solve the room but i cant 
can u help me out a little
as the cookie 
has some way to get access to the database and have to get out the administrator password 
and it is not that tough 
As cause we kind of know the hint 
i know i should be able to manually 
do it nut i cant 
So here i am asking for help help me out a little 
Will u 
i am gonna share the room 
and exact cookie that i saw that has been being used


Lab: Blind SQL injection with conditional errors
PRACTITIONER
LABNot solved











This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user.
 Hint
This lab uses an Oracle database. For more information, see the SQL injection cheat sheet.
ACCESS THE LAB
 Solution







Cookie: TrackingId=bgL0TNQcHbUbpoEl; session=OJyMKFgDnQIjKNyiprdZYlrjn2d6I0es


so if possible give me the manual how to see this myself before running the sql map and how i will test it myself

i did that room yesterday finally

<img width="959" height="431" alt="Screenshot 2026-09-05 104257" src="https://github.com/user-attachments/assets/092a0048-fda5-489a-a3a8-abad71bf5172" />





doing a new room 
blind sql injection with time delay
 and it seems the category is priniting  input in output but i think might not be touching the database 
 but lets see what we can do 
 
<img width="809" height="382" alt="image" src="https://github.com/user-attachments/assets/ea693c9c-2f26-4aa3-abc8-56b2cf48c55c" />



i didnt used sqlmap 
cause sqlmap was not able to solve that room 
so i have to manually and using burp intruder find the password for the administrator account it was tough 
As the commands i had to use to solve the room i was not aware about that 
but it seems sql injection is not as tough as i used to think it was 
