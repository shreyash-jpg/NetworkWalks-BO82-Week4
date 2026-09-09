# Web Application Penetration Test — Mediroza General Hospital
**Confidential Security Assessment — Authorized Educational Engagement**

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Scope & Methodology](#scope--methodology)
- [Tools Used](#tools-used)
- [Attack Surface Discovery](#attack-surface-discovery)
- [Detailed Findings](#detailed-findings)
- [Risk Rating & Overall Assessment](#risk-rating--overall-assessment)
- [Milestone Results](#milestone-results)
- [Recommendations & Remediation](#recommendations--remediation)
- [Evidence Handling & Privacy](#evidence-handling--privacy)
- [Lessons Learned](#lessons-learned)
- [Disclaimer](#disclaimer)

---

## Executive Summary
This report documents the **Week 4 Penetration Testing Engagement** performed on the **Mediroza General Hospital** patient portal. The primary objective of this assessment was to evaluate authentication mechanisms, analyze server behavior, and identify potential exposure of sensitive patient and operational data.

Multiple severe security weaknesses were identified during the testing phase, including **Username Enumeration**, **Predictable Error Responses**, and a **Complete Lack of Rate-Limiting**, exposing the application to targeted credential stuffing and brute-force attacks.

---

## Scope & Methodology
The assessment was conducted using a **Black-Box Methodology**, simulating a real-world external attacker with no prior knowledge of internal systems or privileged credentials.

### Testing Methodology
* **Reconnaissance & Footprinting:** Gathering public intelligence and application mapping.
* **Endpoint Discovery:** Identifying active endpoints, parameter inputs, and hidden portals.
* **Authentication Testing:** Evaluating login mechanisms, session management, and credential processing.
* **Input Manipulation & Analysis:** Injecting payloads to observe server-side handling and responses.
* **Attack Simulation:** Performing manual and automated payload delivery.

---

## Tools Used

| Tool | Category | Purpose / Usage |
| :--- | :--- | :--- |
| **Burp Suite (Community Edition)** | Proxy & Scanner | Intercepting HTTP traffic, request manipulation, and Intruder attack simulation |
| **WhatWeb** | Reconnaissance | Application fingerprinting and web server tech-stack identification |
| **WAFW00F** | Reconnaissance | Web Application Firewall (WAF) detection and profiling |

---

## Attack Surface Discovery
Initial target profiling revealed several key exposed endpoints within the scope:

* **Public Homepage:** Primary landing page and public assets.
* **Patient Portal Login Page:** User authentication entry point for patients.
* **Staff Login Page:** Administrative and medical staff portal.
* **Lab Reports Section:** Authenticated file/data retrieval endpoint.
* **PHP Endpoints:** Dynamic parameters handling backend database interactions.

---

## Detailed Findings

### Finding 1: Username Enumeration
* **Severity:** **Medium**
* **Description:** The login interface returns distinct error messages when an invalid username is submitted versus an invalid password for a valid user.
* **Impact:** Allows malicious actors to harvest valid employee/patient usernames for targeted attacks.

### Finding 2: Predictable Error Responses
* **Severity:** **Medium**
* **Description:** Verbose error handling provides explicit details regarding authentication failures.
* **Impact:** Aids attackers in refining automated brute-force scripts by confirming valid user targets.

### Finding 3: Unencrypted / Verbose Login Request Interception
* **Severity:** **Medium**
* **Description:** Traffic capture via Burp Suite revealed sensitive headers and parameter structures exposed in cleartext/predictable formats.
* **Impact:** Increases vulnerability to Man-in-the-Middle (MitM) attacks and request tampering.

### Finding 4: Absence of Rate-Limiting (Intruder Simulation)
* **Severity:** **High**
* **Description:** Automated payload attacks using Burp Suite Intruder executed without encountering rate limits, CAPTCHA challenges, or IP blocks.
* **Impact:** Enables high-speed automated brute-force and credential stuffing attacks without detection or throttling.

---

## Risk Rating & Overall Assessment

| Metric | Rating |
| :--- | :--- |
| **Overall Application Risk** | **CRITICAL** |
| **Authentication Strength** | **WEAK** |
| **Exploitation Feasibility** | **HIGH** |

**Summary:** The Mediroza Hospital web application is currently exposed to high-risk authentication flaws. If exploited in a real-world scenario, an attacker could compromise valid user accounts, potentially exposing confidential patient records and healthcare systems.

---

## Milestone Results

* [x] Reconnaissance & Asset Mapping Complete
* [x] Authentication & Logic Testing Complete
* [x] Intruder Payload Attack Simulation Complete
* [x] Response & Payload Analysis Complete

---

## Recommendations & Remediation

1. **Generic Error Messages:** Standardize all authentication failure responses to a generic message (e.g., *"Invalid username or password"*).
2. **Implement Rate-Limiting:** Enforce strict request limits per IP address and per account to mitigate automated brute-force attempts.
3. **Account Lockout Policy:** Temporarily lock accounts after a threshold of consecutive failed login attempts (e.g., 5 attempts).
4. **CAPTCHA Integration:** Deploy CAPTCHA verification on all public login endpoints to prevent automated script submissions.
5. **Security Monitoring:** Implement logging and alert triggers for unusual volumes of failed login requests.

---

## Evidence Handling & Privacy
All testing activities were performed strictly within authorized parameters for educational purposes. **No real patient data (PHI) or live hospital databases were accessed, extracted, or stored during this assessment.**

---

## Lessons Learned
This engagement demonstrates how seemingly minor configuration flaws—such as verbose error messages and missing rate limits—can be chained together to compromise critical authentication systems in sensitive sectors like Healthcare IT.

---

## Disclaimer
*This security assessment was performed solely for educational and training purposes under authorized scope through NETWORKWALKS. No unauthorized access, disruption, or illegal activity occurred.*

