# PKI and HTTPS Lab: Simulated Man-in-the-Middle Attack

## Overview

This lab explores HTTPS and Public Key Infrastructure (PKI) by building a simulated Man-in-the-Middle (MITM) attack environment. It covers generating and validating SSL/TLS certificates, configuring an Apache web server with custom certificates, and using DNS spoofing to intercept and manipulate what should be secure communications — then examines how PKI defends against exactly this kind of attack.

## Learning Objective

Public key cryptography underlies modern secure communication, but it's vulnerable to man-in-the-middle attacks whenever a public key is exchanged directly: there's no inherent way to verify that a given public key actually belongs to its claimed owner. PKI solves this trust problem in practice. The objective of this lab was to gain first-hand experience with PKI — understanding how it works, how it protects the web via HTTPS, and how it defeats MITM attacks — as well as to understand the concept of root trust and what breaks down if that root trust is compromised.

## Environment

- Simulated network environment with DNS spoofing capability
- Apache web server
- `openssl` (certificate generation and validation)
- `curl` (testing HTTPS connections and certificate behavior)

## What I Did

Across six tasks, I built out the full MITM simulation end to end:

- **Certificate generation and validation** — Used `openssl` to create SSL/TLS certificates and validate their behavior under different trust scenarios.
- **Apache configuration** — Set up an Apache web server to serve HTTPS using custom (including fraudulent) certificates.
- **DNS spoofing** — Simulated DNS spoofing to redirect traffic intended for a legitimate domain to a fake site under my control, enabling interception of "secure" communications.
- **Certificate behavior testing** — Used `curl` and `openssl` to test and observe how clients respond to various certificate conditions, including trusted connections, certificate–domain mismatches, and certificates issued by untrusted authorities.
- **Cleanup** — Dismantled the MITM environment by disabling the fake site, removing the DNS spoofing entries, and restoring normal resolution and functionality for the legitimate domain.

Screenshots and command outputs were captured at each step to document the process.

## Key Takeaways

- Public key exchange alone doesn't establish trust — without a way to verify that a key belongs to its claimed owner, it's trivially vulnerable to MITM attacks.
- PKI addresses this by anchoring trust in certificate authorities (CAs); HTTPS relies on this chain of trust to validate that a server is who it claims to be.
- Clients (like `curl` and browsers) actively check certificate validity — domain match, chain of trust, expiration — and this is precisely what prevents a spoofed site from silently impersonating a legitimate one.
- If root trust is broken (e.g., a malicious or compromised CA, or a client tricked into trusting a bad root certificate), the entire security model built on top of it collapses, since everything downstream depends on that root being trustworthy.
- Proper certificate management and DNS security practices are essential defenses — DNS spoofing is only a viable attack vector at all because DNS itself isn't cryptographically authenticated by default.

## Abstract

> This report documents a comprehensive exploration of HTTPS and Public Key Infrastructure (PKI) concepts through a simulated Man-in-the-Middle (MITM) attack environment. Over six tasks, the project covered the generation and validation of SSL/TLS certificates, the configuration of Apache web servers with custom certificates, and the simulation of DNS spoofing to intercept and manipulate secure communications. Tools such as curl and openssl were used to validate certificate behavior under various scenarios, including trusted connections, certificate-domain mismatches, and untrusted certificate authorities. The cleanup phase ensured the dismantling of the MITM environment by disabling the fake site, removing DNS spoofing entries, and restoring the legitimate domain's functionality. The results highlight the critical role of PKI and HTTPS in ensuring secure communication and preventing attacks, emphasizing the importance of proper certificate management and DNS security practices. Screenshots and outputs accompany each step to demonstrate the process and provide a complete understanding of the system's behavior under attack and during recovery.
