# Follow-up assessment: Vendor X's reply (simulated)

> **Fictional case study.** Example Bank and Vendor X are placeholders. All vendor replies, evidence, dates and scores are simulated. Legal references are indicative and must be checked against the official texts. 

> **Replies received:** 6 Nov 2026 (first) and 27 Nov 2026 (second evidence batch). **Evidence IDs:** EV-26 to EV-66.

## 1. Cover note from the vendor (simulated)

> Thank you for the follow-up request. We have answered 63 of the 65 new questions and all 23 re-asked questions. Our architecture and security specification is attached. Where we cannot share a document (the full AI provider contract, the full penetration test report, source code), we have offered a summary or a supervised review. We have made several changes since your first assessment: privileged access is now just-in-time, break-glass credentials are vaulted, free text is redacted from logs, VIP profiles are masked for support staff, and the AI assistant is switched off for your tenant. We cannot agree unrestricted audit rights or a 24-hour incident notice, and we have made counter-proposals.

## 2. How the vendor replied

| Reply type | Count |
|---|---|
| Full | 51 |
| Partial | 11 |
| Declined | 1 |
| No reply | 2 |

A "full" reply can still be a Gap. The reply type says how complete the answer was, and the rating says what the bank thinks of it. Of the 65 new questions the bank rated 30 Satisfactory, 26 Partial, 7 Gap and 2 Not assessed (the two "no reply" items were low priority and were not chased).

**Declined or withheld:** the full AI provider contract, the full penetration test report (summary and retest letter given), the software bill of materials (a top-20 library list given), unrestricted audit rights, 24-hour incident notice, mutual TLS, self-service credential revocation.

## 3. Replies on the open findings

| Finding | What the vendor said | Evidence | Outcome | Severity after |
|---|---|---|---|---|
| FND-01 | Read access limited to 3 platform security roles. Break-glass needs two-person approval. | EV-28, EV-26 | Closed | Closed |
| FND-02 | 90-day automated rotation. Revocation within 4 hours by the support desk. No self-service. | EV-29, EV-30 | Partly closed | Medium |
| FND-03 | Just-in-time access live since 9 Nov. Transfer assessment for India provided. Masking for offshore staff by 30 Apr 2027. | EV-26, EV-27, EV-31 | Partly closed | Medium |
| FND-04 | Provider named (Model Provider Z, US). Assistant disabled for the bank on 12 Nov. Full contract withheld. | EV-32, EV-33 | Closed for go-live scope | Closed |
| FND-05 | Counter: two on-site audits a year with 10 working days' notice, unrestricted for regulators, pooled audits. | EV-34 | Open | High |
| FND-06 | A qualified assessor letter says the vendor is out of scope (tokens only). Card Provider Y attestation valid. | EV-35, EV-04 | Closed | Closed |
| FND-07 | Planned for Q2 2027. Interim: a weekly change-log extract to Finance. | none | Open | Medium |
| FND-08 | Bridge letter issued. Scope extension to visa, gifts and card modules in the 2027 audit. | EV-36 | Partly closed | Low |
| FND-09 | No mutual TLS. Private-key JWT, IP allow-list and 15-minute tokens. | EV-37 | Risk accepted (signed) | Closed |
| FND-10 | Test on 18 Nov: 3 hours 40 minutes against 4 hours. | EV-38 | Closed | Closed |
| FND-11 | 90-day automatic deletion live from 20 Nov. | EV-39 | Closed | Closed |
| FND-12 | Redline: 30-day email notice for all changes and a right to object. Visa agency retention to follow by Mar 2027. | EV-45 | Open (agreed, unsigned) | Medium |
| FND-13 | Redaction live from 16 Nov. | EV-40 | Closed | Closed |
| FND-14 | Masked tooling live. Two months of logs show no production copies. | EV-41 | Partly closed | Low |
| FND-15 | Redline adds an insolvency clause and 24-hour credential revocation. Exit test planned for Jun 2027. | EV-45 | Open (agreed, unsigned) | Medium |
| FND-16 | 48 hours offered. Rate card provided. | EV-46 | Partly closed | Medium |
| FND-17 | Retention cut to 12 months. Alert live. | EV-42 | Closed | Closed |
| FND-18 | Vaulted with two-person approval since 10 Nov. | EV-43 | Closed | Closed |
| FND-19 | Masking live from 17 Nov. Tested by Bank IT. | EV-44 | Closed | Closed |
| FND-20 | No regional hosting before 2028. The bank rolls out in the EU first. | none | Closed for go-live scope | Closed |
| FND-21 | PGP signing from Q1 2027. The bank's call-back procedure was approved (BA-01). | none | Partly closed | Low |
| FND-22 | Reports in Q2 2027. | none | Open | Low |

## 4. Physical architecture and security specification (vendor statements)

The diagram is in `vendor-physical-architecture.png` (SVG alongside). Everything below is what the vendor **says**. It is unverified unless stated.

### 4.1 Transport security and protocols

| Flow | Protocol and authentication |
|---|---|
| FS single sign-on | SAML 2.0 over HTTPS (TLS 1.2 and 1.3), signed assertions, 30-minute idle timeout |
| FA, F3, F6, F11 (connector to the bank) | HTTPS REST, OAuth 2.0 client credentials, 15-minute tokens, fixed source IP addresses. Mutual TLS is not offered. Private-key JWT authentication is offered |
| F7, F8 (invoice, remittance) | SFTP with SSH key authentication. Files are unsigned until PGP signing starts in Q1 2027 |
| F5a to F5d (suppliers) | HTTPS, TLS 1.2 or higher. API keys. Some airline links use mutual TLS. The visa agency uses a portal upload |
| F9 (insurer) | HTTPS, TLS 1.2 or higher, OAuth client credentials |
| F12 (Card Provider Y) | HTTPS, TLS 1.2 or higher, signed requests. Tokens only come back |
| FI (AI provider) | HTTPS, TLS 1.2 or higher, API key. Switched off for the bank |
| FN, FL (notices, logs) | HTTPS, TLS 1.2 or higher, API key. Free text redacted in logs since 16 Nov |
| FV (support access) | VPN with multi-factor authentication to a privileged access tool |
| FH (cloud provider) | Provider console with multi-factor authentication. Root access disabled |
| Browser access | HTTPS, TLS 1.2 and 1.3 only, HSTS. The bank's outside-in scan agrees (OS-02) |

### 4.2 Data store security

| Store | Encryption and protection |
|---|---|
| DS1 Roster copy | AES-256 at rest, provider-managed key, TLS 1.2 to the database |
| DS2 Trips and bookings | AES-256, provider-managed key, field-level encryption for passport number and date of birth |
| DS3 Policy and rate table | AES-256, provider-managed key |
| DS4 Invoices and cards | AES-256, provider-managed key. Card tokens only |
| DS5 Audit logs | AES-256, immutable object storage, 13 months |
| Backups | Daily, AES-256, same cloud account as production. Cold-archive copy in a **US region** (found in the follow-up) |

**Key management:** provider default keys in the cloud provider's key service. Key administration and use sit with one platform team. Yearly rotation. Customer-managed keys are not offered.

### 4.3 Trust boundaries and infrastructure

| Layer | Control |
|---|---|
| Perimeter | CDN with web application firewall (managed rules), provider DDoS protection |
| Entry | Load balancer where TLS ends, then an API gateway with OAuth 2.0 and rate limits |
| Network | Public, private application and data tiers. Default-deny rules. Separate cloud accounts for production, staging and development |
| Egress | NAT gateway with an allow-list for fourth parties, reviewed twice a year |
| Connector | A dedicated instance per client in the private tier |
| Monitoring | Managed SOC 24/7, immutable logs, daily posture scans |

### 4.4 Fourth-party data controls

| Flow | Sanitisation (vendor statement) |
|---|---|
| FI prompts | Names and emails masked. Free text is **not** masked. Prompts kept 30 days by the provider. Off for the bank |
| FN notices | Names and trip dates only. No passport data |
| FL logs | Structured fields redacted. Free text redacted since 16 Nov |
| F5 suppliers | Only the fields each supplier needs, per the data-sharing register |
| F9 insurer | Schema validation, minimum fields |
| F12 card | Tokenised. The platform never holds card numbers |

### 4.5 Administrative and support access

| Item | Control |
|---|---|
| Support staff (Ireland, India) | VPN with multi-factor authentication, then a privileged access tool |
| Production access | Just-in-time with approval, 4-hour expiry, session recording. Standing access removed on 9 Nov 2026 |
| Break-glass | Vaulted credentials, two-person approval |
| VIP data | Masked for support staff since 17 Nov |
| Endpoints | Disk encryption and endpoint detection on all laptops. No endpoint data loss prevention for offshore support. USB storage allowed at two of three support sites |
| Cloud provider access | Denied to customer content by default. Support access logged and customer-approved |

### 4.6 Secure development and testing

| Item | Statement |
|---|---|
| Lifecycle | Written policy v4.2, pipeline with security gates |
| Static and dependency scans | On every merge. Three High findings open for 21, 25 and 40 days against a 14-day target |
| Dynamic testing | Quarterly. Last run 4 Oct 2026 |
| Secret scanning | On all repositories, with blocking |
| Branch protection | One reviewer and passing checks. Repository administrators can bypass. No second reviewer for infrastructure code |
| Penetration test | Annual, independent. Retest letter of 22 Jul 2026 |
| Bill of materials | Declined until Q2 2027 |
| Disclosure programme | None. Planned for 2027 |
| SOC 2 | Two exceptions, cloud provider carved out, 14 customer controls listed |

## 5. What the bank verified itself

| Item | How |
|---|---|
| AI assistant switched off | Observed by Bank IT (EV-32) |
| Credential revocation time | Observed test, 2 hours 10 minutes (EV-30) |
| VIP masking | Tested by Bank IT (EV-44) |
| Public TLS settings | Outside-in scan (OS-02) |
| Public subprocessor page | Checked: it omits the AI provider (OS-08) |

Everything else in this document is a vendor statement or a document the vendor supplied.
