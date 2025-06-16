# OSINT Aggregation Project

## Project Overview
So I am going to build a project which uses already built-in tools like Sherlock, Harvester, Maigret, and other tools to provide an interface that gives users the choice to scan publicly available info directly without scanning for different tools at different places. 

They just choose what they want to provide as input, enter the details, and my project will return all the data it can find about that.

## Available Scan Options
- **Username**
- **Email address** 
- **Photo**
- **Phone number**
- **Domain**

After choosing, they will give details and get a detailed report for it.

## Tool Analysis & Strategy

### Username Scanning Approach
So for username, there are a lot of tools, but from my own experience, Sherlock works really well, but it scans only 300+ websites, so it doesn't provide results for a lot of websites. 

Here comes the role of Maigret - it scans around 1500+ websites and returns all the data it can find about that person, but it is not that accurate as it just sends your username and if it returns without a 404 error, it says that the username exists, but it is sometimes not right.

### Initial Strategy (Modified)
**Original Idea:**
I was thinking to first let Maigret scan for the username provided by the user, then when we get active users or successfully returned results, we can send them to Sherlock to scan if the user actually exists or not.

**Current Approach:**
But this is something not possible right now, so for now I will just run both tools and provide a summary of both and write a script for it. 

Similarly, I will use one or two good tools for each option, create a summary of them, and return to the user, providing a more accurate summary for the user.

## Environment Setup Challenges

### Initial Setup Requirements
So first I will check the requirements of Sherlock and Maigret to run, as last time when I used these tools they required environment variables to run venv.

Yeah, I was right - for running these tools I need an environment activated. For that, I am leaving the code here too.

**Basic Virtual Environment Setup:**
```bash
# Create virtual environment
python3 -m venv venv

# Activate the environment  
source venv/bin/activate

# Check if activated (you should see this prompt)
(venv) your-computer:your-project$
```

After doing this, you have to download the tool inside the venv.

### Python Version Compatibility Issues
Lol, this is some error I see very rarely - I have Python version 3.13 which is a more advanced version and doesn't support a lot of tools, so I have to download an old version of Python which is more compatible.

## Python 3.11 Installation Guide

### Method 1: Package Manager Installation
✅ **Step-by-step to install Python 3.11 on Kali Linux and fix everything**

**1. Install Python 3.11 and required packages**
```bash
sudo apt update
sudo apt install python3.11 python3.11-venv python3.11-dev -y
```

**2. Verify installation**
```bash
python3.11 --version
```
You should see something like:
```
Python 3.11.x
```

**3. Create environment with Python 3.11**
```bash
python3.11 -m venv osint-env
source osint-env/bin/activate
```
You should now see `(osint-env)` in your terminal prompt.

**4. Install tools cleanly**
```bash
pip install --upgrade pip
pip install maigret
```
🎯 Now arabic-reshaper, aiohttp, and all other dependencies will install without error.

### Method 2: Manual Installation (When Repos Don't Have Python 3.11)
As Kali doesn't usually have old repos in them, so I can't just download Python 3.11 directly, so I will have to download it manually and download its dependencies manually.

So for that, I used a written script.

### Custom Python 3.11 Build Script
**install_python3_11.sh — Minimal & Safe**

```bash
#!/bin/bash

set -e

echo "[*] Installing dependencies for building Python..."
sudo apt update && sudo apt install -y \
    wget build-essential zlib1g-dev libncurses5-dev \
    libgdbm-dev libnss3-dev libssl-dev libreadline-dev \
    libffi-dev libsqlite3-dev libbz2-dev liblzma-dev \
    uuid-dev tk-dev libdb-dev

echo "[*] Downloading Python 3.11.9 source code..."
cd /tmp
wget https://www.python.org/ftp/python/3.11.9/Python-3.11.9.tgz
tar -xf Python-3.11.9.tgz
cd Python-3.11.9

echo "[*] Configuring Python 3.11..."
./configure --enable-optimizations

echo "[*] Compiling Python 3.11 (this may take a few minutes)..."
make -j$(nproc)

echo "[*] Installing Python 3.11 safely with 'altinstall'..."
sudo make altinstall

echo "[✔] Python 3.11.9 installed successfully!"
echo "[✔] Run 'python3.11 --version' to verify."
```

**📝 Important Notes:**
- This installs Python 3.11 alongside your system Python (3.13 remains untouched)
- Use `python3.11` to run the new version
- Safe for Kali and VirtualBox

**⚡ How to Execute:**

1. **Save the script:**
```bash
nano install_python3_11.sh
# Paste script, save with Ctrl+O, Enter, exit with Ctrl+X
```

2. **Make it executable:**
```bash
chmod +x install_python3_11.sh
```

3. **Run it:**
```bash
./install_python3_11.sh
```

## Integration Challenges & Solutions

### Setup Requirements
So there will be a problem if you try to run all these tools without setting up Python 3.11 version, and also you have to set up environment variables for it too.

After downloading Python 3.11, remember to download tools in the same directory so you can write a script that will run the whole code in the same place.

### Reality Check: Tool Complexity
Man, this is kind of tough - every tool requires different setup and has different working methods. Somehow I managed to install all of them.

But now while running, it is taking a lot of time. I think these tools are built to run individually, but here I am trying to make them run together and provide results, which is time-taking and tough.

### Current Implementation Status
So as of right now, I wrote a script for downloading Python 3.11, also set up environment and folder to set up the needed requirements.

After that, I have to install all the tools in the same directory so I can use them together. For that too, I wrote a script which:
- Checks first if the tool is installed
- If it is installed, checks if it has all its needed requirements
- If not, downloads missing requirements
- If tool isn't downloaded at all, starts cloning and setup from beginning

### Tool Execution Format Fix
After all this, I have one more fix to correct - as most of the tools require to be run by Python, so I have to edit the usage format.

**New execution format:**
```bash
python3 -m sherlock_project damnkrishna
```

## Project Pivot: From Integration to Modular Approach

### Initial Approach Problems
So this project just got compromised as it was becoming way too complex to solve all the problems that are not mine, as all tools use different setups, so running them together is not something I am showcasing in my project. 

I want to showcase my knowledge about OSINT.

### New Strategy: Modular Tool Execution
So now I will build a project, and this time I will keep all tools in different boxes and edit their reports to give me data about them individually and not all at once.

## Phase 1: Success! 🎉

### Current Working Implementation
It worked! I cloned tools inside the tools folder in my directory and made a script that runs different tools based upon the user input:

- **Phone number input** → Runs PhoneInfoga
- **Email input** → Uses different email OSINT tool  
- **Username input** → Runs Sherlock/Maigret individually
- **Domain input** → Uses domain reconnaissance tools

Each tool returns its output independently, providing clean, focused results.

### Project Phases

**Phase 1 (Current):** ✅ **Completed**
- Modular tool execution based on input type
- Individual tool reports
- Clean separation of concerns
- Working proof of concept

**Phase 2 (Upcoming):** 🚀 **Planned**
- Provide summary of found information
- Identify security level of the tools
- Enhanced reporting and analysis
- Data correlation across tools



##Projectlink
https://github.com/damnkrishna/DataHawk-
