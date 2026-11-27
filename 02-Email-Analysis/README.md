
# Module 2 — Email Analysis

## 1. Objective

To investigate a controlled phishing simulation email by examining its original email headers, tracing its delivery path, and analyzing email authentication mechanisms such as SPF, DKIM, and DMARC.

The objective is to understand how email authentication works and identify suspicious characteristics that may indicate phishing activity.

## 2. Tools Used

- Gmail — Original Message / Show Original
- GoPhish
- Kali Linux
- Manual email header analysis

## 3. Email Overview

The investigated email was generated as part of the controlled GoPhish phishing simulation conducted in Module 1.

| Attribute | Observed Value |
|---|---|
| Sender | `sender@example.com` |
| Recipient | `recipient@example.com` |
| Subject | Urgent: Suspicious Activity on your Microsoft Account |
| Sending Application | GoPhish |
| X-Mailer | `gophish` |
| Content Type | `text/html` |
| Email Classification | Gmail Spam |

The email used Microsoft-themed branding and claimed that suspicious login activity had occurred on the recipient's account.

## 4. Email Authentication Analysis

Gmail's original-message analysis reported the following authentication results:

| Mechanism | Result | Observed Details |
|---|---|---|
| SPF | PASS | Sending IP authorized by Gmail sender domain |
| DKIM | PASS | Signing domain: `gmail.com` |
| DMARC | PASS | Visible From domain aligned with authenticated domain |

### 4.1 SPF — Sender Policy Framework

**Result: PASS**

Relevant header information:

- Envelope sender domain: `gmail.com`
- Sending server IP: `209.85.220.65` (placeholder)

SPF checks whether the sending server is authorized to send email on behalf of the envelope-sender domain.

The authentication results indicated that the sending IP was authorized under the sender domain's SPF policy.

### 4.2 DKIM — DomainKeys Identified Mail

**Result: PASS**

Relevant header information:

- Signing domain (`d=`): `gmail.com`
- Selector (`s=`): `20260707`
- Algorithm: `rsa-sha256`

DKIM uses a digital signature to help verify that signed portions of an email have not been modified and that the signature corresponds to the signing domain.

The receiving Gmail server successfully validated the DKIM signature.

### 4.3 DMARC — Domain-based Message Authentication, Reporting and Conformance

**Result: PASS**

Relevant authentication details:

- Visible From domain: `gmail.com`
- DMARC policy (`p`): `NONE`
- Subdomain policy (`sp`): `QUARANTINE`
- Disposition (`dis`): `NONE`

DMARC evaluates whether SPF or DKIM authentication aligns with the domain shown in the visible From address.

In this investigation, DMARC passed because the authenticated Gmail domain aligned with the visible sender domain.

**Important observation:** Passing SPF, DKIM, and DMARC does not establish that an email's content or claimed brand identity is legitimate.

## 5. Email Delivery Path Analysis

The Received headers provided information about the email's delivery route.

The observed sequence was:

1. **Originating machine:** The message originated from the local machine identified as `auto-bots`.
2. **Gmail SMTP:** GoPhish submitted the email through Gmail's authenticated SMTP service (`smtp.gmail.com`).
3. **Google outbound server:** Gmail transmitted the message through a Google mail server.
4. **Recipient mail server:** Google's receiving infrastructure accepted the message.

Additional observations:

- SMTP authentication was used (`ESMTPSA`).
- The SMTP connection used TLS 1.3.
- The negotiated cipher suite was `TLS_AES_128_GCM_SHA256`.

This confirms that the message was submitted through Gmail's authenticated mail infrastructure rather than being sent directly from the local machine to the recipient's mail server.

## 6. Phishing Indicators Identified

### 6.1 Brand Impersonation

The email used Microsoft-themed branding and a subject suggesting suspicious Microsoft account activity.

However:

- The actual sender used a Gmail address.
- The DKIM signing domain was `gmail.com`.
- The email did not establish that it originated from Microsoft's official mail infrastructure.

This mismatch between the claimed brand and actual sender identity is a phishing indicator.

### 6.2 Suspicious Link Destination

The email contained a tracked link pointing to:

`http://127.0.0.1/?rid=SAMPLE123`

The message also contained a tracking image:

`http://127.0.0.1/track?rid=SAMPLE123`

The address `127.0.0.1` is the loopback address, which refers to the local machine making the request.

The `rid` parameter was used by GoPhish for campaign tracking.

The destination did not correspond to an official Microsoft website.

### 6.3 GoPhish Identification

The following header was present:

`X-Mailer: gophish`

This identifies GoPhish as the application that generated and submitted the test email.

## 7. Spam Classification Observation

Although SPF, DKIM, and DMARC all passed, Gmail classified the test email as spam.

This demonstrates that successful email authentication does not guarantee inbox placement.

Spam filtering can consider additional signals, including sender reputation, message content, sending patterns, and recipient feedback.

The exact reason for this particular spam classification cannot be established from the available headers alone.

## 8. Investigation Findings

| Investigation Area | Finding |
|---|---|
| Email authentication | SPF, DKIM, and DMARC passed |
| Sending application | GoPhish |
| Actual sender domain | gmail.com |
| Claimed brand | Microsoft |
| Delivery route | GoPhish → Gmail SMTP → Google mail infrastructure |
| SMTP encryption | TLS 1.3 |
| Suspicious link | Localhost tracking URL |
| Spam classification | Classified as spam by Gmail |

## 9. Limitations

- The investigation was conducted using a controlled test email.
- Authentication results establish the sending domain's authentication status, not the legitimacy of the email's claims.
- The exact reason for Gmail's spam classification could not be determined from the available headers.
- The investigation does not establish that a real Microsoft account was targeted or compromised.

## 10. Conclusion

The email header investigation demonstrated how SPF, DKIM, and DMARC can be used to evaluate email authentication and sender-domain alignment.

All three authentication mechanisms passed because the test email was sent through Gmail's authorized infrastructure using a Gmail sender identity.

However, the message used Microsoft-themed branding while originating from a Gmail address and contained a GoPhish tracking link pointing to localhost.

The investigation highlights an important security principle: **an authenticated email is not necessarily a trustworthy email.**

This module establishes the foundation for further threat intelligence investigation, IOC identification, and incident response analysis.

## Disclaimer

This investigation was performed as part of an authorized educational phishing simulation in a controlled environment. No real Microsoft accounts were targeted.

---

**Note:** Email addresses, IP addresses, and tracking identifiers in this public documentation are illustrative placeholders. They do not represent the original captured values.
