# Return-to-libc Attack Lab

## Overview

This lab investigates the return-to-libc attack, a technique for exploiting buffer-overflow vulnerabilities that bypasses the non-executable stack protection found in operating systems like Fedora Linux. Rather than injecting and jumping to shellcode on the stack, this attack redirects execution to existing code already loaded in memory, specifically functions inside the libc library; making it effective even when the stack itself cannot execute code.

## Learning Objective

A standard buffer-overflow exploit overflows a buffer with malicious shellcode and hijacks the return address to jump into that shellcode on the stack. Marking the stack non-executable defeats this by causing any jump into it to fail. However, this protection isn't foolproof: a return-to-libc attack sidesteps it entirely by redirecting the vulnerable program's control flow to legitimate, already-loaded library code (such as `system()`) instead of injected shellcode. The objective of this lab was to build such an attack against a vulnerable Set-UID program to gain root privileges, and then evaluate how well Linux's various protection schemes actually hold up against it.

## Environment

- Linux system with a Set-UID vulnerable program (`retlib`)
- GNU Debugger (GDB)
- Python (for exploit automation)

## What I Did

### Task 1: Locating libc Function Addresses
Used GDB to debug the Set-UID `retlib` program and determine the memory addresses of the libc functions `system()` and `exit()`, which would serve as the targets for the hijacked return address.

### Task 2: Preparing the Shell String
Used environment variables to place the string `/bin/sh` into memory, then determined its address so it could be passed as an argument to `system()` — enabling the exploit to spawn a shell rather than execute injected shellcode.

### Task 3: Automating the Exploit
Wrote a Python script to automate construction of the malicious input (`badfile`), assembling the correct sequence of memory addresses and function calls needed to overwrite the return address and trigger `system("/bin/sh")`.

### Task 4: Bypassing Shell Countermeasures
Even after successfully spawning a shell connected to `/bin/sh`, worked around additional shell-level countermeasures designed to prevent the elevated shell from being abused, completing the final stage of the attack.

## Key Takeaways

- A non-executable stack blocks classic shellcode-injection attacks but does not prevent control-flow hijacking in general — return-to-libc attacks achieve the same outcome using code that's already loaded in memory.
- Precise knowledge of memory addresses (for both library functions and injected strings like `/bin/sh`) is central to building a working exploit, and tools like GDB make that reconnaissance possible.
- Exploit construction can be automated once the required addresses and calling conventions are known, turning a manual process into a repeatable script.
- Even after gaining a shell, additional defenses can restrict what an attacker can do with it, requiring further steps to fully bypass protections.

## Abstract

> Using the retlib program, I investigate and put into practice a number of return-to-libc attacks that alter memory, issue commands, and increase privileges. Each of the four tasks in the lab focuses on a distinct facet of the attack. First, I debug the Set-UID retlib program using the GNU Debugger (GDB) to determine the memory locations of the libc functions system() and exit(). I then use environment variables to load the shell text (/bin/sh) into memory and determine its address to send to system(). Next, I use Python to automate the process by creating a malicious input file (badfile) with the required memory addresses and function calls. Even with /bin/sh connected to a shell, I get around shell countermeasures in the last job by using execv() to escalate privileges and obtain a root shell.
