# CS428-ComputerSecurity-Labs
# Computer Security Labs

A collection of three hands-on labs exploring memory-corruption vulnerabilities, exploitation techniques, and the web's trust infrastructure.

## Labs

### 1. Buffer Overflow Vulnerability Lab
Explored the fundamentals of buffer-overflow exploitation on a 32-bit Linux system. Located and overwrote return addresses to hijack control flow and run arbitrary shellcode, adapted payloads to work with unknown/varying buffer sizes, defeated Address Space Layout Randomization (ASLR) via brute force, and evaluated StackGuard as a defense against stack-smashing attacks.

**Key tools/concepts:** return address overwriting, shellcode injection, ASLR, StackGuard, brute-forcing memory addresses

### 2. Return-to-libc Attack Lab
Built a return-to-libc attack against a vulnerable Set-UID program to bypass non-executable stack protections. Used GDB to locate `system()` and `exit()` in libc, staged `/bin/sh` in memory via environment variables, automated exploit construction in Python, and worked around shell-level countermeasures after gaining a shell.

**Key tools/concepts:** GDB, libc function addresses, non-executable stack bypass, exploit automation with Python

### 3. PKI and HTTPS Lab
Simulated a Man-in-the-Middle (MITM) attack to study how HTTPS and Public Key Infrastructure (PKI) defend against it. Generated and validated SSL/TLS certificates, configured Apache with custom certificates, spoofed DNS to intercept traffic, and tested client certificate validation across trusted, mismatched, and untrusted-CA scenarios before cleaning up the attack environment.

**Key tools/concepts:** openssl, curl, Apache/HTTPS configuration, DNS spoofing, certificate authority trust chains

## Common Thread

All three labs sit under the same broader theme: how software vulnerabilities and trust assumptions can be exploited to violate a system's intended security guarantees, and what defenses exist (or don't) to stop that. The first two labs focus on memory-corruption attacks at the binary/OS level; the third shifts to the network/application layer, examining how trust is established (and can be subverted) between clients and servers.

## Repository Structure

Each lab has its own detailed README with task-by-task breakdowns, key takeaways, and the original report abstract:

- `buffer-overflow-lab/README.md`
- `return-to-libc-lab/README.md`
- `pki-https-lab/README.md`
