# Fundamentals of Reverse Engineering

Reverse Engineering (RE) is the process of deconstructing a compiled program to understand its internal logic, flow, and data structures. It is a critical skill in malware analysis, vulnerability research, and software auditing.

## 1. The Core Pre-requisites
To be effective in RE, you need to move beyond high-level programming and understand how the computer executes instructions at the hardware level.

* **Assembly Language (x86/x64/ARM):** Programs are eventually converted into machine code. Assembly is the human-readable version of that code.
* **Computer Architecture:** You must understand how the CPU, Registers (EAX, EBX, etc.), and Memory (Stack vs. Heap) interact.
* **Operating System Internals:** Knowledge of how Windows (PE) or Linux (ELF) files are loaded into memory is vital.

## 2. Hexadecimal and ASCII: The "Language" of Binaries
Your friend suggested learning Hexadecimal to ASCII conversion because binaries are viewed in **Hex Editors**. 

### What is Hexadecimal (Base-16)?
Computers use Binary (0s and 1s), but Binary is too long for humans to read. Hexadecimal is a shorthand. 
* One "Byte" of data consists of 8 bits.
* In Hex, one Byte is represented by exactly **two characters** (e.g., `4A`).
* Hex range: `0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F`.

### What is ASCII?
ASCII is a standard that maps numerical values to characters. Every letter on your keyboard has a corresponding number. 
* For example, the letter **'A'** is represented by the decimal number **65**, which is **0x41** in Hexadecimal.

### Why Conversion Matters
In RE, you will often see a string of Hex values. If you can't recognize them as ASCII, you will miss vital clues like hardcoded passwords, IP addresses, or file paths.

**Example Conversion:**
Hex String: `53 65 63 75 72 65`

1.  `53` -> **S**
2.  `65` -> **e**
3.  `63` -> **c**
4.  `75` -> **u**
5.  `72` -> **r**
6.  `65` -> **e**
**Result:** "Secure"

## 3. Recommended Tools for Beginners
1.  **Ghidra:** A free, open-source software reverse engineering suite (developed by the NSA). It includes a "Decompiler" that turns Assembly back into C-like code.
2.  **x64dbg / GDB:** Debuggers used to watch a program run in real-time, instruction by instruction.
3.  **HnD (Hex Editor):** A tool to view the raw bytes of a file.

## 4. Next Steps
* **Practice Hex Math:** Learn to add and subtract small hex values.
* **Read C Code:** Understand how variables and functions look in source code so you can recognize them in Assembly.
* **Start with 'Crackmes':** Look for beginner-level reverse engineering challenges online.
