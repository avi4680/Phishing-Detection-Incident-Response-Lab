# Module 5 — Incident Response

## 1. Objective

To document an incident response workflow based on the controlled phishing simulation conducted using GoPhish.

This module focuses on analyzing the simulation results, assessing potential risks, identifying relevant indicators, and recommending appropriate security response measures.

## 2. Incident Overview

A controlled phishing simulation was conducted using GoPhish to understand how users may interact with phishing emails and how security teams can investigate suspicious email activity.

The test email used Microsoft-themed branding and claimed that suspicious account activity had been detected.

The campaign recorded email delivery, link-click activity, and a form-submission event.

Only dummy test values were submitted during the simulation. No real account credentials were used.

## 3. Incident Classification

| Attribute | Details |
|---|---|
| Incident Type | Phishing Simulation |
| Severity | Controlled educational exercise |
| Source | GoPhish campaign |
| Target | Authorized test recipient |
| Email Theme | Microsoft account security alert |
| Email Authentication | SPF, DKIM and DMARC passed |
| Link Destination | Localhost GoPhish landing page |
| Credential Submission | Dummy values only |
| Confirmed Account Compromise | No |

## 4. Investigation Summary

The investigation was performed using the evidence collected in previous modules.

### Email Analysis

- Examined the original email headers.
- Verified SPF, DKIM and DMARC authentication results.
- Identified GoPhish through the X-Mailer header.
- Observed that the message used Microsoft-themed branding while originating from a Gmail address.
- Observed Gmail spam classification.

### URL Analysis

- Extracted the tracked URL from the email.
- Identified `127.0.0.1` as the localhost destination.
- Identified the `rid` parameter as GoPhish tracking metadata.
- Confirmed that the URL belonged to the controlled simulation environment.

### Campaign Activity

The GoPhish campaign results recorded:

- Email sent.
- Email opened.
- Link clicked.
- Form data submitted.

The form-submission event involved dummy test values and did not represent a confirmed disclosure of real credentials.

## 5. Risk Assessment

| Risk Area | Observation | Assessment |
|---|---|---|
| Email impersonation | Microsoft-themed email | Demonstrated phishing technique |
| Sender identity | Gmail sender address | Brand and sender mismatch |
| Email authentication | SPF, DKIM and DMARC passed | Authentication does not guarantee trustworthiness |
| Link interaction | Click event recorded | User interaction simulated |
| Credential submission | Dummy values entered | No real credential exposure |
| Account compromise | No evidence | Not established |

## 6. Incident Response Recommendations

### 6.1 Email Containment

- Identify and quarantine similar suspicious emails.
- Block confirmed malicious sender addresses and domains where appropriate.
- Preserve original email headers for investigation.
- Review mail gateway and email security logs.

### 6.2 Account Protection

- If real credentials are submitted in an actual phishing incident, initiate password reset procedures.
- Revoke suspicious active sessions where appropriate.
- Enable multifactor authentication.
- Review unusual login activity and account access logs.

### 6.3 URL and Infrastructure Investigation

- Extract URLs and domains from suspicious emails.
- Investigate public indicators using threat-intelligence platforms.
- Preserve relevant network and endpoint evidence.
- Avoid blocking legitimate infrastructure based on unverified indicators.

### 6.4 User Awareness

- Educate users about brand impersonation and suspicious email links.
- Encourage verification through official websites and communication channels.
- Establish a process for reporting suspicious emails.

## 7. Lessons Learned

The controlled simulation demonstrated several important security concepts:

1. Email authentication passing does not guarantee that an email is trustworthy.
2. Brand impersonation can make fraudulent messages appear convincing.
3. Tracking links can help security teams understand email interaction.
4. Form-submission events should be investigated carefully.
5. IOC classification must be supported by evidence.
6. Incident response should include containment, investigation, remediation, and user awareness.

## 8. Limitations

- The exercise was performed in a controlled educational environment.
- Only dummy credentials were submitted.
- No real account compromise occurred.
- No external malicious infrastructure was confirmed.
- The simulation does not establish the effectiveness of a production email security system.

## 9. Conclusion

The incident response exercise brought together the findings from phishing simulation, email header analysis, threat intelligence assessment, and IOC documentation.

The investigation demonstrated how suspicious email activity can be identified, analyzed, and documented through a structured security workflow.

Although the simulation recorded link interaction and dummy credential submission, no real credentials were exposed and no account compromise was established.

The exercise provided practical experience in phishing investigation, security evidence documentation, risk assessment, and incident response recommendations.

## Disclaimer

This project was conducted as an authorized educational cybersecurity simulation using GoPhish. Only dummy test values were submitted, and no real user accounts or credentials were compromised.
