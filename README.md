# Phishing Detection & Incident Response Lab

A hands-on cybersecurity project focused on phishing simulation, email security analysis, threat intelligence investigation, IOC documentation, and incident response.

The project combines a controlled phishing simulation using **GoPhish** with practical email-header investigation and public threat-intelligence analysis using **VirusTotal, MXToolbox, and AbuseIPDB**.

## Project Overview

Phishing is one of the common techniques used by attackers to deceive users, steal credentials, and gain unauthorized access to systems.

This project demonstrates a practical investigation workflow, starting with a controlled phishing email simulation and progressing through email analysis, threat intelligence, IOC classification, and incident response documentation.

The objective is to understand how phishing attacks can be identified, investigated, and documented using commonly used cybersecurity tools.

## Objectives

- Configure and conduct controlled phishing simulations using GoPhish.
- Analyze email headers and investigate SPF, DKIM, and DMARC authentication.
- Identify suspicious email characteristics and embedded URLs.
- Investigate URL reputation, domain information, and IP reputation.
- Extract and classify Indicators of Compromise (IOCs).
- Prepare incident investigation reports and security recommendations.

## Tools & Technologies

| Tool | Purpose |
|---|---|
| GoPhish | Controlled phishing simulation and campaign tracking |
| Kali Linux | Cybersecurity testing environment |
| Gmail | Email header inspection |
| VirusTotal | URL reputation and threat intelligence |
| MXToolbox | DNS and email security record analysis |
| AbuseIPDB | IP reputation investigation |

## Investigation Workflow

The project is organized into five modules.

### Module 1 — Phishing Simulation

- Configured GoPhish on Kali Linux.
- Created a Microsoft-themed test email template.
- Configured a landing page and test recipient.
- Launched a controlled phishing campaign.
- Verified email delivery, link tracking, and dummy form submission.

[View Module 1 →](01-Phishing-Simulation/)

### Module 2 — Email Analysis

- Examined original email headers using Gmail's Show Original feature.
- Analyzed SPF, DKIM, and DMARC authentication results.
- Investigated the email delivery path and SMTP encryption.
- Identified sender identity and brand impersonation indicators.
- Examined suspicious links and GoPhish-related headers.

[View Module 2 →](02-Email-Analysis/)

### Module 3 — Threat Intelligence Investigation

Conducted two investigations:

**Local GoPhish investigation**
- Extracted the localhost tracking URL.
- Identified the GoPhish tracking parameter.
- Classified local and email-delivery infrastructure.

**Public phishing URL investigation**
- Selected a reported phishing URL from PhishTank.
- Investigated URL reputation using VirusTotal.
- Examined DNS and DMARC information using MXToolbox.
- Investigated associated IP reputation using AbuseIPDB.
- Correlated findings across the three platforms.

[View Module 3 →](03-Threat-Intelligence/)

### Module 4 — IOC Documentation

- Extracted indicators from email headers and message content.
- Documented URLs, IP addresses, domains, and application identifiers.
- Classified indicators based on available evidence.
- Distinguished local simulation artifacts from public infrastructure.
- Prepared a structured IOC register.

[View Module 4 →](04-IOC-Analysis/)

### Module 5 — Incident Response

- Reviewed findings from the previous investigation modules.
- Assessed phishing-related risks.
- Documented containment and remediation recommendations.
- Identified account protection and user-awareness measures.
- Prepared an incident response report based on the controlled simulation.

[View Module 5 →](05-Incident-Response/)

## Key Investigation Findings

The project demonstrated several important cybersecurity concepts:

- SPF, DKIM, and DMARC can pass even when an email contains phishing content.
- Sender authentication does not establish the legitimacy of claimed brand identity.
- GoPhish can record email delivery, link interactions, and form-submission events.
- VirusTotal, MXToolbox, and AbuseIPDB provide different perspectives on URLs, domains, and IP addresses.
- A URL can receive malicious or phishing detections even when its associated IP has no abuse reports.
- IOC classification must be supported by investigation evidence.

## Project Structure

```text
Phishing-Detection-Incident-Response-Lab/
│
├── 01-Phishing-Simulation/
│   ├── campaign-setup.md
│   └── screenshots/
│       ├── 01-gophish-dashboard.png
│       ├── 02-email-template.png
│       ├── 03-campaign-configuration.png
│       ├── 04-test-email.png
│       ├── 05-landing-page.png
│       └── 06-campaign-results.png
│
├── 02-Email-Analysis/
│   └── README.md
│
├── 03-Threat-Intelligence/
│   └── README.md
│
├── 04-IOC-Analysis/
│   └── README.md
│
├── 05-Incident-Response/
│   └── README.md
│
└── README.md
```

## Key Learning Outcomes

Through this project, I gained practical experience in:

- Phishing campaign configuration and tracking.
- Email header analysis and authentication mechanisms.
- URL, domain, and IP reputation investigation.
- Threat intelligence correlation.
- IOC extraction and classification.
- Incident investigation and response documentation.

## Limitations

- The GoPhish simulation was conducted in a controlled local environment.
- Only dummy values were submitted during the simulation.
- No real credentials were collected or real accounts compromised.
- The public phishing sample was investigated using third-party threat-intelligence services.
- Threat-intelligence results represent observations at the time of investigation and may change.
- No real-world attacker infrastructure or compromise was independently established through the controlled simulation.

## Disclaimer

This project is intended strictly for educational and authorized cybersecurity testing.

The GoPhish simulation was conducted in a controlled environment using an authorized test recipient. The public phishing URL was investigated through threat-intelligence platforms without directly visiting the website or submitting credentials.

No unauthorized access, credential theft, or real-world phishing activity was conducted.

---

**Project Focus:** Phishing Simulation | Email Security | Threat Intelligence | IOC Analysis | Incident Response
