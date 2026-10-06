# Stage 1: Business process, scoping and inherent risk

> **Fictional case study.** Example Bank and Vendor X are placeholders. All figures are assumptions made for this exercise. Legal references are indicative and must be checked against the official texts.

## 1. Why this service exists

Example Bank is headquartered in the EU, operates in several EU member states and in other regions (Asia, wider EMEA, and the US and Mexico), and has about 20,000 employees (assumption). Today employees book travel by email and spreadsheet, which is slow and hard to control. Vendor X is a corporate travel management platform delivered as SaaS. It would:

- enforce the bank's travel policy by employee grade
- connect to the HR system so that only current employees can book
- return approved trips and booking references to the HR portal
- calculate the daily allowance by designation, destination and trip length
- register the trip with the company-wide travel insurance
- send one monthly invoice to the bank's finance system for payment

### Departments and their role

| Department | Role in this process | Why it matters for the assessment |
|---|---|---|
| HR (business owner) | Owns policy, approvals, employee data | Source of personal data |
| Finance and Accounting | Invoices, cost centres, daily allowance posting, month-end reconciliation | Financial integrity, rate tables, fraud risk |
| Payroll (or expense system) | Pays daily allowances to employees | Payment accuracy, tax treatment |
| HR benefits, Insurance and Risk | Owns the company-wide travel insurance and emergency assistance | Coverage, data shared with the insurer, claims |
| Executive office | Books senior management and VIP travel, and guest travel on behalf of guests | Confidentiality of itineraries |
| Procurement | Contract and commercial terms | Contract clauses, exit |
| IT and Security | Identity, connector, integration | Technical controls |
| Privacy (DPO) | Lawful basis, transfers, DPIA | Employee, guest and recipient data |
| Compliance | Gifts and hospitality, sanctions, regulatory classification | Policy compliance |
| TPRM | Runs the assessment and risk decision | This case study |

## 2. Scope

### 2.1 In scope

| ID | Service | Note |
|---|---|---|
| S1 | Booking of flights, rail, hotels and ground transport for business trips | Core service |
| S2 | Senior management and VIP travel | Special handling, see 2.4 |
| S3 | Visa support for non-EU travel | Passport data goes to visa agencies, see 2.5 |
| S4 | Company-wide travel insurance cover and emergency assistance | Trip registered with the bank's group insurer, see 2.8 |
| S5 | Guest travel for non-employees | Booked by a bank employee, see 2.6 |
| S6 | Approval against the travel policy | Through the HR portal |
| S7 | Monthly invoicing and settlement to the bank's ERP | Finance flow |
| S8 | Employee roster sync and single sign-on | Identity and data feed |
| S9 | Miscellaneous business expenses: gifts, flowers, bouquets, awards | Treated as another valid business expense, see 2.7 |
| S10 | Virtual cards to pay for bookings | Brings card data and PCI DSS into scope |
| S11 | Loyalty programmes and discounts: frequent flyer numbers, corporate discounts | Personal data and a fraud and ownership question, see 2.9 |
| S12 | Daily allowance (per diem) by designation | Finance and payroll involvement, see 2.10 |

**Regions:** the platform is used by employees in the EU, Asia, wider EMEA, and the US and Mexico. Data moves across regions.

### 2.2 Out of scope

- Personal vacation and leisure travel (a business trip extended privately is booked and paid by the employee outside the platform, assumption)
- Long-term relocation and international assignments
- Event organisation (venues, catering, conference management)

### 2.3 Trip purposes covered (business trips only)

| Trip type | Examples | Scoping note |
|---|---|---|
| Trade fairs and conferences | Industry events, speaker attendance | Group bookings possible |
| Business development and client meetings | Relationship manager visits | The trip purpose field must not contain client names or deal details (banking secrecy, possible market-sensitive information) |
| Internal visits | Head office to branches, subsidiaries or other offices | Routine |
| Executive visits | CEO or managing director visits to offices or subsidiaries, board travel | Sensitive itineraries, see 2.4 |
| Training and certification | External courses | Routine |
| Regulator and audit-related meetings | Staff attending supervisory or audit meetings | Itineraries may reveal supervisory activity |

### 2.4 Senior management travel (special attention)

Executive itineraries raise the inherent risk because:

- Movements of the CEO or board members are a **physical-safety** matter.
- A trip to a particular city can signal **market-sensitive** activity, for example a planned acquisition or a regulatory meeting.
- Executives are prime targets for **phishing and impersonation**, and travel details make those attacks more convincing.
- VIP profiles often hold preferences and personal contacts.

Controls to test later: restricted visibility of VIP itineraries, limited access for vendor support staff, masking of the trip purpose, alerts on unusual access.

### 2.5 Visa support for non-EU travel

Visa handling is where the most sensitive documents leave the bank. A visa application can involve a passport copy, a photo, date of birth, home address, and sometimes an employment letter. The platform usually passes these to a **visa agency**, which is a fourth party. The bank needs to know which agency is used, where it is located, and how documents are deleted afterwards.

### 2.6 Guest bookings (non-employees)

Guests are people who are not in the HR system but whose travel the bank pays for, for example external auditors, consultants and advisers, advisory or supervisory board members, and senior visitors attending meetings.

- **The guest has no access to the platform.** A bank employee (the booker, for example an executive assistant) uses the portal and enters the guest's details.
- The booking is approved by a named **bank sponsor**.
- Confirmations and tickets go to the **booker**, who passes them on (assumption, so that no external email address is held as a platform user).
- Guest data does **not** arrive through the HR sync, so the **legal basis** and **retention** must be confirmed with the privacy team.
- Paying travel for **external auditors or supervisory staff** may be restricted by the bank's independence and anti-bribery rules. Compliance must confirm before go-live.

### 2.7 Miscellaneous business expenses: gifts, flowers, awards

These are included as an optional service, classed as another valid business expense and not as travel. They add risk, so the following apply:

- Purchases follow the bank's **gifts and hospitality policy**: approval, value limits and a business reason.
- No gifts to **public officials or supervisory staff** without compliance approval.
- An **audit trail** records who ordered what, for whom, and at what cost.
- Recipient data (name, delivery address) is personal data of a third party (D12).
- A **florist or gift supplier** becomes a new fourth party.

### 2.8 Company-wide travel insurance

The bank provides group travel cover for employees on business trips (for example accident, medical, evacuation and assistance). The platform registers each trip with the **group insurer**, which receives traveller data (name, date of birth, passport, itinerary). Assumption: only the bank's group policy is used. Insurance sold separately through the platform is not in scope.

The group insurer is a **third party of the bank** that receives data **through the vendor**. Insurance data can include health information if assistance is requested (D15).

### 2.9 Loyalty programmes and discounts

Employees may add frequent flyer or hotel loyalty numbers, and the bank may hold corporate discount agreements. Questions to settle: who owns the points (the employee or the bank), how personal loyalty accounts are protected, and how discount codes are kept from misuse. Loyalty data also reveals travel patterns (D13).

### 2.10 Daily allowance by designation

Employees receive a daily allowance that depends on grade, destination and trip length. The platform calculates the entitlement from the bank's rate table, and the bank's expense or payroll system pays it (assumption: **the vendor never pays employees**). Finance owns the rate table and posts the costs. A wrong rate or a changed rate table leads to financial leakage, fraud or tax errors, so rate-table changes need control and an audit trail. Tax treatment of allowances is country-specific.

## 3. The business process

| Step | What happens | Systems involved |
|---|---|---|
| A | Nightly sync of the employee roster (read-only, agreed fields) | HR system, connector, vendor roster |
| 1 | Employee submits a trip request | HR portal |
| 2 | Line manager approves the request | HR portal |
| 3 | Approved trip is sent to the travel platform | HR portal, connector, vendor platform |
| 4 | Platform checks the trip against policy and the roster | Vendor platform |
| 5 | Platform books flights, hotels, transport and visas with suppliers | Vendor platform, suppliers |
| 6 | Booking reference returns to the employee | Vendor platform, connector, HR portal |
| 7 | Vendor sends the monthly invoice, one line per trip | Vendor invoicing, bank ERP |
| 8 | Bank pays the invoice | Bank ERP, vendor invoicing |
| 9 | Trip is registered with the group insurer and the employee receives cover details | Vendor platform, group insurer |
| 10 | Daily allowance is calculated from grade, destination and days | Vendor platform, bank rate table |
| 11 | Allowance is paid through payroll or the expense system and posted by Accounting | Expense or payroll system, bank ERP |
| 12 | Virtual card is issued for a booking and settled at month-end | Vendor platform, card provider, bank ERP |

Steps 9 to 12 run alongside steps 5 to 8.

**Guest variant:** a bank sponsor approves the request and a booker enters the guest's data (replacing steps 1 and 2). Steps 3 to 9 and 12 are the same. There is no daily allowance (step 10 and 11) unless the bank's policy provides one.

**Miscellaneous expense variant:** an authorised employee orders a gift, which is approved under the gifts policy and then invoiced through steps 7 and 8.

These step IDs are reused in the data-flow table in stage 3.

## 4. Data in scope

| ID | Data | Used for | Sensitivity |
|---|---|---|---|
| D1 | Employee ID, name, grade, cost centre, manager, employment status, work location | Roster, policy, approval routing | Medium |
| D2 | Name as on passport, gender, passport or ID number, expiry, nationality | Tickets, visas, insurance | High |
| D3 | Date of birth | Tickets, insurance | High |
| D4 | Trip details (dates, destinations, purpose) | Bookings | Medium, **High for executives** |
| D5 | Booking references | Confirmation | Low |
| D6 | Invoice data (trip reference, cost centre, amount) | Settlement | Medium (financial) |
| D7 | Integration credentials and tokens | Authentication between systems | High |
| D8 | Visa application data (photo, passport copy, possibly an employment letter) | Visa support | High |
| D9 | Special requests (meals, mobility or medical assistance) | Booking | High (may reveal health or religion, special-category data under GDPR Art 9) |
| D10 | Guest data (name, employer, email, passport) | Guest travel | High |
| D11 | Contact details, home address, emergency contact | Visas, insurance, traveller support | Medium to High |
| D12 | Gift recipient data (name, delivery address) | Miscellaneous expenses | Medium (third-party data) |
| D13 | Loyalty and frequent flyer numbers | Discounts, points | Medium |
| D14 | Virtual card data (card number or token, limit, expiry) | Payment | High (payment data) |
| D15 | Insurance data (certificate, policy reference, assistance requests, possibly health details) | Cover and claims | High |
| D16 | Allowance data (grade, destination, days, amount) | Daily allowance | Medium (financial, reveals grade) |

**Data minimisation:** gender and home address are sent only where a visa form, airline or insurer requires them. They are not part of the nightly roster sync. Assumption: passport data (D2, D3) is held in the HR system and sent only when a booking needs it.

## 5. Inherent risk rating

Inherent risk means the risk before any vendor controls are considered. Each factor is scored 1 (low), 2 (medium) or 3 (high). The scoring is simple and unweighted.

| ID | Factor | Score | Reason |
|---|---|---|---|
| F1 | Data sensitivity | 3 | Name, gender, home address, passport, date of birth, visa documents, card data, possible health data |
| F2 | Data volume and spread | 3 | About 20,000 employees across several regions, plus guests and gift recipients |
| F3 | Integration depth | 3 | HR, approvals, ERP, payroll or expense system and the insurer |
| F4 | Fourth-party exposure | 3 | Airlines, hotels, visa agencies, insurers, card provider, gift suppliers, hosting |
| F5 | Executive and VIP exposure | 3 | Senior management itineraries |
| F6 | Business, duty-of-care and reputational impact | 3 | Travellers abroad rely on assistance, and a breach of executive or passport data would damage the bank's reputation |
| F7 | Financial exposure | 3 | Virtual cards, monthly invoices, daily allowance rates |
| F8 | Regulatory exposure | 3 | DORA, GDPR, and rules in several regions |
| F9 | Substitutability | 1 | Many travel platforms exist |
| | **Total** | **25 of 27** | |

**Bands:** 9 to 13 low, 14 to 18 medium, 19 to 23 high, 24 to 27 very high.
**Result: very high inherent risk.**

## 6. Criticality classification

Question: would a disruption seriously impair the bank's financial performance, soundness, continuity of services, regulatory compliance, **or reputation**?

DORA's own definition of a critical or important function (Art 3(22)) refers to financial performance, soundness, continuity and compliance. Reputational damage is not named there. Banks normally include it in their **internal** impact criteria, so this case study records it as an internal criterion.

| Test | Answer | Reasoning |
|---|---|---|
| An outage stops a regulated or customer-facing service | No | Travel booking is an internal support process |
| A workable fallback exists | Partly | Phone agent and direct booking, but not for emergency assistance abroad or for virtual-card payments |
| Duty of care to travellers | Yes | Staff abroad rely on cover and assistance |
| Reputational damage from a failure or breach | **Yes** | Executive itineraries and passport data of a global workforce |
| Scale and spread | Yes | Several regions, large workforce |

**Decision (author): classified as a critical or important function.**

Note for interviews: many banks would class a plain travel booking tool as non-critical. This case study chooses critical because of the duty of care, reputational impact and global scale, and it states that reasoning openly. In a real bank, the business and compliance teams decide.

## 7. Applicable regulations and what the bank requires from the vendor

The bank is the regulated party. It assesses the vendor to meet its own obligations.

| ID | Source | Why it applies | What the bank assesses | Evidence to request |
|---|---|---|---|---|
| R1 | DORA, Regulation (EU) 2022/2554 | The platform is an ICT service (Art 3(21)) that supports a critical or important function | Register of information entry (Art 28(3)), pre-contract assessment (Art 28(4)), full contract terms (Art 30(2) and 30(3)), exit strategy (Art 28(8)), access and data security (Art 9) | Contract terms, subprocessor list, service levels, incident assistance, audit rights, exit plan |
| R2 | GDPR | EU employee, guest and recipient data. Bank is controller, vendor is processor | Processing agreement (Art 28), security (Art 32), minimisation (Art 5), transfers outside the EU (Arts 44 to 49), breach notice (Art 33), DPIA (Art 35) | Data processing agreement, subprocessor list, transfer mechanism, retention schedule, DPIA input |
| R3 | EBA guidelines on outsourcing (EBA/GL/2019/02) | Applies because the arrangement is treated as outsourcing of a critical or important function (A8) | Due diligence, outsourcing register, exit, audit rights, sub-outsourcing | Due diligence file, contract |
| R4 | Bank internal policies | Third-party risk, information security, data classification, travel and expense | Alignment with the bank's own standards | Vendor policy statements |
| R5 | Anti-bribery rules and the gifts and hospitality policy | Guest bookings (auditors, officials) and gifts (S9) | Approval rules, value limits, audit trail | Workflow evidence |
| R6 | Sanctions and restrictive measures (internal compliance policy) | Destinations and suppliers | Whether restricted destinations can be flagged | Configuration evidence |
| R7 | PCI DSS (industry standard) | Virtual cards (S10) put card data in scope | Vendor and card provider compliance | Attestation of compliance |
| R8 | ISO/IEC 27001 and SOC 2 | Not laws, but the main way vendors evidence controls | Whether scope covers this service | Certificate or report, bridge letter |
| R9 | Regional rules outside the EU (Asia, wider EMEA, US, Mexico) | Local staff, local regulators and local data laws | Local data protection and data localisation limits, and local third-party or outsourcing rules | Regional compliance mapping |
| R10 | Tax and payroll rules on daily allowances | Allowance rates differ by country | Rate-table accuracy and audit trail | Rate-table configuration, change log |
| R11 | NIS2, Directive (EU) 2022/2555 | May apply to the vendor as a service provider. For the bank, DORA is the specific rule | Not mapped question by question. Applicability to be verified | To be confirmed after verification |

**Examples for R9 (to be verified):** the UK PRA expectations on outsourcing and third-party risk, the US interagency guidance on third-party relationships, and the Singapore MAS outsourcing guidelines. Each country needs its own check.

**Group view:** DORA applies to the EU financial entities. Non-EU branches and subsidiaries may fall under local regulators. The bank may need one group assessment plus local addenda.

## 8. Assumption A2 and A8, explained

Two different questions are asked about the same vendor:

| Question | Test | Answer here |
|---|---|---|
| Is it an ICT service under DORA? | Does the vendor provide digital or data services through ICT systems on an ongoing basis? | **Yes**. It is a cloud platform with SSO, HR sync and an ERP link |
| Is it outsourcing? | Does the vendor perform a process or service the bank would otherwise perform itself? | **Yes**. Booking, policy checks, visa support and allowance calculation are things the bank does today by email and spreadsheet |
| Does the vendor access our data or systems? | Does the vendor receive bank data or connect to bank systems? | **Yes** (HR data, ERP link). This raises the risk, but it is not the legal test itself |

Result: the arrangement is an ICT service and also outsourcing of a critical or important function. The bank may need to **inform its supervisor before signing** (DORA Art 28(3)). Compliance confirms this.

Buying an airline seat or a hotel night is a purchase of goods or services, not outsourcing. The platform that manages the process around it is the outsourced part.

## 9. Assessment tier

| Tier | Condition | Depth |
|---|---|---|
| **1** | Supports a critical or important function | Full assessment, audit rights, exit plan, resilience testing cooperation |
| 2 | Not critical, but high on data, fourth-party or executive exposure | Full questionnaire, evidence verification, baseline contract review |
| 3 | Everything else | Lightweight questionnaire and certificate check |

**Assigned: Tier 1.**

Focus areas for later stages:

1. Data protection, including cross-border transfers and passport data
2. Fourth parties and the data each receives (airlines, visa agencies, insurers, card provider, gift suppliers)
3. Identity, access and vendor staff access to executive itineraries
4. The connector, its credentials, and the invoice path
5. Virtual cards and PCI DSS evidence
6. Daily allowance rate-table integrity
7. Hand-off to the group insurer and emergency assistance
8. DORA Art 30(2) and 30(3) contract terms, audit rights and exit plan
9. Business continuity, disaster recovery and incident support
10. Regional compliance for non-EU staff

## 10. Assumptions and decisions

| ID | Decision | Source |
|---|---|---|
| A1 | Bank is EU-headquartered with operations in the EU, Asia, wider EMEA, and the US and Mexico. About 20,000 employees | confirm (size is an assumption) |
| A2 | The platform is an ICT service under DORA | confirm, see section 8 |
| A3 | Classified as a critical or important function | confirm |
| A4 | Tier 1 | Follows from A3 |
| A5 | Gifts, flowers and awards are in scope as miscellaneous business expenses, with controls | confirm |
| A6 | Guests are in scope. The guest has no access. A bank employee books on the guest's behalf | confirm |
| A7 | Virtual cards and loyalty or frequent flyer programmes are in scope. PCI DSS applies | confirm |
| A8 | The arrangement is treated as outsourcing as well as an ICT service | confirm, see section 8 |
| A9 | Daily allowance is calculated by the platform and paid by the bank's payroll or expense system. The vendor does not pay employees | Assumption |
| A10 | Insurance is the bank's group policy. The platform registers trips with the group insurer | Assumption |
| A11 | Guest confirmations go to the booker, not to the guest | Assumption |

## 11. Output and handoff

- Inherent risk: **very high (25 of 27)**
- Criticality: **critical or important function**
- Tier: **1**
