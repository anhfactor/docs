# What Is a WAF?

### What Is a WAF?

**Web Application Firewall** (WAF) is an optional add-on to the vServer service that enables users to protect their web applications and APIs deployed on vServer by monitoring, filtering, and blocking potentially malicious HTTP/HTTPS requests before they reach the application servers.

Unlike traditional network firewalls that operate at the network or transport layer (L3/L4), a WAF works at the **application layer (Layer 7)** and understands web-specific protocols, requests, and behaviors.

In short:\
👉 **WAF sits in front of your web application and acts as a security gatekeeper.**

***

### Why Do You Need a WAF?

Modern web applications are exposed to many threats such as:

* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Remote Code Execution (RCE)
* File Inclusion (LFI/RFI)
* Bot abuse, scraping, and credential stuffing
* DDoS attacks at the application layer

A WAF helps you:

* Protect applications without changing source code
* Reduce security risks and data breaches
* Meet compliance requirements (e.g. PCI-DSS, security regulations)
* Improve overall application availability and reliability

### How a WAF Works

Typical traffic flow:

```
Client  →  WAF  →  Web Application (Origin Server)
```

1\. A client sends an HTTP/HTTPS request

2\. The WAF inspects the request in real time

3\. Security rules and detection engines analyze the request

4\. Based on the result, the WAF:

* **Allows** the request
* **Blocks** the request
* **Challenges** the request (CAPTCHA, verification)
* **Logs** the request for monitoring and auditing

### Key Capabilities of a WAF

#### 1. Attack Protection

* OWASP Top 10 protection
* Zero-day and unknown attack pattern detection (behavior-based)
* Protocol and request validation

#### 2. Access Control

* IP allowlist / denylist
* Geo-based access control
* Rate limiting by IP, URL, or user behavior

#### 3. Bot Management

* Detect and mitigate malicious bots
* Allow legitimate bots (search engines, monitoring tools)
* Protect login pages and APIs from brute-force attacks

#### 4. Traffic Visibility & Logging

* Real-time request and attack logs
* Detailed attack details (rule, source IP, payload, action)
* Traffic statistics and trends

#### 5 Custom Rules

* Create allow, deny, or monitoring rules
* Match by URL, method, headers, parameters, body
* Flexible rule priority and scope
