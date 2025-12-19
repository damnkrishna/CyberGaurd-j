# Memory Analysis Introduction

You must have heard that when someone's laptop or computer is picked up for artifacts or investigation, they quickly try to recover as much data as possible. This is because the data in a laptop is divided into multiple levels:

- **CPU Registers** - Fastest, smallest storage
- **Cache** - Very fast, small storage
- **RAM** - Fast, volatile memory
- **Disk Storage** - Slowest, permanent storage

The fastest is CPU register but with least memory, and all the data that is present in RAM or above level gets deleted the second the laptop is closed. But that is not the case with disk storage because it is permanent memory that never gets deleted until deleted on purpose. Hence, RAM is usually targeted first during investigation of laptop cause data will be lost in it very quickly.

---

## RAM Structure

RAM has two parts:

### 1. User Space
Contains processes and functions that user does or uses:

- **Stack**: Stores function arguments and return address => shell command
- **Heap**: Dynamically memory allocation is done here, stores encryption keys, credentials, etc.
- **Executable**: Actual code or instructions to run
- **Data Section**: Stores global variables or variables for executable

### 2. Kernel Space (OS)
Operating system kernel space that manages system-level operations.

### Swap
Disk-based area that temporarily stores RAM data when memory is full. Also a source to be checked when you want additional data, might be there in swap.

---

## Memory Dump

Snapshots of system's RAM at a specific time:

- **Full Memory Dump** - Complete capture of all RAM contents
- **Process Dump** - Capture of specific process memory
- **Pagefile or Swap Analysis** - Analysis of disk-based virtual memory

---

## Ways to Find Data

### In Windows

- **Tool**: RAMMap
- **File**: `hiberfil.sys` (hibernation file containing RAM snapshot)

### In Linux and macOS

- **Tool**: LiME (Linux Memory Extractor)
- **File**: `/dev/mem` (physical memory access)
- **File**: `/proc/kcore` (kernel core dump)

---

## Additional Tools

### Note: Mimikatz Tool

When used with WinDbg extension (also called `mimilib.dll`), can be very useful in finding data such as:
- Passwords and credentials
- Kerberos tickets
- Authentication tokens
- Other sensitive information stored in memory

---

## Investigation Priority

Remember: **RAM-based evidence is volatile and must be collected first before powering down the system**, as all data in RAM will be lost once the system is shut down. Disk storage can be analyzed afterwards as it persists even when powered off.
