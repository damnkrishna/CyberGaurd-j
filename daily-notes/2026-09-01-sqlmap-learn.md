## my goal for tommorrow is solely to use and learn sql map to learn how to use burp request post or paramter and response and how to test it if it is a true vulneraibility or not 
from sqlmap tool

and tomorrow the sole goal is this and this only


i am feeling way too low today i am feeling like a dead body how cant even move 
i know i have a call and maybe today or tomrrow and cause of that i am not sure whether i am saving my energy or just lazy i am feeling like watching a good series not gonna lie
i feel like just chilling watching a series and do nothing type feel this has been coming a lot lately maybe i am recovering and it is normal but i need to study as well so for today i am just gonna do a little of regular daily streak maintaince just that and no extra


have done no shit till now 
yesterday too i just had a resume review and a bangalore based security expert told me that my resume can get me 10 lpa+ job as i wish 
if i keep applying and stay consistent it wont be a issue
i will really be able to secure a job 


just keep patience and keep applying 
and everythign will be fine 



well my cousin is coming one today and one tomorrow it seems that 
i am the type of guy who actually performs more when people are around 
maybe to show off or maybe cause i am restricted to my desk than if guest are at home whatever the thing is

when relatives are at home 
i seem to study for more hours and get more study hours out of my day to day schedule 
i know it looks like i perform only when people are watching or making me a performative male 
but whatever suits the purpose of me studying
i dont care about the reason behind it as long as i am studying 


i will clear that sql injection room for sure i can say that for sure 



well so lets go 
i am going to start with the blind sql injection with conditional response room

as for the starting i will start with 
opening burp and opening the room with connection to burp proxy 

and next start active scan as i have already tried this room once so i know 
after 
burp suite actively scan this host it will give some sql injection relation response vulnerability when in the true condition it is giving different response while in false it is giving different type of response so we are going to test just that
at first 

first i manually confirm this vulnerability by trying to put a true and a false statement i will first test the result myself then will start with tool usage 
So lets go 


<img width="959" height="430" alt="image" src="https://github.com/user-attachments/assets/f7954ab4-10d4-4a04-9d93-4e3d0453d61d" />


solved my first room letsgo 



just to remeber the command i runned

└─$ sqlmap -r newinjection.txt --force-ssl -p TrackingId --level=2 --technique=B --prefix="'" -T users -C username,password --dump --batch


