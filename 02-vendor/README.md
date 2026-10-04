# Stage 2: Vendor profile

> **Fictional case study. All vendor information in this document is simulated.** Vendor X, Card Provider Y and every figure, date and certificate below are invented for the exercise. Drafted with AI assistance, to be reviewed by the author.
>
> **Status:** Confirmed by author. Revised on 4 Oct 2026 to record decision A12 (the vendor operates the connector), claim V13 and early observation 9.
> **Builds on:** Stage 1 v1.0 (scope S1 to S12, data D1 to D16, Tier 1, critical or important function).

## 1. Purpose of this stage

Answer four questions about Vendor X before looking at architecture or controls:

1. Who are they, and are they a sound business to depend on?
2. What exactly do they offer, and how does it map to our scope?
3. Where do they host and operate, and who runs what?
4. What do they **claim**, and what would we need as **evidence**?

Rule used throughout: a vendor statement is a **claim** until the bank has seen evidence. Stage 5 tests the claims.

## 2. Who they are (simulated)

| Item | Vendor X (simulated) |
|---|---|
| Legal entity | Vendor X Travel Platform Ltd |
| Headquarters | Ireland (EU) |
| Founded | 2012 |
| Employees | About 900, offices in Ireland, India, Singapore and Mexico |
| Customers | About 600 corporate clients, including about 40 banks and financial institutions |
| Ownership | Private-equity owned since 2021 |
| Revenue and finances | About EUR 180 million revenue, profitable since 2024 |
| Cyber insurance | EUR 10 million cover |
| Adverse media and sanctions screening | No findings |
| Business model | Subscription fee per employee plus a transaction fee per booking |

## 3. Non-security due diligence

These checks sit beside the security assessment. A secure vendor that fails financially is still a risk to a Tier 1 service.

| Check | What we ask | Evidence to request | Why it matters |
|---|---|---|---|
| Legal and ownership | Who owns and controls the vendor? | Company registry extract, ownership chart | Sanctions and change-of-control risk |
| Financial health | Can the vendor stay in business for the contract term? | Audited accounts for the last 3 years | Failure would disrupt a critical service |
| Concentration | How much revenue depends on a few clients or suppliers? | Customer concentration statement | Dependency risk |
| Insurance | Is there cyber and professional liability cover? | Insurance certificates | Recovery after an incident |
| Litigation and adverse media | Any regulatory action, breach or lawsuit? | Declaration and independent search | Reputation and compliance |
| Ownership change | Is a sale or merger planned? | Contract clause on change of control | Continuity |

## 4. What they offer, mapped to our scope

| Scope ID | Vendor module (simulated) | How it works |
|---|---|---|
| S1 | Booking engine | Flights through GDS and direct airline connections, rail, hotels, ground transport |
| S2 | VIP desk | Restricted profiles, named agents, itinerary visibility limited to chosen users |
| S3 | Visa module | Application packs prepared by the platform and submitted by a partner visa agency |
| S4 | Insurance and assistance | Trip registered with the bank's group insurer by API, 24/7 traveller assistance line |
| S5 | Guest profiles | Created by a bank booker, no guest login |
| S6 | Policy and approval engine | Policy rules by grade, approval calls to the bank's HR portal |
| S7 | Invoicing | One monthly invoice with a line per trip, sent to the bank's ERP |
| S8 | Identity and roster | SAML and OIDC single sign-on, nightly roster sync through the connector |
| S9 | Gifts marketplace | Orders flowers and gifts from partner suppliers |
| S10 | Virtual cards | Single-use cards per booking, issued by Card Provider Y |
| S11 | Loyalty wallet | Stores frequent flyer numbers and applies corporate discounts |
| S12 | Allowance engine | Calculates the daily allowance from the bank's rate table |

## 5. Where and how they operate

### 5.1 Hosting (simulated)

| Item | Claim |
|---|---|
| Cloud provider | A major public cloud provider, EU regions |
| Primary and secondary region | Two EU regions in different countries, active and standby |
| Data location | All customer data stored in the EU |
| Environments | Production, staging, test. Claim: no real personal data in test |
| Tenancy | Multi-tenant platform, logical separation by tenant ID |
| Backups | Encrypted, kept 35 days, stored in the secondary region |

### 5.2 Operating model

| Item | Claim |
|---|---|
| Support | 24/7 follow-the-sun support from Ireland and India |
| Support access to customer data | Through a controlled admin tool, with logging |
| Emergency assistance line | Operated by a partner, see FP8 |
| Software releases | Weekly releases through a pipeline with automated tests |
| Connector | **Operated by the vendor**, one dedicated instance per client in the vendor's cloud (decision A12). The bank supplies a read-only service account and an approval endpoint |

## 6. Assurance claimed (simulated)

| ID | Certification or report | What the vendor states | Date |
|---|---|---|---|
| V1 | ISO/IEC 27001:2022 | Certificate covers the core platform and hosting | Valid until March 2027 |
| V2 | SOC 2 Type II | Report covers security and availability for the core platform | Audit period ended 31 Dec 2025 |
| V3 | PCI DSS v4.0 | Vendor states it is compliant for the card module | Date not given |
| V4 | Penetration test | Annual external test by an independent firm | Latest June 2026 |
| V5 | Business continuity | Recovery time 4 hours, recovery point 1 hour, tested yearly | Last test 2025 |

## 7. Claims register

Each row is something the vendor says. The last column shows what the bank must check, so the claim can become a verified fact or a finding.

| ID | Claim | Source | Evidence to request | What to verify |
|---|---|---|---|---|
| V1 | ISO 27001 certified | RFP response | Certificate and scope statement | Does the scope include the visa, gifts and card modules and the support locations? |
| V2 | SOC 2 Type II | Trust page | Full report, bridge letter | The audit period ended ten months ago. Is there a bridge letter for January to October 2026? Which modules are in scope? |
| V3 | PCI DSS compliant | RFP response | Attestation of compliance for the vendor and for Card Provider Y | Whose attestation is it, and does it cover the vendor's own handling of card data? |
| V4 | Annual penetration test | Security whitepaper | Test summary and remediation status | Were all high findings fixed? Does it cover the connector and APIs? |
| V5 | RTO 4 hours, RPO 1 hour | RFP response | BCP and disaster recovery test report | Was the failover actually tested, and did it meet the targets? |
| V6 | Data stored only in the EU | RFP response | Hosting evidence, data flow diagram | Does support access from India or any subprocessor in the US count as a transfer? |
| V7 | Connector secrets are kept in a vault | Security whitepaper | Secrets management procedure | How often are secrets rotated, and who can read them? Vendor says "annually or on request" |
| V8 | Support access is logged | RFP response | Sample access logs | Can vendor support staff view executive itineraries? |
| V9 | Subprocessor changes are announced | Contract draft | Subprocessor policy | Notice is given by website posting. Does the bank get advance notice and a right to object? |
| V10 | No real data in test environments | RFP response | Test data policy | Is production data ever copied for debugging? |
| V11 | Customer data is encrypted | Security whitepaper | Encryption standard | Which algorithms, who holds the keys, and is a customer-managed key available? |
| V12 | Tenant separation | Security whitepaper | Architecture description, test evidence | How is cross-tenant access prevented and tested? |
| V13 | The platform uses AI features (itinerary suggestions, chat assistant), and customer data is not used to train models | RFP response | AI feature inventory, contract clause | Which model provider is used? Does bank data leave the vendor cloud for it? Can training use be switched off? |

## 8. Fourth parties and subprocessors

A fourth party is a supplier of Vendor X that handles the bank's data or supports the service. The role column is a **first view and needs a legal check** by the privacy team: a supplier is a processor if it acts on the vendor's instructions, and an independent controller if it decides its own purposes (for example an airline holding passenger records).

| ID | Fourth party | What it does | Data received | Likely role (to confirm) | Location | Contract with the bank |
|---|---|---|---|---|---|---|
| FP1 | Cloud hosting provider | Hosts the platform and data | All data, encrypted (D1 to D16) | Subprocessor | EU | No, through the vendor |
| FP2 | Airlines and GDS providers | Issue tickets | D1, D2, D3, D4, D9, D13 | Airlines: independent controllers. GDS: to confirm | Global | No |
| FP3 | Hotels and ground transport | Provide rooms and rides | D1, D4, D9, D13 | Independent controllers | Global | No |
| FP4 | Visa agency network | Submits visa applications | D2, D3, D8, D11 | Processor or controller, to confirm | Destination countries | No |
| FP5 | Group insurer (the bank's own) | Provides travel cover and claims | D1, D2, D3, D4, D15 | Independent controller. **A third party of the bank** that receives data through the vendor | EU | Yes, held by the bank |
| FP6 | Card Provider Y | Issues virtual cards | D14, D6, D1 | Processor and card issuer | EU | No |
| FP7 | Gift and florist marketplace | Delivers gifts | D12 | Processor or controller, to confirm | Several countries | No |
| FP8 | Emergency assistance partner | Runs the 24/7 assistance line | D1, D2, D4, D11, D15 | Processor | EU | No |
| FP9 | Email and SMS provider | Sends notifications | D1, D4, D5 | Processor | US, with an EU data boundary claimed | No |
| FP10 | Monitoring and logging provider | Collects application logs | Logs that may contain D1, D4, D5 | Processor | US | No |

The bank has **no direct contract** with FP1 to FP4 and FP6 to FP10, so it cannot audit or enforce controls there. Control comes through the vendor contract and the subprocessor list.

## 9. Proposed answers to the open questions from Stage 1 (simulated)

| Question | Proposed answer | Where it is tested next |
|---|---|---|
| Who operates the connector? | The vendor, in a dedicated instance in its cloud | Stage 3 (architecture) |
| Where is the roster copy stored, and for how long? | Primary EU region, replicated to the secondary region. Deactivated employees are removed 90 days after leaving. Backups are kept 35 days | Stage 4 (retention control) |
| Which suppliers are controllers and which are subprocessors? | See section 8. A first view only | Stage 4 (legal check) |
| Which card provider issues the virtual cards? | Card Provider Y, an EU-licensed issuer | Stage 4 (PCI DSS evidence) |

## 10. Early observations to test in Stage 5

These come from the claims register. They are **hypotheses**, not findings.

1. The SOC 2 audit period ended ten months ago, so a bridge letter is needed.
2. The SOC 2 and ISO scope may not cover the visa, gifts and card modules.
3. PCI DSS status is unclear: it is not stated whose attestation applies.
4. Connector secrets are rotated "annually or on request", which looks weak.
5. Support from India, and providers FP9 and FP10 in the US, may count as transfers outside the EU.
6. Subprocessor changes are announced on a website, with no advance notice or objection right.
7. The vendor operates the connector, so the vendor holds the bank's service-account credentials.
8. Several fourth parties have no contractual link to the bank.
9. AI features may send data to a model provider not listed in FP1 to FP10.

## 11. Decisions made in this stage

| ID | Decision | Source |
|---|---|---|
| A12 | The vendor operates the connector, in a dedicated instance per client in the vendor's cloud. The vendor holds the credentials the bank supplies (read-only HR service account, approval endpoint access). The bank must allow connections from the vendor's cloud to its HR system. The vendor is assessed on its secrets handling, staff access and connector security | Author |

## 12. Handoff

**To Stage 3 (architecture):** draw the zones (bank, connector, vendor cloud, suppliers), the flows for steps A and 1 to 12, mark where D1 to D16 cross a boundary, and mark the vendor-operated connector.
**To Stage 4 (controls):** turn each claim V1 to V13 and each observation into a control requirement and a question, and add Tier 1 contract questions.
**To Stage 5 (assessment):** simulate the vendor's evidence, record gaps and decide.

**Traceability keys added in this stage:** V vendor claim, FP fourth party.

## Addendum: FP11 (added after Stage 5, change PF-1)

FP11: AI model provider, US. Runs the chat assistant and itinerary suggestions. Data: D1, D4, and free text that may contain D9. Likely role: processor, to confirm. No contract with the bank. Not disclosed in the vendor's fourth-party list. See the Stage 5 assessment overview, section 4.
