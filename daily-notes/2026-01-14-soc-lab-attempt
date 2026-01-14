# Building a SOC Home Lab: Initial Attempt and Learnings

## Project Clarification

well I am gonna build my own soc home lab using splunk or siem tools to build a lab at home though I am little confused on what exactly am I building here so first I wil clarify that the purpose of this project 

well I used to think one person is there for each company observing its log one by one but I forgot no one can do that it is all automatic and only when something bad happens on a system then alert arises and engineer got to know that something is wrong then they start analysing the problem and finding solution but if something doesn't give any alert on siem tool than no one in this world will know that they are under attack 

well thats okay but what will be the workflow for the project 

like am i gonna download a siem tool like splunk then on the same device or localhost i will send attack both normal and malicious and that attack will be analyzed by my siem setup and give me alert then i will analyze it and create report and also there will be a dashboard 

but if this is it isnt it like log analyzer project whats different in this

well at last everything is a log but deciding and observing pattern is what makes it different from simple log analyzer project to soc project 

## Implementation Process

### Task 1: Initial Wazuh Setup

so here starts the real work 

install wazuh store its login credential and set up login and free some space 

a little fuck up happened my laptop is down the process stopped cause of download wait or something I am starting it again but letts see if it restarts on its own or I will have to do something 

### Technical Challenges Encountered

well seems like wazuh is a tool usually used on red hat or centos or some other os cause it is not allowed in this particular os and I have to force install it that's why it is giving a lot of problem actually like a ton of problems 

well I guess it is not working have to go some other way using vm like ubuntu I guess I am not in mood to do that just now 

well i am back so wazuh wont wont work in kali Linux os as kali is for attack and stuff but for hosting a siem tool like wazuh which is supported by ubuntu and other server 

### Alternative Approach: VirtualBox Setup

so now i am going to use virtual box and creating a ubuntu os and setting up my siem tool there are will use kali Linux for attacking and network and will create dashboard on virtual box or siem tool on virtual box and for that i wanna setup a command that will run whole siem tool in one go for my house network and stuff 

using wireshark and dashboard but this will be future scope for rn i will doing only between two host one my laptop and one my vm inside the same laptop so it is more like localhost so for future scope i will try to control my home network 

### VirtualBox Configuration Issues

well this setup is quite lengthy i got to know thinkpad kali Linux os bios has set virtualization to disabled thats why i was facing so much problem and error 

but now i have enabled virtualization might it be done now 

fuck now it is showing some download error first i thought it was again bios setup error that secure boot was closed but no the download had some error some file is probably missing 

so have to download some modules of virtualbox again 

lets do it 

well i had to delete all and everything related to virtual box and download everytool and everything again 

well now without chatgpt i dont even know how would i fix this problem on my own 

### Hardware Limitations

well wazuh is not working on my laptop maybe cause of storage problem and also cause my laptop cant handle that much pressure my whole mouse keypad and screen got hanged cant do anything 

### Pivot to Elastic Stack

so now i will shift to elastic i know it is not that big or professional but for a beginner soc it is fine 

so now will go with ubuntu server VM 

elastic stack minimal 

dashobarod and basic detection 

here we go again but first i have to remove everything related to wazuh from my vm it might be taking too much space cause either i can create new vm or use already build one so lets see 

## Current Status and Next Steps

This initial attempt to build a SOC home lab encountered several significant technical constraints, primarily related to hardware limitations and OS compatibility issues. The experience highlighted the resource-intensive nature of SIEM tools like Wazuh and the importance of proper system configuration for virtualization.

### Lessons Learned:
- Kali Linux is optimized for offensive security operations, not for hosting SIEM infrastructure
- Wazuh requires substantial system resources and is better suited for enterprise-grade hardware
- BIOS-level virtualization settings can create unexpected deployment barriers
- Tool compatibility and system requirements must be thoroughly validated before implementation

### Future Roadmap:
Due to current hardware constraints, this project will be revisited with either upgraded hardware specifications or alternative lightweight SIEM solutions such as Elastic Stack. The methodology and troubleshooting process documented here will serve as a foundation for future implementation attempts with optimized system configurations.
