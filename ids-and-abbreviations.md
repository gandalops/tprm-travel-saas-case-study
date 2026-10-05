# Guide to the IDs and abbreviations

> **Fictional case study.** Example Bank and Vendor X are placeholders, and all vendor data is simulated. This guide explains the short codes used in all five stages, so a reader can follow any item from the architecture to the decision.
>
> **Status:** Draft for author review.

## 1. The idea in 30 seconds

Every item in the case study has a short ID: a letter code and a number. The letter says what kind of item it is, and the number says which one. For example, **V7** is vendor claim 7, **X2** is architecture observation 2, **CR-03** is control requirement 3, and **FND-01** is finding 1. Because the IDs repeat from stage to stage, you can follow one thread end to end:

**Flow, observation or claim, risk, control, framework reference, question, vendor answer, finding, decision.**

## 2. Quick reference: what each code means

| Code | Stands for | Range | Defined in | Example |
|---|---|---|---|---|
| **S** | Scope item | S1 to S12 | Stage 1 | S3: visa support |
| **D** | Data type | D1 to D16 | Stage 1 | D2: passport details |
| **F** (Stage 1) | Inherent risk factor | F1 to F9 | Stage 1 | F5: executive and VIP exposure |
| **R** | Regulation or standard | R1 to R11 | Stage 1 | R1: DORA |
| **A** | Assumption or decision | A1 to A16 | Stages 1 to 3 | A3: critical function |
| **V** | Vendor claim | V1 to V13 | Stage 2 | V7: connector secrets are in a vault |
| **FP** | Fourth party | FP1 to FP11 | Stage 2 | FP6: Card Provider Y |
| **Z** | Trust zone | Z1 to Z5 | Stage 3 | Z3: vendor cloud |
| **FW** | Firewall boundary | FW1 to FW3 | Stage 3 | FW1: bank edge |
| **FS, FA, F1 to F12, FG, FN, FL, FH, FV, FI** | Data flow | see section 7 | Stage 3 | FA: nightly roster pull |
| **X** | Architecture observation | X1 to X12 | Stage 3 | X2: connector holds several credentials |
| **CR** | Control requirement | CR-01 to CR-28 | Stage 4 | CR-03: credential storage |
| **A to W** (one letter and a number) | Question (domain letter and number) | 87 questions | Stage 4 | E3, O3 |
| **Q-** | Question prefix in the traceability matrix | Q-E3 | Stages 4 and 5 | Q-O3 |
| **EV** | Evidence item | EV-01 to EV-25 | Stage 5 | EV-06: secrets procedure and access list |
| **FND** | Finding | FND-01 to FND-22 | Stage 5 | FND-01: wide access to credentials |
| **RR** | Risk in the risk register | RR-01 to RR-17 | Stage 5 | RR-01: stolen connector credential |
| **REM** | Remediation action | REM-01 to REM-22 | Stage 5 | REM-02: rotate credentials |
| **KRI** | Key risk indicator | KRI-01 to KRI-13 | Stage 5 | KRI-01: days since rotation |
| **T** | Traceability thread | T-01 to T-20 | Stage 5 | T-01: credential storage |
| **PF** | Change after the freeze | PF-1 | Stage 5 | PF-1: the AI provider |
| **EX** | Example row in the questionnaire | one row | Stage 4 | Row 6 |

**Watch out:** **R is regulation, not risk.** Risks use **RR**. The letters D, F and R are also used for questions or flows, so always read the code in context (see section 11).

## 3. Stage 1 codes

**S: scope items**

| ID | In scope |
|---|---|
| S1 | Booking of flights, rail, hotels and ground transport |
| S2 | Senior management and VIP travel |
| S3 | Visa support for non-EU travel |
| S4 | Company-wide travel insurance and emergency assistance |
| S5 | Guest travel for non-employees |
| S6 | Approval against the travel policy |
| S7 | Monthly invoicing and settlement |
| S8 | Employee roster sync and single sign-on |
| S9 | Miscellaneous business expenses (gifts, flowers, awards) |
| S10 | Virtual cards |
| S11 | Loyalty programmes and discounts |
| S12 | Daily allowance by designation |

**D: data types**

| ID | Data | ID | Data |
|---|---|---|---|
| D1 | Employee identity | D9 | Special requests (meals, mobility, medical) |
| D2 | Passport details | D10 | Guest data |
| D3 | Date of birth | D11 | Contact details and home address |
| D4 | Trip details | D12 | Gift recipient data |
| D5 | Booking references | D13 | Loyalty numbers |
| D6 | Invoice data | D14 | Virtual card data |
| D7 | Credentials and tokens | D15 | Insurance data |
| D8 | Visa application data | D16 | Allowance data |

**F: inherent risk factors** (each scored 1 to 3, total 25 of 27)

F1 data sensitivity, F2 data volume and spread, F3 integration depth, F4 fourth-party exposure, F5 executive and VIP exposure, F6 business, duty-of-care and reputational impact, F7 financial exposure, F8 regulatory exposure, F9 substitutability.

**R: regulations and standards**

| ID | Source |
|---|---|
| R1 | DORA (Regulation (EU) 2022/2554) |
| R2 | GDPR |
| R3 | EBA guidelines on outsourcing |
| R4 | The bank's internal policies |
| R5 | Anti-bribery rules and the gifts and hospitality policy |
| R6 | Sanctions and restrictive measures |
| R7 | PCI DSS |
| R8 | ISO/IEC 27001 and SOC 2 |
| R9 | Regional rules outside the EU |
| R10 | Tax and payroll rules on daily allowances |
| R11 | NIS2 |

**A: assumptions and decisions**

| ID | Decision |
|---|---|
| A1 | EU-headquartered bank with operations in the EU, Asia, wider EMEA, and the US and Mexico |
| A2 | The platform is an ICT service under DORA |
| A3 | Critical or important function |
| A4 | Tier 1 |
| A5 | Gifts and flowers are in scope as miscellaneous business expenses |
| A6 | Guests are in scope. They have no access, and a bank employee books for them |
| A7 | Virtual cards and loyalty programmes are in scope, so PCI DSS applies |
| A8 | Treated as outsourcing as well as an ICT service |
| A9 | The platform calculates the allowance and the bank's payroll pays it |
| A10 | Insurance is the bank's group policy |
| A11 | Guest confirmations go to the booker |
| A12 | The vendor operates the connector (Stage 2) |
| A13 | Finance admins edit the allowance rate table in the vendor console (Stage 3) |
| A14 | The vendor pushes invoices to the ERP intake (Stage 3) |
| A15 | Payment itself uses the bank's normal channels (Stage 3) |
| A16 | Users reach the vendor by browser with SSO (Stage 3) |

**Process steps:** step **A** is the nightly roster sync, and steps **1 to 12** are the business process (request, approval, booking, invoice, payment, insurance, allowance, virtual card).

## 4. Stage 2 codes

**V: vendor claims** (a claim stays a claim until evidence is seen)

| ID | The vendor says |
|---|---|
| V1 | ISO 27001 certified |
| V2 | SOC 2 Type II report |
| V3 | PCI DSS compliant |
| V4 | Annual penetration test |
| V5 | Recovery time 4 hours, recovery point 1 hour |
| V6 | Data stored only in the EU |
| V7 | Connector secrets are kept in a vault |
| V8 | Support access is logged |
| V9 | Subprocessor changes are announced |
| V10 | No real data in test environments |
| V11 | Customer data is encrypted |
| V12 | Customer tenants are separated |
| V13 | AI features are used, and customer data is not used to train models |

**FP: fourth parties** (suppliers of the vendor)

| ID | Fourth party | ID | Fourth party |
|---|---|---|---|
| FP1 | Cloud hosting provider | FP7 | Gifts and florist marketplace |
| FP2 | Airlines and GDS | FP8 | Emergency assistance partner |
| FP3 | Hotels and ground transport | FP9 | Email and SMS provider |
| FP4 | Visa agency network | FP10 | Monitoring and logging provider |
| FP5 | The bank's own group insurer | FP11 | AI model provider (added after Stage 5) |
| FP6 | Card Provider Y | | |

## 5. Stage 3 codes

**Z and FW: zones and boundaries**

| ID | Meaning |
|---|---|
| Z1 | Bank internal network |
| Z2 | Internet |
| Z3 | Vendor cloud |
| Z4 | Suppliers and insurer |
| FW1 | Bank edge firewall (the bank decides what comes in) |
| FW2 | Vendor edge firewall (the vendor controls it) |
| FW3 | Vendor to suppliers (the bank cannot enforce it) |

**Flows** (an arrow points from the system that opens the connection to the system that receives it)

| ID | Flow |
|---|---|
| FS | Single sign-on login |
| FA | Nightly roster pull by the connector (step A) |
| F1, F2 | Employee request and manager approval in the HR portal |
| F3 | Approved trip goes to the platform |
| F4 | Policy check inside the vendor |
| F5a to F5d | Supplier calls: airlines and GDS, hotels and ground, visa agency, gifts marketplace |
| F6 | Booking reference returns to the HR portal |
| F7 | Invoice from the vendor to the ERP |
| F8 | Remittance advice from the ERP to the vendor |
| F9 | Trip registered with the group insurer |
| F10 | Allowance rate table maintained by Finance |
| F11 | Allowance entitlement sent to the bank |
| F12 | Virtual card issued by Card Provider Y |
| FG | Guest booking by a bank employee |
| FN | Notifications by email and SMS |
| FL | Logs sent to the monitoring provider |
| FH | Hosting at the cloud provider |
| FV | Vendor support access to production data |
| FI | Platform to AI model provider (added after the freeze) |

**X: observations from the architecture**

| ID | Observation |
|---|---|
| X1 | Four openings into the bank, all opened from the vendor cloud |
| X2 | The connector holds credentials for several bank systems |
| X3 | The invoice path bypasses the connector |
| X4 | Single sign-on runs through the user's browser |
| X5 | Vendor support staff in India can reach production data |
| X6 | Providers FP9 and FP10 are in the US |
| X7 | Suppliers are outside the bank's contract |
| X8 | The group insurer is reached through the vendor |
| X9 | The allowance rate table is edited in the vendor console |
| X10 | Guest data is typed in by hand |
| X11 | The virtual card flow |
| X12 | The bank does not control FW3 |

## 6. Stage 4 codes

**CR: control requirements.** CR-01 to CR-28. Each says what must be true, for example CR-03: bank credentials are held in a vault, readable only by named roles, with access logged. Each CR is linked to its source (X, V or flow), to DORA, GDPR and ISO references, and to the questions that test it.

**Question IDs.** A question ID is a domain letter plus a number. The letter says the domain.

| Letter | Domain | Letter | Domain |
|---|---|---|---|
| A | Scope and service model | K | Subprocessors |
| B | Identity and sign-on | L | Assurance |
| C | Provisioning and leavers | M | Resilience and exit |
| D | Administration and access | N | Contract terms |
| E | HR data sync | O | Connector and credentials |
| F | Approvals and policy | P | Virtual cards |
| G | Financial sync | Q | Allowance, gifts and loyalty |
| H | Network and gateway | T | Regional and transfers |
| I | Data protection | U | Insurance hand-off |
| J | Logging and monitoring | W | AI and automation |

In the traceability matrix, questions are written with the prefix **Q-** (for example Q-E3), because the letters D, F and R are also used for data, factors and regulations.

## 7. Stage 5 codes

| Code | Meaning |
|---|---|
| EV | An evidence item received from the vendor, with its strength |
| FND | A finding: a gap or partial result, with a severity |
| RR | A risk in the risk register, scored before controls (inherent), as assessed (current) and after remediation (target) |
| REM | A remediation action with an owner, a date and the evidence needed to verify it |
| KRI | A key risk indicator monitored after go-live |
| T | A traceability thread, one row in the matrix |
| PF | A change after the freeze (PF-1: the AI provider) |

## 8. Ratings and scales

| Item | Values |
|---|---|
| Tier | 1 (critical or important function), 2 (high data or fourth-party risk, not critical), 3 (the rest) |
| Evidence strength | Strong (independent report or dated export or test), Medium (dated screenshot, policy with a sample), Weak (policy only or vendor statement) |
| Rating | Satisfactory, Partial, Gap, Not applicable |
| Finding severity | High (bulk personal data, fraudulent payment, access into the bank, or a mandatory contract term unmet), Medium, Low |
| Risk score | Likelihood times impact, each 1 to 5. Bands: Low 1 to 4, Medium 5 to 9, High 10 to 15, Very high 16 to 25 |
| Treatment | Mitigate, avoid, transfer, accept |

## 9. Abbreviations

| Abbreviation | Meaning |
|---|---|
| AI | Artificial intelligence |
| AP | Accounts payable |
| API | Application programming interface |
| BCP, DR | Business continuity plan, disaster recovery |
| DMZ | Demilitarised zone, a network area between two trust zones |
| DORA | Digital Operational Resilience Act |
| DPIA | Data protection impact assessment |
| DPO | Data protection officer |
| EBA | European Banking Authority |
| ERP | Enterprise resource planning (the finance system) |
| GDPR | General Data Protection Regulation |
| GDS | Global distribution system (airline booking network) |
| GRC | Governance, risk and compliance |
| HRIS | Human resources information system |
| ICT | Information and communication technology |
| IdP | Identity provider |
| ISMS | Information security management system |
| ISO 27001 | International standard for information security management |
| KRI | Key risk indicator |
| MFA | Multi-factor authentication |
| mTLS | Mutual TLS: both sides prove their identity |
| NIS2 | EU Directive on network and information security |
| OIDC, SAML | Protocols for single sign-on |
| PCI DSS | Payment Card Industry Data Security Standard |
| PII | Personally identifiable information |
| RTO, RPO | Recovery time objective, recovery point objective |
| SCIM | System for cross-domain identity management (automatic account provisioning) |
| SFTP | Secure file transfer protocol |
| SIEM | Security information and event management |
| SoA | Statement of Applicability (ISO 27001) |
| SOC 2 | Service organisation control report |
| SSO | Single sign-on |
| TIA | Transfer impact assessment |
| TLS | Transport layer security (encryption in transit) |
| TPRM | Third-party risk management |
| VIP | Very important person (senior management) |
| WAF | Web application firewall |

## 10. How to follow one thread

Take **T-01** (the connector credentials):

1. **Flow:** FA, the vendor-operated connector pulls the employee roster every night.
2. **Observation and claim:** X2 and V7.
3. **Risk:** RR-01, a stolen credential allows bulk reading of employee data.
4. **Control:** CR-03, credentials in a vault, readable only by named roles.
5. **Frameworks:** DORA Art 9, GDPR Art 32, ISO 27001 A.5.17 and A.8.24.
6. **Questions:** Q-E3 and Q-O3 (in the Questionnaire sheet, column A).
7. **Vendor answer and evidence:** a vault, but 11 staff can read it (EV-06). Rating: Partial.
8. **Finding and action:** FND-01 (High), REM-01.
9. **Decision:** mitigate, as a pre-go-live condition.

## 11. Same letter, different meaning

| Letter | Meanings, by where it appears |
|---|---|
| **D** | D1 to D16 is data (Stage 1). D1 to D5 as a question is the administration and access domain (Stage 4) |
| **F** | F1 to F9 is an inherent risk factor (Stage 1). F1 to F12 is a data flow (Stage 3). F1 to F4 as a question is the approvals domain (Stage 4) |
| **R** | R1 to R11 is a regulation (Stage 1). **RR** is a risk (Stage 5) |
| **A** | A1 to A16 is an assumption. A1 to A3 as a question is the scope domain |
| **S** | S1 to S12 is a scope item |
| **X** | X1 to X12 is an architecture observation |

If an ID has a hyphen and three letters or more (CR-, FND-, RR-, REM-, KRI-, EV-), it is unambiguous. For short IDs, read them in context, or look for the **Q-** prefix on questions.
