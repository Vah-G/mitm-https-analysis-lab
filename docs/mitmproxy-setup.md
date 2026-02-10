# mitmproxy Setup and HTTPS Interception

## Goal
Intercept HTTPS traffic between a Windows client and external websites using **mitmproxy**, and analyze how certificate trust affects encrypted connections.

This step demonstrates a practical Man-In-The-Middle (MITM) scenario in a controlled environment.

---

## Environment

### Attacker / Proxy
- OS: Kali Linux
- Tool: mitmproxy
- Mode: regular
- Proxy address: `192.168.101.14:8080`

### Client
- OS: Windows
- Browser: Chromium-based browser
- Network: same local network as Kali

---

## Step 1: Starting mitmproxy

On Kali Linux, mitmproxy was started with:

```bash
mitmproxy --mode regular
```

## Step 2: Configuring Proxy on Windows

On the Windows machine, a manual proxy configuration was enabled.

The following settings were applied for both HTTP and HTTPS traffic:

- IP address: `192.168.101.14`
- Port: `8080`

By default, mitmproxy listens on port `8080`.

After applying the proxy settings, all browser traffic was routed through mitmproxy.

---

## Step 3: Observing Certificate Error (Untrusted CA)

When accessing an HTTPS website **before installing the mitmproxy CA certificate**, the following behavior was observed:

- The browser displayed a security warning
- The HTTPS connection was marked as *not secure*
- mitmproxy generated its own certificate for the target domain
- The certificate issuer was shown as `mitmproxy`

This indicates that the browser did not trust the MITM certificate authority.

---

## Step 4: Installing mitmproxy CA Certificate

On the Windows client:

- Opened `http://mitm.it` through the configured proxy
- Downloaded the CA certificate for Windows
- Imported the certificate into the following certificate store:
  - **Trusted Root Certification Authorities**
- The certificate was imported without requiring additional credentials.

After installation, the operating system trusted certificates issued by mitmproxy.

---

## Step 5: Successful HTTPS Interception

After the CA certificate was installed:

- HTTPS websites opened without browser warnings
- HTTPS traffic was fully visible in mitmproxy
- mitmproxy continued to act as the certificate issuer
- The browser accepted the forged certificates as trusted

This confirms a successful MITM interception due to a trusted malicious CA.

---

## Observations

- HTTPS encryption does not prevent interception if a malicious CA is trusted
- The certificate issuer changed while the connection remained encrypted
- Background HTTPS requests from browsers and system services were also intercepted

---

## Conclusion

This setup demonstrates that:

- HTTPS security relies on the trust model of Certificate Authorities
- Installing a rogue root CA enables full MITM interception
- Users can unknowingly compromise HTTPS security by trusting unverified certificates

This stage focuses on certificate trust manipulation. Packet-level analysis is covered in a later stage using Wireshark.

Screenshots related to this stage are available in:
- screenshots/certificates/
- screenshots/mitmproxy/
