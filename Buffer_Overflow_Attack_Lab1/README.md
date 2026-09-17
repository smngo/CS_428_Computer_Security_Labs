# Buffer Overflow Vulnerability Lab

## Overview

This lab explores buffer-overflow vulnerabilities on a 32-bit Linux system, along with the defenses designed to prevent them. The goal was to move beyond theory and gain hands-on experience exploiting a vulnerable program to gain root privileges, then evaluate how well different protection schemes (address randomization, StackGuard) hold up against that exploit.

## Learning Objective

Buffer overflow occurs when a program writes data past the boundary of a fixed-length buffer. Because data storage (buffers) and control storage (like return addresses) often sit close together in memory, an overflow in the data can corrupt the control flow of the program — potentially letting an attacker redirect execution to arbitrary code. This lab's objective was to understand that mechanism first-hand by exploiting it directly, then to test the mitigations Linux provides against it.

## Environment

- 32-bit Linux system
- Set of intentionally vulnerable applications

## What I Did

### Tasks 1–4: Basic Buffer Overflow Exploits
Worked through the fundamentals of exploiting a buffer overflow:
- Located the return address on the stack and overwrote it to redirect execution.
- Crafted and injected shellcode to run arbitrary commands.
- Adapted the exploit payload to work under tighter constraints, including varying buffer sizes.
- In Task 4 specifically, refined the approach to succeed without knowing the exact buffer size in advance, minimizing reliance on trial and error.

### Task 8: Defeating Address Randomization
Investigated Address Space Layout Randomization (ASLR) as a defense mechanism, then used a brute-force approach to guess the correct stack address and successfully execute the exploit despite randomization.

### Task 9: StackGuard
Examined StackGuard's stack-canary approach to detecting buffer overflows before a corrupted return address can be used, and evaluated its effectiveness at stopping the earlier attacks.

## Key Takeaways

- A buffer overflow can be leveraged to hijack a program's control flow and execute arbitrary code, including gaining elevated privileges.
- Precise knowledge of memory layout (buffer size, return address location) makes exploitation easier, but exploits can be adapted to work with imperfect information.
- ASLR raises the bar against exploitation but isn't foolproof — it can be defeated through brute-force techniques given a small enough search space.
- StackGuard-style stack canaries provide a meaningful, distinct layer of defense compared to address randomization, and materially reduce the reliability of naive buffer overflow attacks.

## Abstract

> I discuss randomization, buffer overflow vulnerabilities, and the efficacy of different solutions in thwarting such assaults. Using a 32-bit Linux system and a number of susceptible apps, the lab's objectives were to interact with security features like StackGuard and handle randomization while taking advantage of buffer overflow flaws. I studied simple buffer overflow vulnerabilities in Tasks 1-4, where I discovered how to locate and replace return addresses to run arbitrary shellcode. I improved my strategy by modifying the payload to operate under restrictions, including different buffer sizes in Task 4, where I had to minimize trial and error tries and operate without knowing the precise buffer size. Task 8 focused on defeating address randomization, where I utilized brute-force methods to identify the correct stack address in the presence of address space layout randomization (ASLR). In Task 9, I examined the role of StackGuard in defending against buffer overflow attacks.
