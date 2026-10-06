# Follow-up assessment: the bank's request to Vendor X

> **Fictional case study.** Example Bank and Vendor X are placeholders. All vendor replies, evidence, dates and scores are simulated. Legal references are indicative and must be checked against the official texts. 
>
> **Request date:** 12 Oct 2026. **First reply due:** 6 Nov 2026. **Builds on:** the initial assessment (folders 01 to 05, unchanged).

## 1. Why a follow-up assessment

The initial assessment gave a conditional decision with 22 findings, 5 of them High, and left 23 questions unassessed. The vendor has since seen the data flow diagrams, and the bank now needs the **physical view**: protocols, encryption, network segmentation, support access and secure development. This request asks for that, and for the evidence that would let the bank re-rate the open findings.

The follow-up does not change the initial assessment. It adds evidence, and the re-rating is recorded separately (see `follow-up-overview.md`).

## 2. How to reply

| Item | Rule |
|---|---|
| Deadline | First reply by 6 Nov 2026. If more time is needed for a specific item, say so and give a date |
| Evidence | Prefer exports, reports and dated screenshots. A policy alone, or a statement, is weak evidence |
| Priority | **Must** items are needed for the go-live decision. **Should** items improve confidence. **If applicable** items depend on the vendor's setup, and the bank may drop them |
| Asked by | Shows which bank function needs the answer (Analyst, TPRM lead, IT security, DPO, Compliance, Finance) |
| Refusals | If an item cannot be shared, say why and offer an alternative (for example a summary or a supervised review) |

## 3. Part A: evidence to close the open findings (22)

| Finding | Title | Severity | What the bank asks for |
|---|---|---|---|
| FND-01 | Wide standing access to connector credentials | High | Updated list of who can read connector secrets; approval workflow |
| FND-02 | Connector credentials rotated only once a year | High | Rotation schedule and a revocation test |
| FND-03 | Standing support access from India with no transfer assessment | High | Just-in-time access, access logs, masked data, transfer assessment |
| FND-04 | Undisclosed AI model provider with US hosting | High | Name of the provider and a way to switch the feature off |
| FND-05 | Audit and inspection rights too limited | High | An amended audit clause giving unrestricted rights |
| FND-06 | Vendor's own PCI DSS attestation missing | Medium | The vendor's own attestation or a scoping statement |
| FND-07 | No four-eyes control on the allowance rate table | Medium | Second approval for rate changes |
| FND-08 | Assurance reports are outdated or narrow | Medium | A bridge letter and a scope extension |
| FND-09 | No mutual TLS on bank-facing connections | Medium | Mutual TLS, or compensating controls |
| FND-10 | Recovery targets not proven | Medium | A disaster recovery test that meets the target |
| FND-11 | Guest data kept 24 months without deletion | Medium | Automatic deletion of guest data |
| FND-12 | Weak fourth-party notice, deletion and role classification | Medium | Notice and a right to object for every subprocessor change; shorter retention at suppliers |
| FND-13 | Free text not redacted from logs | Medium | Redaction of free text in logs |
| FND-14 | Production data used in test | Medium | Masked data in test |
| FND-15 | Exit arrangements weak | Medium | An insolvency clause and a tested exit plan |
| FND-16 | Slow incident notification and no assistance rate card | Medium | Notice within 24 hours and a rate card |
| FND-17 | Insurer and assistance data handling | Medium | Shorter retention and an alert on interface failure |
| FND-18 | Break-glass admin accounts not vaulted | Medium | Vaulted break-glass credentials |
| FND-19 | VIP itineraries visible unmasked to support staff | Medium | Masked VIP profiles for support staff |
| FND-20 | No regional hosting for non-EU staff | Medium | A regional hosting plan |
| FND-21 | Invoice files not signed and no call-back on bank-detail changes | Medium | Signed invoice files and a call-back check |
| FND-22 | Minor gaps in loyalty, discount codes and booker access reporting | Low | Access and usage reports |

## 4. Part B: physical architecture and security specification

Please provide a physical data flow or technical architecture diagram, or an updated specification, covering these five points:

1. **Transport security and protocols** for every data flow, in particular single sign-on (FS), the supplier flows (F5a to F5d, F9, F12) and browser flows: the protocol, the TLS version, and whether mutual authentication is used.
2. **Data store security** for DS1 to DS5: encryption at rest and in database connections, and key management (who holds keys, rotation, backups).
3. **Trust boundaries and infrastructure security:** the perimeter and network controls between the internet, the vendor cloud and the databases (firewalls, web application firewall, API gateway, load balancers, network segmentation).
4. **Fourth-party data controls:** whether personal data is masked, tokenised or sanitised before it is sent to the AI provider (FI), to notification and monitoring providers (FN, FL) and to suppliers.
5. **Administrative and support access:** the mechanisms for remote vendor support (FV) and cloud provider access (FH), for example multi-factor authentication, bastion hosts, VPN and privilege management.

Please also provide evidence of secure development and testing:

| Item | Examples of evidence |
|---|---|
| Automated pipeline scanning | Summaries of static analysis, dependency scanning, dynamic testing and secret scanning |
| Branch protection and code review | Repository rule screenshots: no direct pushes to production branches, required reviewers, required passing scans |
| Penetration testing | The report, or a retest letter, and the tracker showing fixes within the vendor's own deadlines |
| Frameworks and assurance | SOC 2 Type II or ISO 27001 scope, exceptions and carve-outs, and the application security standard the vendor follows |

## 5. Part C: new questions by area (65)

Priority: 38 Must, 21 Should, 6 If applicable.

### Identity and access management (IAM)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-IAM-01 | How is privileged access to production systems granted (just-in-time, approval, expiry), and how long can a privileged session last? | Must | IT security | FND-03 | Privileged access tool configuration; 30-day access log |
| FU-IAM-02 | Provide the privileged account inventory and the date of the last privileged access review. | Must | Analyst | FND-01 | Account inventory; review record |
| FU-IAM-03 | How are service accounts and API keys inventoried, owned and rotated? Which belong to the bank's connector? | Must | IT security | FND-02 | Service-account inventory; rotation logs |
| FU-IAM-04 | Can the bank revoke the connector's credentials itself, and how fast can the vendor revoke on request? | Must | IT security | FND-02 | Revocation test record |
| FU-IAM-05 | How is segregation of duties enforced for vendor staff who can both deploy code and access production data? | Should | TPRM lead | new | Segregation matrix; approved exceptions |

### Data security (DAT)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-DAT-01 | Provide the data classification scheme and show how passport data and executive itineraries are labelled and handled. | Should | DPO | D2, D4 | Classification scheme; handling rules |
| FU-DAT-02 | Provide the record of where each data type is stored and processed, including every location of backups and replicas. | Must | DPO | V6 | Data inventory; storage regions |
| FU-DAT-03 | How are backups and snapshots encrypted, and who can restore them? | Should | IT security | new | Backup encryption configuration; restore rights |
| FU-DAT-04 | How do you stop personal data leaving through endpoints and email (data loss prevention)? | If applicable | Analyst | new | DLP configuration; device policies |

### Cryptography and key management (CRY)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-CRY-01 | Who manages the encryption keys for databases and backups, and can the bank use its own keys? | Must | IT security | FND-27 | Key management description |
| FU-CRY-02 | How are key custodians separated, and how often are keys rotated and revoked? | Must | IT security | FND-27 | Key policy; rotation log |
| FU-CRY-03 | Provide the TLS configuration for public endpoints and for connections to the database and to fourth parties. | Should | Analyst | FND-09 | TLS configuration summary |

### Application security (APP)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-APP-01 | Provide the secure development policy and a process diagram showing where security checks occur. | Must | Analyst | new | Policy; process diagram |
| FU-APP-02 | Provide the latest static analysis and dependency scan summaries for the platform and the connector, with open High findings and their age. | Must | IT security | new | Scan summaries (SAST, SCA) |
| FU-APP-03 | How often is dynamic testing (DAST) run against a staging environment, and what were the last results? | Should | IT security | new | DAST summary |
| FU-APP-04 | Show the branch protection and code review rules for production and infrastructure repositories. | Must | TPRM lead | new | Branch protection screenshots |
| FU-APP-05 | Is automated secret scanning run on code repositories, and how are leaked secrets handled? | Must | IT security | V7 | Scanner configuration; incident records |
| FU-APP-06 | Provide the software bill of materials, or the list of critical third-party libraries, for the connector and platform. | If applicable | TPRM lead | new | Bill of materials or library list |
| FU-APP-07 | Has a threat model been done for the connector and the support access path, and when was it last updated? | Should | IT security | new | Threat model summary |

### Cloud security (CLD)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-CLD-01 | Provide the shared-responsibility matrix between the vendor and its cloud provider. | Should | Analyst | new | Responsibility matrix |
| FU-CLD-02 | How is cloud configuration monitored for drift and misconfiguration (posture management)? | Should | IT security | new | Posture report |
| FU-CLD-03 | Describe production, standby and backup regions, with a diagram of data replication between them. | Must | Analyst | V6 | Region and replication diagram |
| FU-CLD-04 | How are production, staging and development environments separated, and who can access each? | Must | IT security | V10 | Environment separation description |

### Network security (NET)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-NET-01 | Provide the network segmentation design: separation of web, application and database tiers, and administrative access. | Must | IT security | new | Segmentation diagram; rule summary |
| FU-NET-02 | Which perimeter controls protect public endpoints (web application firewall, DDoS protection, API gateway, rate limits)? | Must | IT security | new | Configuration summary |
| FU-NET-03 | How is outbound traffic from production restricted to approved destinations? | Should | IT security | FND-09 | Egress rules |

### Third-party risk (TPR)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-TPR-01 | How do you assess your own suppliers (security review, questionnaire, reassessment), and how often? | Must | Analyst | FND-12 | Supplier assessment procedure |
| FU-TPR-02 | Which suppliers receive personal data from the bank's tenant, and what contract terms flow down to them? | Must | DPO | FND-04, FND-12 | Supplier register; flow-down terms |
| FU-TPR-03 | What is your concentration exposure to your cloud provider, and what is the plan if it fails? | Should | TPRM lead | new | Concentration statement; exit plan |
| FU-TPR-04 | Provide your last two supplier incident notifications and how you responded. | If applicable | TPRM lead | new | Incident records |

### AI security (AIS)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-AIS-01 | Name the AI model provider and its hosting region, and provide the contract and data processing terms for the bank's use case. | Must | TPRM lead | FND-04 | Provider name; contract excerpt |
| FU-AIS-02 | Show that the AI assistant can be switched off for the bank's tenant, and demonstrate it. | Must | Analyst | FND-04 | Configuration; test session |
| FU-AIS-03 | How are prompts and outputs logged, masked and retained, and does free text with personal data reach the provider? | Must | DPO | FND-04 | Prompt handling description |
| FU-AIS-04 | How are prompt injection and data leakage tested, and how is the feature classified under the EU AI Act? | Should | Compliance | new | Test summary; classification note |

### Vulnerability and security testing (VUL)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-VUL-01 | Provide vulnerability scan coverage and patch deadlines, with the number of open Critical and High items. | Must | IT security | L3 | Scan summary |
| FU-VUL-02 | Provide the full penetration test report or the retest letter confirming the High findings were fixed. | Must | TPRM lead | EV-03 | Retest letter |
| FU-VUL-03 | Do you run a vulnerability disclosure programme or bug bounty, and is there a security contact page? | If applicable | Analyst | new | Public page; programme details |

### Security monitoring (MON)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-MON-01 | Describe 24/7 security monitoring, escalation times, and coverage of identity, cloud and database logs. | Must | IT security | new | SOC contract summary; coverage matrix |
| FU-MON-02 | Are logs immutable, and how long are they kept (hot and cold)? | Should | IT security | FND-13 | Retention configuration |
| FU-MON-03 | Can vendor administrator activity on the bank's tenant be sent to the bank's SIEM? | Should | IT security | FND-03 | Integration description |

### Incident response (INC)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-INC-01 | Provide the incident response plan summary, the severity scale, and the date of the last exercise. | Must | Analyst | new | Plan summary; exercise record |
| FU-INC-02 | List security incidents in the last three years that affected customer data, with root cause and customer notification time. | Must | TPRM lead | new | Incident list |
| FU-INC-03 | Will you notify the bank within 24 hours of confirming an incident affecting its data? If not, what can you commit to? | Must | Compliance | FND-16 | Contract language |
| FU-INC-04 | Will you share the root cause report for incidents affecting the bank? | Should | Analyst | new | Contract language |

### Business continuity and disaster recovery (BCD)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-BCD-01 | Provide the business impact analysis and the recovery objectives for the connector and the booking platform. | Should | Analyst | V5 | Impact analysis summary |
| FU-BCD-02 | Provide the latest disaster recovery test report, including actual recovery times. | Must | Analyst | FND-10 | Test report |
| FU-BCD-03 | Provide the last backup restore test and show that backups are stored separately from production. | Must | IT security | new | Restore test record; account structure |
| FU-BCD-04 | What is the plan if your cloud provider's region is unavailable for more than a day? | Should | TPRM lead | new | Continuity plan |

### Privacy (PRV)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-PRV-01 | Provide the record of processing for the bank's data and your process for data subject requests. | Must | DPO | new | Processing record; request procedure |
| FU-PRV-02 | Provide transfer impact assessments for India, the US email and monitoring providers, and the AI provider. | Must | DPO | FND-03 | Impact assessments |
| FU-PRV-03 | How is the bank's data deleted at contract end, including backups, and how is it evidenced? | Must | DPO | FND-15 | Deletion procedure; certificate sample |

### Governance, risk and compliance (GRC)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-GRC-01 | Provide the SOC 2 exceptions, the carved-out subservice organisations and the customer controls you expect the bank to operate. | Must | Analyst | L1 | Exception list; customer control list |
| FU-GRC-02 | Provide the cyber insurance certificate and compare the cover with the liability cap in the contract. | Must | Finance | new | Insurance certificate; contract cap |
| FU-GRC-03 | Provide audited financial statements for the last two years and any going-concern notes. | Should | Finance | new | Audited accounts |
| FU-GRC-04 | Provide the anti-bribery and sanctions policy and training records, and say whether any investigation exists. | If applicable | Compliance | new | Policy; training records |

### Change and configuration management (CHG)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-CHG-01 | How are changes to production approved, tested and rolled back, and how are emergency changes handled? | Must | IT security | new | Change procedure |
| FU-CHG-02 | How do you detect and handle configuration drift on the connector and platform baselines? | Should | IT security | new | Drift reports |
| FU-CHG-03 | Will you notify the bank before changes that affect its integration (IP addresses, interfaces, new modules, new fourth parties)? | Must | Analyst | FND-12 | Contract language |

### People security and endpoints (PPL)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-PPL-01 | What background screening applies to staff with access to customer data, including the offshore support team? | Must | Compliance | new | Screening policy; verification samples |
| FU-PPL-02 | Provide security training completion rates and phishing exercise results for staff with production access. | Should | Analyst | new | Training metrics |
| FU-PPL-03 | How are leavers' access and laptops handled within 24 hours, and how are endpoints protected (EDR, disk encryption, local admin rights)? | Must | IT security | new | Leaver sample; endpoint report |

### Infrastructure security (INF)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-INF-01 | How are hosts hardened (baselines, golden images), and how are administrative ports exposed? | Should | IT security | new | Hardening baseline; admin access design |
| FU-INF-02 | How can the cloud provider's staff reach customer data, and what controls apply? | Must | IT security | FH | Provider access description |

### Physical security (PHY)

| ID | Question | Priority | Asked by | Linked to | Evidence to request |
|---|---|---|---|---|---|
| FU-PHY-01 | Provide the cloud provider's data centre assurance reports and confirm the locations used for the bank's data. | Should | Analyst | V6 | Provider reports; location list |
| FU-PHY-02 | Describe physical access controls at your offices and the India support site. | If applicable | IT security | new | Site description |

## 6. Part D: questions from the initial assessment that were not assessed (23)

These were lower priority in the initial assessment. Please answer them in the same reply.

| ID | Question |
|---|---|
| A1 | Is the service multi-tenant SaaS, single-tenant cloud, or self-hosted? Which edition and version are we buying? |
| A2 | Which data categories will the service store or process (employee data, passport/ID numbers, financial data)? |
| B4 | What session timeout, re-authentication and device or network restrictions apply? |
| C1 | How are accounts created (SCIM, API, manual, self-signup)? Is self-signup disabled? |
| C3 | How are role changes (movers) reflected in groups, roles and entitlements? |
| C4 | How are seats assigned and reclaimed, and are dormant accounts reported? |
| E1 | Which employee fields are received, and are they limited to the minimum needed? |
| E2 | What method (REST, webhook, SFTP) and direction is used, and who initiates the connection? |
| F1 | How are policy rules defined, approved and version-controlled? |
| F2 | How is an approval request authenticated so it cannot be forged or replayed? |
| F3 | Is segregation of duties enforced (a requester cannot approve their own booking)? |
| F4 | How does the platform stop users who are not authorised bookers from creating bookings, and how is the sponsor's approval enforced for guest travel? |
| G3 | How are payment details and supplier data protected against tampering? |
| H2 | Which TLS versions and cipher policy are used? Is mutual TLS available for APIs? |
| H3 | How are APIs authenticated (OAuth, keys), scoped and rate-limited? |
| I3 | What are the retention, deletion and return rules at contract end, including backups? |
| I4 | How is sensitive personal data (passport, ID, emergency contacts) protected (masking, field-level encryption)? |
| J2 | Can we export logs to our SIEM in near real time? |
| J3 | How are suspicious events detected, and how are we alerted? |
| K2 | How are subprocessors assessed, and how are we notified of changes? |
| L3 | What are the vulnerability management and patching timelines? |
| N2 | Does the vendor commit to cooperate with our competent and resolution authorities? |
| N6 | Will the vendor take part in our security awareness and resilience training where required? |


## 7. Totals

| Part | Count |
|---|---|
| A. Evidence for open findings | 22 |
| B. Physical specification | 5 points and 4 evidence groups |
| C. New questions | 65 |
| D. Re-asked questions | 23 |
| E. Bank outside-in checks and own actions | 10 and 13 |
