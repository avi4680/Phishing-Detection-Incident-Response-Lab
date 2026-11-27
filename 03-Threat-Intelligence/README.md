# Module 3 — Threat Intelligence Investigation

## 1. Objective

To extract and investigate indicators from the phishing simulation conducted in Module 1 and the email analyzed in Module 2.

This module also includes a separate public phishing URL investigation using VirusTotal, MXToolbox, and AbuseIPDB.

The objective is to understand URL reputation, domain infrastructure, IP reputation, and the correlation of findings across threat-intelligence platforms.

## 2. Tools and Resources

- GoPhish
- Kali Linux
- Gmail Original Message
- PhishTank
- VirusTotal
- MXToolbox
- AbuseIPDB

# Part A — Local GoPhish Investigation

## 3. Indicators Extracted from the Simulation Email

The original GoPhish email and its headers contained the following indicators:

| Indicator | Observed Value | Description |
|---|---|---|
| URL | `http://127.0.0.1/?rid=SAMPLE123` | Local GoPhish landing-page URL |
| IP Address | `127.0.0.1` | Loopback address |
| Tracking Parameter | `rid` | GoPhish recipient tracking identifier |
| Sender Domain | `gmail.com` | Email sender/signing domain |
| Google Outbound Mail Server IP | `209.85.220.65` | Google server that handled outbound email delivery |
| Sending Application | `gophish` | Identified through X-Mailer header |

Note: The tracking identifier is represented using a placeholder.

## 4. Local URL Analysis

### Extracted URL

`http://127.0.0.1/?rid=SAMPLE123`

### Analysis

- Protocol: HTTP
- Host: `127.0.0.1`
- Port: 80 (default HTTP port)
- Path: `/`
- Query parameter: `rid`

The address `127.0.0.1` is a reserved loopback address that refers to the local machine.

The `rid` parameter is used by GoPhish to associate tracked requests with campaign recipients.

### Finding

The URL was configured for a local phishing simulation environment. It was not a publicly accessible phishing website.

A public URL reputation lookup was not meaningful for this localhost address.

# Part B — Public Phishing URL Investigation

## 5. Investigation Sample and Source

A separate public phishing URL was selected from PhishTank for threat-intelligence analysis.

| Attribute | Details |
|---|---|
| Source | PhishTank |
| PhishTank Entry ID | `9566126` |
| Reported URL | `https://tuilianmeng.com/` |
| Domain | `tuilianmeng.com` |
| Submitted By | `Josua33` |

Source: https://phishtank.org/phish_detail.php?phish_id=9566126

The public sample was investigated using VirusTotal, MXToolbox, and AbuseIPDB. The website itself was not visited directly.

## 6. VirusTotal — URL Reputation Analysis

### Investigated URL

`https://tuilianmeng.com/`

### Observed Results

| Attribute | Result |
|---|---|
| Domain | `tuilianmeng.com` |
| Associated IP | `95.85.244.113` |
| HTTP Status | `200` |
| Content Type | `text/html; charset=utf-8` |
| Detection Ratio | `5/93` |
| Report Date | 27 November 2026 |

### Security Vendor Detections

The following vendors flagged the URL:

| Security Vendor | Classification |
|---|---|
| Emsisoft | Phishing |
| Fortinet | Phishing |
| LevelBlue | Phishing |
| Netcraft | Malicious |
| Webroot | Malicious |

The other displayed vendors in the screenshot showed clean results.

### Analysis

Five out of 93 security vendors flagged the URL as phishing or malicious.

This provides a suspicious reputation signal, although the detection ratio alone does not establish that every security vendor agrees on the classification.

The HTTP 200 response indicates that the server returned a successful HTTP response. It does not establish that the website is safe.

### Finding

Multiple security vendors independently flagged the URL. The associated domain and IP address were extracted for further investigation.

VirusTotal Report:

https://www.virustotal.com/gui/url/6c8a57a56498f826db72749cf4284dfd401216acdf06e9712daf8a1d737f7ec1/detection

## 7. MXToolbox — Domain and DNS Investigation

### Investigated Domain

` tuilianmeng.com `

### Observed DNS Results

| Attribute | Result |
|---|---|
| Record Type | A |
| Domain | `tuilianmeng.com` |
| Resolved IP | `95.85.244.113` |
| TTL | 10 minutes |
| DNS Record | Published |

### DMARC Check

MXToolbox displayed the following warning:

The domain does not currently have protection from email spoofing.

The lookup indicated that a DMARC record was not found.

DMARC allows domain owners to publish policies for handling emails that fail authentication and alignment checks.

### Analysis

The domain's A record resolved to `95.85.244.113`, matching the IP associated with the URL in the VirusTotal report.

The missing DMARC record is a domain email-security configuration observation. It does not independently prove that the domain is malicious.

### Finding

DNS resolution was successful, and the domain was associated with the same IP identified by VirusTotal.

MXToolbox also displayed a DMARC-related warning.

## 8. AbuseIPDB — IP Reputation Investigation

### Investigated IP Address

`95.85.244.113`

### Observed Results

| Attribute | Result |
|---|---|
| IP Address | `95.85.244.113` |
| Abuse Confidence Score | `0%` |
| Abuse Reports | None |
| ISP | Noyobzoda Faridduni Saidilhom |
| Usage Type | Data Center/Web Hosting/Transit |
| ASN | AS208885 |
| Country | Czechia |
| City | Veseli nad Moravou |
| Domain Name | Unknown |

### Analysis

AbuseIPDB reported that no abuse reports were available for this IP address.

The abuse confidence score was 0%, indicating that the platform had no recent abuse reports on file.

A zero score does not guarantee that an IP address is safe. It only describes the information available in the AbuseIPDB database at the time of the lookup.

### Finding

No reported abusive activity was found for the IP address in AbuseIPDB.

The IP was associated with data center/web hosting/transit infrastructure according to the displayed lookup result.

## 9. Cross-Platform Indicator Correlation

The results from all three platforms were compared to identify relationships between the URL, domain, and IP address.

| Indicator | VirusTotal | MXToolbox | AbuseIPDB |
|---|---|---|---|
| URL | 5/93 detections | Not assessed | Not assessed |
| Domain | `tuilianmeng.com` | A record found | Domain name unknown |
| IP Address | `95.85.244.113` | `95.85.244.113` | `95.85.244.113` |
| Reputation | Multiple vendor detections | DNS and DMARC findings | 0% abuse confidence |

### Correlation Findings

1. VirusTotal associated the investigated URL with `95.85.244.113`.
2. MXToolbox independently resolved the domain to the same IP address through its A record lookup.
3. MXToolbox displayed a warning indicating that no DMARC record was found.
4. AbuseIPDB returned a 0% abuse confidence score and no abuse reports for the IP.

### Overall Assessment

The URL received suspicious reputation detections from multiple VirusTotal vendors.

However, AbuseIPDB did not have reports identifying the associated IP as abusive.

This demonstrates that URL reputation and IP abuse reputation are separate investigation dimensions. A suspicious URL can be flagged even when its hosting IP has no abuse reports.

## 10. Investigation Summary

| Investigation | Result |
|---|---|
| Local GoPhish URL analysis | Completed |
| PhishTank sample identification | Completed |
| VirusTotal URL investigation | 5/93 detections |
| Domain DNS lookup | A record found |
| DMARC lookup | Warning displayed |
| Associated IP extraction | Completed |
| AbuseIPDB IP investigation | 0%, no reports |
| Cross-platform correlation | Completed |

## 11. Limitations

- The local GoPhish URL was not publicly accessible.
- The public phishing URL was investigated through external intelligence platforms rather than by directly visiting the website.
- VirusTotal detection results represent the reporting engines at the time of analysis.
- MXToolbox DNS and DMARC findings represent the lookup results at the time of testing.
- AbuseIPDB had no abuse reports for the associated IP at the time of lookup.
- A lack of IP abuse reports does not establish that the IP is safe.
- No malicious activity was independently confirmed on the hosting server.
- Threat-intelligence results can change over time.

## 12. Conclusion

This module investigated indicators from both the controlled GoPhish simulation and a separate public phishing URL sample.

The local investigation identified the localhost URL, tracking parameter, sender domain, and email delivery IP.

The public investigation used PhishTank as the sample source and VirusTotal, MXToolbox, and AbuseIPDB to examine URL reputation, DNS configuration, and IP reputation.

Multiple VirusTotal vendors flagged the public URL, MXToolbox resolved its domain to the associated IP and displayed a DMARC warning, while AbuseIPDB reported no abuse records for that IP.

The investigation demonstrated the importance of combining multiple threat-intelligence sources and interpreting their findings together rather than relying on a single reputation score.

## Disclaimer

This project was conducted for educational and authorized cybersecurity investigation purposes.

The original GoPhish simulation was performed in a controlled local environment. The public URL was investigated using third-party threat-intelligence services without directly visiting the website or submitting credentials.
