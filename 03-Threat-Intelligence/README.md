# Module 3 — Threat Intelligence Investigation

## 1. Objective

To extract and investigate indicators from the phishing simulation email created in Module 1 and analyzed in Module 2.

The objective is to examine suspicious URLs, domains, and IP addresses, understand their purpose, and determine whether public threat-intelligence investigation is applicable.

## 2. Tools and Resources

- GoPhish
- Gmail Original Message
- Kali Linux
- VirusTotal — planned for applicable public URL investigations
- MXToolbox — planned for applicable domain investigations
- AbuseIPDB — planned for applicable public IP investigations

## 3. Indicator Extraction

The indicators were extracted from the original GoPhish email and its email headers.

| Indicator | Observed Value | Description |
|---|---|---|
| URL | `http://127.0.0.1/?rid=SAMPLE123` | GoPhish landing-page link |
| IP Address | `127.0.0.1` | Loopback address |
| Tracking Parameter | `rid` | GoPhish recipient tracking identifier |
| Sender Domain | `gmail.com` | Email sender/signing domain |
| Sending IP | `209.85.220.65` | Google outbound mail server |
| Sending Application | `gophish` | Identified through X-Mailer header |

Note: Tracking identifiers and email-related values are represented using documentation placeholders where appropriate.

## 4. URL Investigation

### Extracted URL

`http://127.0.0.1/?rid=SAMPLE123`

### Analysis

- Protocol: HTTP
- Host: `127.0.0.1`
- Port: 80 (default HTTP port)
- Path: `/`
- Query parameter: `rid`

The IP address `127.0.0.1` is a reserved loopback address. It refers to the local machine making the request.

The `rid` parameter is used by GoPhish to associate requests with a campaign recipient.

### Finding

The URL was configured for a local phishing simulation environment. It was not a publicly accessible phishing website.

A public URL reputation lookup using VirusTotal was therefore not applicable to this localhost address.

## 5. Domain Investigation

The extracted landing-page URL did not contain a public domain name.

The email authentication headers identified `gmail.com` as the sender and DKIM signing domain.

### Finding

- No public landing-page domain was identified.
- `gmail.com` was part of the legitimate email delivery and authentication infrastructure.
- No malicious domain was established during this investigation.

A public domain reputation investigation using MXToolbox was not applicable to the extracted localhost URL.

## 6. IP Address Investigation

Two IP addresses were identified during the email investigation.

| IP Address | Classification | Observation |
|---|---|---|
| `127.0.0.1` | Loopback | Local machine address |
| `209.85.220.65` | Google infrastructure | Outbound email server |

### Findings

**127.0.0.1**

This is a reserved loopback address used for local communication. It does not represent a publicly routable target.

**209.85.220.65**

This address appeared in Google's email delivery headers as the outbound mail server.

It was not identified as malicious in this investigation.

An AbuseIPDB malicious-IP assessment was therefore not justified based on the available evidence.

## 7. Threat Intelligence Assessment

| Indicator | Investigation Result |
|---|---|
| Localhost URL | Identified |
| Public URL reputation | Not applicable |
| Public landing-page domain | Not identified |
| Sender domain | gmail.com |
| Local IP | Reserved loopback |
| Email sending IP | Google infrastructure |
| Confirmed malicious IP | None identified |
| Confirmed malicious domain | None identified |

## 8. Limitations

- The simulation used a localhost landing-page address.
- No public phishing domain was present in the extracted URL.
- Public reputation lookups could not provide meaningful results for the localhost indicator.
- The Google sending IP was observed as part of normal email delivery and was not treated as malicious.
- No external threat-intelligence result was claimed without an actual lookup.

## 9. Conclusion

The threat-intelligence investigation identified the URL, tracking parameter, sender domain, and IP addresses associated with the original phishing simulation email.

The investigation established that the landing-page URL used a localhost address and that the email was transmitted through Google's mail infrastructure.

No publicly accessible malicious domain or confirmed malicious IP was identified.

This module demonstrates the importance of extracting and classifying indicators before submitting them to threat-intelligence platforms. Not every suspicious-looking indicator represents malicious infrastructure, and investigation conclusions must be supported by evidence.

## Disclaimer

This investigation was conducted as part of an authorized educational phishing simulation in a controlled environment. Documentation values may use illustrative placeholders to protect identifying information.
