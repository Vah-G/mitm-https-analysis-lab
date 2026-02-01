# MITM HTTPS Analysis Lab

This project demonstrates a practical Man-In-The-Middle (MITM) scenario
where HTTPS traffic from a Windows machine is intercepted using a Kali Linux system
in a controlled lab environment.

The goal of the project is to understand how MITM attacks affect TLS/HTTPS connections
and how such activity can be identified through certificate and traffic analysis.

---

## Project Goal

- Simulate a MITM scenario in a lab environment
- Intercept and inspect HTTPS traffic
- Analyze X.509 certificates and certificate chains
- Identify changes caused by interception

---

## Environment

- Interceptor: Kali Linux
- Client: Windows PC
- Network: Local lab network
- Traffic: HTTPS connections to public websites
- Scope: Controlled, educational environment

---

## Tools Used

- Kali Linux
- MITM proxy tools (e.g. mitmproxy)
- Wireshark
- Web browser (Chrome / Firefox)
- OpenSSL
- Browser certificate inspection tools

---

## Experiment Overview

### 1. Baseline HTTPS Connection
- Direct HTTPS connection from Windows to a website
- Inspection of:
  - Certificate issuer
  - Validity period
  - Certificate chain
  - SHA-256 fingerprint

### 2. MITM Setup
- Kali Linux positioned between Windows and the internet
- HTTPS traffic intercepted via a proxy
- Proxy generates substitute certificates

### 3. Certificate Analysis
- Comparison of original and intercepted certificates
- Detection of:
  - Issuer changes
  - Fingerprint mismatch
  - Trust chain modifications

---

## Key Observations

- HTTPS traffic remains encrypted but trust is altered
- Certificate metadata changes during interception
- Browsers rely on trusted CAs to detect MITM activity

---

## Next Steps

- Document detailed MITM setup steps
- Add packet capture (PCAP) analysis
- Include screenshots and logs
