# Windows Forensics Investigation: Manual Analysis of a Compromised System

## Room Information
**Room:** Investigating Windows  
**About the room:** A windows machine has been hacked, its your job to go investigate this windows machine and find clues to what the hacker might have done.

## Initial Setup
For performing this room I initially planned to use Autopsy and tried downloading it on my Kali Linux virtual box but it showed a lot of error so I downloaded autopsy on my own windows as I read it is more smooth on windows. However, for this investigation I ended up using native Windows tools and commands for manual forensic analysis.

## Tools Used
- Windows Command Line (net commands)
- Task Scheduler
- Event Viewer
- Windows Firewall with Advanced Security
- File System Analysis

## Investigation Process

### Step 1: Joining the Room
So first I joined into a windows using remote desktop resulting in entering a already hacked machine. I need to find the malicious person log and identify what he find out.

### Step 2: User Analysis
So I used command:
- `net user administrator`: to find who logged in last time 
- `net user <username>`: to find the details about user who logged in last time

As in my case here it was john who logged in using this command I was able to find last time he logged into the system.

- `net localgroup administrators`: to find the users who have administrative privileges 

### Step 3: Finding Malicious Tasks
Next we have to find the task that is malicious so for that u can open task scheduler and check all tasks and the one that is odd or u think is doubtful is the malicious one.

Next we have to find what file it is running for that go to action section after clicking on that task which will tell u the file name and port name both usually important to know.

### Step 4: Identifying Compromise Date
Next I have to identify when the compromise happened so for that I checked any unknown file in device and check for its date of download or use that is our compromise take place date.

### Step 5: Finding Special Privilege Assignment
Next I have to find when the windows first assign special privilege to a new login so for that go to:
**Event viewer -> windows logs -> security**

Then check each access provided and check for the one that provides special logon. Check the date and time and that is the required answer.

### Step 6: Identifying Attack Tools
So next we have to find the tool used for gaining windows password so check the file for any executable python script try to run it if it runs check the tool name or if u have idea about the tool u got it.

### Step 7: Finding External Control and Command Servers
Next we need to find the attackers external control and common servers IP address so for this u go to:
**Local disk -> windows -> system32 -> drivers -> etc -> hosts**

Inside the folder check for the website which u think is not right like in this room we know google.com is hosted on 10.10.0.1 or something unique but here the ip is 76.32.97.132 which is clearly dns poisoning of google.com.

So ya check for that.

### Step 8: Identifying Last Opened Port
Next we need to check which port was last opened by the attacker so for that u assume that the last thing did by attacker was their and u haven't opened any port yourself so for that go to firewall and when u see firewall open there u can see the last runned task and what port it worked on that your answer go for it see it.

For checking which port go to:
**Windows firewall with advanced security -> inbound rules ->**

Here see the last run task and see the port used.

## Conclusion
That the end of the room this room doesn't have any single walkthrough so it was very very tough for me as I dont know a little even of steps and they didn't provided any walkthrough for it.
