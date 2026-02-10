# Wireshark TLS Traffic Analysis

## Goal
Analyze HTTPS traffic at the packet level using Wireshark and compare network‑level visibility with application‑level interception performed by mitmproxy.

This stage focuses on observing encrypted TLS traffic rather than decrypting its contents.

---

## Environment

- OS: Kali Linux
- Tool: Wireshark
- Traffic source: Windows client (proxied through mitmproxy)
- Network: Local network (same subnet)

---

## Step 1: Selecting the Network Interface

Wireshark was launched on Kali Linux using the graphical interface.

The active network interface was selected based on observed traffic activity corresponding to the Windows client.

---

## Step 2: Starting Packet Capture

Packet capture was started on the selected interface while:
- mitmproxy was running
- Proxy settings remained enabled on the Windows client

Only HTTPS‑related traffic was considered for analysis.

---

## Step 3: Applying Display Filters

To reduce noise, the following display filters were applied:

```text
tcp.port == 443
```

Optionally, traffic was filtered by the Windows client IP address:

ip.addr == <WINDOWS_CLIENT_IP>

---

## Step 4: Identifying TLS Handshake

Within the captured traffic, TLS handshake messages were identified, including:

- Client Hello
- Server Hello
- Certificate exchange

These packets confirm the establishment of an encrypted TLS session.

---

## Step 5: Observing Encrypted Application Data

After the TLS handshake:

- Application data packets were marked as encrypted
- Payload contents were not readable in Wireshark
- Only metadata such as IP addresses, ports, and packet sizes were visible

---

## Observations

- TLS traffic is visible at the packet level but remains encrypted
- Wireshark does not decrypt HTTPS content without session keys
- mitmproxy and Wireshark provide different perspectives:
  - mitmproxy: application‑layer interception
  - Wireshark: network‑layer packet analysis

---

## Conclusion

This analysis demonstrates that:

- HTTPS traffic can be captured but not directly inspected at the packet level
- Encryption protects payload data even when packets are observable 
- Combining mitmproxy and Wireshark provides a broader understanding of HTTPS security

This stage complements the MITM certificate analysis performed earlier.

Screenshots related to this stage are available in:
screenshots/wireshark/
