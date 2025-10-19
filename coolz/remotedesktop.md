# Using RDP to Gain Windows Access and FreeRDP Tool

so i decided to cover some cool things before changing my other laptop from windows to linux only operating system so i decided to do certain task one of it is gaining access to desktop view like either gaining access to his screen or his whole device using certain steps to find a way to get screen access that we see in series  
and actually its quite easy u can scan your nearby network or larger number of device if u just have proper high power device to brute force thing.

- u can scan for open ports of a device with its ip  
- u can brute force his username and password  
- using powerful tools like hydra to find his id and pass  
- once u have the device id pass and ip u can actually one way or other get a person’s device full access  
both from nearby as well as far away  
nearby by manually entering that password in his laptop  
faraway by using his ip or one of many way to get windows access using winrm, rdp, vnc server and ssh ports  

but this is not where my thinking is going rn i want to somehow keep a gateway open on a device so that i anytime i want to see what someone is doing on my device or his device i can simply enter device ip id pass and get to see what he doing  
something like spy work  
and thats what i will be trying to learn and do  

this one is for using remote desktop and freerdp tool  

## Step 1: Find Target Windows Laptop IP

- open cmd  
- write `ipconfig`  
- look for ipv4 address  
- note the ip target down somewhere safe  

## Step 2: Enable Remote Desktop on Windows

=> on windows laptop  
- press windows+I to open setting  
- go to system -> remote desktop  
- enable remote desktop  
- allow it through firewall if asked  

=> Note target windows Username  
  username: RAJA  
=> Make sure u know the password for that account  
  password: pass  
  note: right now i dont know how to crack password so for now i will be using already know password of device but u can brute force the password using tools like hydra or hashcat and get access to device  

## Step 3: Install RDP Client on Kali

```bash
sudo apt update
sudo apt install freerdp2-x11 -y
```

FreeRDP is an open-source command-line tool to connect to Windows machines via RDP. It’s used for remote desktop access, supports multiple auth methods, and is popular with sysadmins and pentesters for testing RDP security

<img width="1600" height="249" alt="image" src="https://github.com/user-attachments/assets/27c8d37a-c6f2-4dcb-81c2-086de4c307f4" />

## Step 4: Connect from Kali to Windows in Kali Terminal

for this u need freerdp version downloaded in kali and target’s ip address with his device id and pass

```
xfreerdp /u:<username> /p:<password> /v:<ip_address>
```

this is the basic command to connect to rdp using kali directly  
u can also use more syntax to improve the speed and view of screen  

```
xfreerdp /u:<username> /p:<password> /v:<ip_address> /f /cert:ignore
```
<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/41abffc8-c0e6-4dc2-9f86-b0be71f74cc9" />

this will ignore all the certification required to enter the rdp and also allows u to view a fullscreen view on your terminal  
note: while u are signed in as or enter this command the actual user will be kicked out or signed out and u will get complete access to his system until he signs back in  
so its not like u just watching his screen or something its basically u have whole access to his system  

next target: have to find a way to just view his screen while he is allowed to do whatever he do and this i have to setup as a backgate so anytime i want to see what that specific person is doing i can just enter his ip and stuff and boom i will be in...


