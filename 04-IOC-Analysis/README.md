# Module 4 — IOC Documentation

## 1. Objective

To extract, classify, and document Indicators of Compromise (IOCs) identified during the phishing simulation and email investigation.

This module organizes investigation artifacts into a structured IOC register to support security analysis, threat identification, and incident response.

## 2. Sources of Indicators

The indicators documented in this module were obtained from:

- GoPhish campaign configuration
- Original phishing simulation email
- Gmail email headers
- Email body and embedded links
- Threat intelligence investigation conducted in Module 3

## 3. IOC Register

| IOC ID | Indicator Type | Indicator Value | Source | Classification |
|---|---|---|---|---|
| IOC-001 | URL | `http://127.0.0.1/?rid=SAMPLE123` | Email body | Local simulation URL |
| IOC-002 | IP Address | `127.0.0.1` | Extracted URL | Reserved loopback |
| IOC-003 | Tracking Parameter | `rid=SAMPLE123` | Email body | GoPhish tracking identifier |
| IOC-004 | Domain | `gmail.com` | Email authentication headers | Sender/signing domain |
| IOC-005 | IP Address | `209.85.220.65` | Received header | Google outbound mail infrastructure |
| IOC-006 | Application Identifier | `gophish` | X-Mailer header | Sending application |
| IOC-007 | Email Subject | `Urgent: Suspicious Activity on your Microsoft Account` | Email header | Simulation content |
| IOC-008 | URL | `https://tuilianmeng.com/` | PhishTank / VirusTotal | Reported phishing URL |
| IOC-009 | Domain | `tuilianmeng.com` | URL analysis / MXToolbox | Suspicious domain |
| IOC-010 | IP Address | `95.85.244.113` | VirusTotal / MXToolbox | Associated hosting IP; not confirmed malicious |

**Note:** Tracking identifiers and identifying email values are represented using illustrative placeholders.
**Public Sample Reference:** PhishTank ID `9566126`  
**Source:** https://phishtank.org/phish_detail.php?phish_id=9566126

## 4. Indicator Analysis

### IOC-001 — Local Phishing Simulation URL

**Value:** `http://127.0.0.1/?rid=SAMPLE123`

**Source:** Original simulation email.

**Context:** The email contained a tracked link pointing to the locally hosted GoPhish landing page.

**Classification:** Local simulation URL.

**Recommended Action:** Keep the landing page restricted to the authorized testing environment.

### IOC-002 — Loopback IP Address

**Value:** `127.0.0.1`

**Source:** Extracted URL.

**Context:** This address refers to the local machine and is not publicly routable.

**Classification:** Reserved loopback address.

**Recommended Action:** Do not treat it as an external malicious IP or submit it as an attacker IP to reputation services.

### IOC-003 — GoPhish Tracking Identifier

**Value:** `rid=SAMPLE123`

**Source:** Embedded URL parameter.

**Context:** Used by GoPhish to associate tracked requests with a campaign recipient.

**Classification:** Campaign tracking metadata.

**Recommended Action:** Keep tracking identifiers private and avoid publishing real recipient-specific values.

### IOC-004 — Sender and Signing Domain

**Value:** `gmail.com`

**Source:** From and DKIM authentication headers.

**Context:** Gmail was used for the sender identity and DKIM signing.

**Classification:** Email service domain.

**Recommended Action:** Evaluate sender identity and claimed brand separately. Do not classify the domain as malicious based on this simulation.

### IOC-005 — Outbound Mail Server IP

**Value:** `209.85.220.65`

**Source:** Received and Authentication-Results headers.

**Context:** Identified as Google's outbound mail server.

**Classification:** Email delivery infrastructure.

**Recommended Action:** Do not classify this address as malicious based solely on its appearance in the email headers.

### IOC-006 — Sending Application

**Value:** `gophish`

**Source:** `X-Mailer` header.

**Context:** Identifies the application used to generate and send the simulation email.

**Classification:** Application identifier.

**Recommended Action:** Use this artifact to understand the origin of the controlled simulation message.

### IOC-007 — Suspicious Email Subject

**Value:** `Urgent: Suspicious Activity on your Microsoft Account`

**Source:** Original email subject header.

**Context:** Uses urgency and Microsoft-themed account-security messaging.

**Classification:** Phishing simulation content.

**Recommended Action:** Treat unexpected urgent account-security messages cautiously and verify them through official channels.

## 5. IOC Classification Summary

| Classification | Meaning | Investigation Result |
|---|---|---|
| Malicious | Confirmed harmful indicator | No external IP confirmed malicious |
| Suspicious | Indicator with threat-intelligence warnings | `tuilianmeng.com` and its URL were reported by PhishTank and flagged by 5/93 VirusTotal vendors |
| Unconfirmed | Indicator requiring additional validation | `95.85.244.113` — AbuseIPDB showed 0% abuse confidence |
| Benign / Infrastructure | Identified legitimate infrastructure | Gmail domain and Google outbound mail server |
| Local Simulation | Used within the controlled lab | GoPhish localhost URL and tracking identifier |
| Informational | Useful investigation artifact | X-Mailer and email subject |

## 6. Investigation Limitations

- The original GoPhish simulation used localhost infrastructure and does not represent a real external phishing campaign.
- The public phishing sample was investigated using PhishTank, VirusTotal, MXToolbox, and AbuseIPDB.
- VirusTotal detections represent vendor opinions at the time of lookup and may change.
- AbuseIPDB's 0% abuse confidence score does not prove that an IP address is safe.
- The association between the public phishing domain and its hosting IP does not independently establish that the IP is malicious.
- No direct interaction with the public phishing website was performed as part of this investigation.
- IOC classifications are based on the available evidence and should be reassessed if new intelligence becomes available.

## 7. Conclusion

This module organized the artifacts collected during the phishing simulation and email-header investigation into a structured IOC register.

The investigation distinguished between local simulation indicators, legitimate email infrastructure, and suspicious message characteristics.

No indicator was classified as confirmed malicious without supporting evidence.

Maintaining accurate IOC records helps security analysts investigate incidents, communicate findings, and support appropriate incident response decisions.

A separate public phishing sample was also investigated. The URL and domain were classified as suspicious based on PhishTank and VirusTotal findings, while the associated IP address remained unconfirmed.

## Disclaimer

This IOC register was created as part of an authorized educational phishing simulation. It documents controlled lab artifacts and does not identify confirmed malicious external infrastructure.
