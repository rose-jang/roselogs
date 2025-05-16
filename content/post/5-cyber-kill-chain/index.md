---
title: Understanding the Cyber Kill Chain
date: 2025-05-16
draft: false
disqus: false
image: cyberkillchain-banner.png
tags:
  - Security
  - SOC
categories: 
  - Cybersecurity
---
# Cyber Kill Chain

To effectively defend a network, we must learn to think like an attacker. By understanding how cyber attacks unfold, we can proactively secure our systems and prevent damage before it happens. One of the key steps in that process is learning the **Cyber Kill Chain**.

## What is it?

The **Cyber Kill Chain** is a foundational framework in cybersecurity that outlines the typical stages of a cyber attack—from initial planning to achieving the attacker’s end goal. Developed by Lockheed Martin, this model helps security teams understand the attack lifecycle in depth. By identifying and interrupting attacks at various stages, defenders can significantly reduce the likelihood of a successful breach.

## 7 Stages

### 1-Reconnaissance

Planning phase, attackers gather information about their target

- **Passive**: Collect data without direct interaction (*e.g., archived websites, social media, public records*)
- **Active**: Direct engagement (*e.g., scanning ports, pining servers***)**

---

**Defender’s role**:

- Avoid publicly exposed information
- Patch known vulnerability in an early stage
- Monitor suspicious network activity (scanning or probing)

### 2-Weaponization

Prepare a payload (bundle of malicious codes) to exploit using the information collected

**Defender’s role**:

- Use the latest threat intelligence
- Configure detection rules for common exploits

### 3-Delivery

Expose the payload to lure victims (vis phishing emails, malicious websites/attachments, USBs, …)

Defender’s role:

- Test suspicious files in sandbox
- Educate users on phishing attacks
- Monitor for unusual behaviour

### 4-Exploitation

Payload executed once vulnerability is triggered

Defender’s role: 

- User training to avoid clicking suspicious links/files
- EDR (Endpoint Detection & Response) monitoring
- Continuous monitoring for unusual behaviour

### 5-Installation

Malware installation (backdoor, web shell) on the compromised system

Defender’s role:

- Monitor OS settings change
- Block unauthorized system tasks or services
- Threat hunting to detect uncommon installation

### 6-Command&Control (C2)

The malware contacts a remote server that manipulates the infected machine

**Defender’s role:**

- Analyze outbound traffic
- Block known malicious IPs/domains
- Isolate infected systems

### 7-Actions on Objectives

Accomplish initial goals by stealing data, damage systems, or ransomware, …

**Defender’s role:**

- Restrict network access from external
- Implement DLP to prevent data leakage
- Lock down sensitive resources

---

# Conclusion

We explored the stages of the Cyber Kill Chain that offers valuable insight into how attackers operate, and how defenders respond at each phase. Understanding this model is a crucial step toward building a proactive and effective cybersecurity strategy.