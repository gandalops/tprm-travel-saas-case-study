# Follow-up assessment: re-rating and risk reduction

> **Fictional case study.** Example Bank and Vendor X are placeholders. All vendor replies, evidence, dates and scores are simulated. Legal references are indicative and must be checked against the official texts.
>
>> **Builds on:** the initial assessment (folders 01 to 05, unchanged). **Position at:** 4 Dec 2026.

## 1. What the follow-up assessment is

In a real programme the first assessment is not the end. The bank asks follow-up questions, the vendor replies, and the analyst re-rates the findings **only on verified evidence**. The follow-up does that for the travel platform. The initial assessment (folders 01 to 05) stays as the baseline and is not edited. The follow-up is recorded in this folder, so a reader can see what moved, what stayed and what is new.

## 2. Files in this folder

| File | Content |
|---|---|
| `bank-request.md` | The bank's request: evidence for the 22 open findings, the physical architecture request, 65 new questions in 18 areas, 23 re-asked questions |
| `vendor-response.md` | The vendor's simulated reply, including its physical architecture and security specification |
| `vendor-physical-architecture.png` and `.svg` | The vendor's submitted diagram, with the analyst's red annotations |
| `follow-up-workbook.xlsx` | Questions, replies, ratings, evidence, findings, four-score risk register, conditions, new actions, bank actions, regulatory map, ISO view |
| `decision-memo-follow-up.md` | The updated decision |
| `follow-up-dashboard.png` and `.svg` | One-page before and after view |
| `traceability-matrix-follow-up.xlsx` | The threads from the initial assessment plus follow-up columns and new threads |

## 3. Timeline (simulated)

| Date | Event |
|---|---|
| 12 Oct 2026 | Bank request issued |
| 6 Nov 2026 | First vendor reply, including the physical architecture |
| 27 Nov 2026 | Second evidence batch |
| 4 Dec 2026 | Re-assessment closed |
| 11 Dec 2026 | Risk committee |
| 15 Jan 2027 | Conditions due |
| 1 Feb 2027 | Go-live target |

## 4. What was asked and how the vendor replied

| Item | Count |
|---|---|
| Evidence requests for open findings | 22 |
| New questions | 65 (38 Must, 21 Should, 6 If applicable) in 18 areas |
| Re-asked questions from the initial assessment | 23 |
| New evidence items | 41 (EV-26 to EV-66) |
| Vendor replies to the 65 | 51 full, 11 partial, 1 declined, 2 no reply |
| Rating of the answers | 30 Satisfactory, 26 Partial, 7 Gap, 2 not assessed |

The areas follow a standard security control catalogue (access, data, cryptography, application, cloud, network, third parties, AI, vulnerabilities, monitoring, incidents, continuity, privacy, governance, change, people, infrastructure, physical). Questions were chosen to **close open findings first**, then to fill gaps, and the depth matches a Tier 1 vendor. Nine kinds of request were left out on purpose (see the end of this section).

### What the bank did itself, and what it chose not to ask

Not everything needs the vendor. The bank ran ten outside-in checks from public information: sanctions and adverse media, TLS configuration, email security records, certificates, an external security rating, breach history, the company registry, the public subprocessor page, credit indicators and the security contact page. Two of them backed up findings: the public subprocessor page omits the AI provider (FND-04), and there is no security contact page (FND-33).

The bank also listed thirteen actions it must perform itself, such as the invoice call-back check, the weekly review of rate-table changes and a runbook to disable the connector's accounts. These are the customer-side controls that the vendor assumes the bank operates.

The bank deliberately did not ask for source code, did not run tests against the vendor, did not visit data centres, and left out environmental and social reporting, e-discovery, container configuration, full application security verification and red team reports. Choosing what not to ask is part of proportionality.

The results, owners and reasons are in the workbook sheets *Outside-in checks*, *Bank actions* and *Not requested*.


## 5. What happened to the 22 initial findings

| Outcome | Count | Findings |
|---|---|---|
| Closed with verified evidence | 8 | FND-01, 06, 10, 11, 13, 17, 18, 19 |
| Closed for the go-live scope (avoided) | 2 | FND-04 (AI assistant off), FND-20 (EU rollout only) |
| Risk accepted with a signed sign-off | 1 | FND-09 (no mutual TLS) |
| Partly closed (severity reduced or kept) | 6 | FND-02, 03, 08, 14, 16, 21 |
| Still open | 5 | FND-05, 07, 12, 15, 22 |

**High findings:** 5 in the initial assessment became 2 open. FND-01 closed, FND-04 avoided, FND-02 and FND-03 reduced to Medium, FND-05 still High. One new High appeared (FND-23).

## 6. New findings from the follow-up

Deeper questions found more. Eleven new findings appeared.

| ID | Finding | Severity | Control | Risk |
|---|---|---|---|---|
| FND-23 | US backup replication contradicts the EU-only claim | High | CR-14, CR-30 | RR-18 |
| FND-24 | Security testing gaps | Medium | CR-29 | RR-19 |
| FND-25 | Branch protection can be bypassed | Medium | CR-29 | RR-19 |
| FND-26 | No software bill of materials | Low | CR-29 | RR-19 |
| FND-27 | Weak encryption key management | Medium | CR-31 | RR-20 |
| FND-28 | SOC 2 exceptions and unmapped customer controls | Medium | CR-23 | RR-12 |
| FND-29 | Incident exercise out of date | Low | CR-24 | RR-08 |
| FND-30 | Offshore staff screening and endpoint protection | Medium | CR-32 | RR-21 |
| FND-31 | Backup restore not tested | Medium | CR-24 | RR-07 |
| FND-32 | Liability cap far below the potential loss | Medium | CR-33 | RR-08 |
| FND-33 | No public vulnerability disclosure programme | Low | CR-23 | RR-19 |

**The most important new finding is FND-23.** The vendor's own architecture diagram shows cold backups replicated to a US region since 2025. This contradicts the claim in Stage 2 that data stays in the EU (V6). It was found by comparing a vendor **claim** with a vendor **diagram**, which is the point of asking for the physical view.

## 7. How the risk rating reduced

Risk falls only when evidence is verified. Four scores are kept for each risk: inherent, initial current, verified after the follow-up, and target.

| Band | Inherent | Initial | Follow-up | Target |
|---|---|---|---|---|
| Very high | 2 | 2 | 1 | 0 |
| High | 12 | 4 | 3 | 0 |
| Medium | 7 | 11 | 13 | 12 |
| Low | 0 | 0 | 4 | 9 |
| Not identified in the initial assessment | | 4 | | |

For the 17 risks that existed in the initial assessment, those at High or above fell from **6 to 3**. Four new risks (RR-18 to RR-21) were added, and one of them (US backups) is Very high until fixed.

| Risk | Inherent | Initial | Follow-up (verified) | Target |
|---|---|---|---|---|
| RR-01 Stolen connector credential allows bulk reading of employee data | 20 Very high | 15 High | 8 Medium | 8 Medium |
| RR-02 Standing support access from India exposes production data | 16 Very high | 16 Very high | 12 High | 8 Medium |
| RR-03 Personal data reaches an undisclosed AI provider in the US | 12 High | 16 Very high | 4 Low | 4 Low |
| RR-04 Fraudulent or altered invoice reaches the ERP | 12 High | 9 Medium | 6 Medium | 6 Medium |
| RR-05 Fraudulent allowance payments through rate-table changes | 9 Medium | 9 Medium | 6 Medium | 3 Low |
| RR-06 Card misuse or PCI non-compliance | 12 High | 8 Medium | 4 Low | 4 Low |
| RR-07 Outage or slow recovery of the platform | 9 Medium | 9 Medium | 9 Medium | 6 Medium |
| RR-08 Late breach notice, costly incident assistance and a low liability cap | 12 High | 12 High | 12 High | 6 Medium |
| RR-09 Excess retention and exposure of guest, log and test data | 12 High | 9 Medium | 6 Medium | 4 Low |
| RR-10 Unseen fourth parties and late notice of change | 12 High | 9 Medium | 9 Medium | 6 Medium |
| RR-11 No effective audit or exit rights for a critical service | 15 High | 15 High | 15 High | 5 Medium |
| RR-12 Reliance on outdated or narrow assurance reports | 9 Medium | 9 Medium | 9 Medium | 6 Medium |
| RR-13 Leak of executive itineraries | 15 High | 12 High | 8 Medium | 8 Medium |
| RR-14 Takeover of vendor break-glass admin accounts | 12 High | 8 Medium | 4 Low | 4 Low |
| RR-15 Non-compliance with local rules outside the EU | 9 Medium | 9 Medium | 6 Medium | 6 Medium |
| RR-16 Insurer and assistance data kept too long or interface fails | 9 Medium | 6 Medium | 3 Low | 3 Low |
| RR-17 Minor misuse of loyalty data, discount codes or booker accounts | 6 Medium | 6 Medium | 6 Medium | 4 Low |
| RR-18 Personal data stored outside the EU through US backup replication | 12 High | not identified | 16 Very high | 4 Low |
| RR-19 Application vulnerability reaches production through weak development controls | 12 High | not identified | 9 Medium | 6 Medium |
| RR-20 Encryption keys weakly protected | 8 Medium | not identified | 8 Medium | 4 Low |
| RR-21 Misuse or data leakage by offshore support staff | 12 High | not identified | 9 Medium | 6 Medium |

Why risks moved in different ways:

| Movement | Example | Reason |
|---|---|---|
| Down, evidence verified | RR-14 break-glass takeover: 8 to 4 | Vault configuration and approval log verified (FND-18) |
| Down, risk avoided | RR-03 AI provider: 16 to 4 | The assistant was switched off and the bank watched the test (FND-04) |
| Down, but not to target | RR-02 support access: 16 to 12 | Just-in-time access works, but masking for offshore staff and screening are still open |
| Accepted with sign-off | RR-01 credential: 15 to 8 | Mutual TLS refused, compensating controls accepted by Bank IT security |
| No movement | RR-11 audit and exit rights: 15 | The vendor's counter-proposal is not enough, and the exit clauses are unsigned |
| Up or new | RR-18 US backups: new, 16 | A new fact found through the vendor's own diagram |

A promise (for example "masking by April 2027") lowers the risk only after it is delivered and verified. Until then the plan is a tracked action, not a lower score.

## 8. Go-live conditions

Ten conditions are due on 15 Jan 2027 (the 8 from the initial assessment plus two new ones). After the follow-up:

| Status | Count |
|---|---|
| Verified | 2 |
| Verified with residual | 2 |
| In progress (agreed, not signed) | 3 |
| Partly met | 1 |
| Not met | 2 (REM-05 audit rights, REM-23 US backups) |

Both feature gates are verified: the AI assistant stays off, and virtual cards can be enabled.

## 9. Decision

Conditional approval is kept. Go-live on 1 Feb 2027 is **not yet cleared**, because two High findings are open. The details and the options for the risk committee are in `decision-memo-follow-up.md`.

## 10. What this shows about the analyst's work

- Starts from the open findings and asks for evidence, not for everything.
- Compares a claim with an artefact, and catches a contradiction (FND-23).
- Rates evidence strength, and tells apart a verified fix, a promise and a refusal.
- Accepts a compensating control only with a signed owner.
- Keeps the baseline intact and records change with IDs and dates.
- Lists what the bank must do itself (customer-side controls) and what it chose not to ask.

## 11. Limits

- All replies, evidence and dates are simulated.
- Likelihood and impact are judgement scores.
- The analyst did not test the vendor or review code. Only a few items were observed by the bank (EV-30, EV-32, EV-44).
- Dates after October 2026 are part of the simulation.
- The new regulatory references are indicative. Check them against the official texts.


## ============================================= left out on purpose==================================================================

## 1. what the bank does itself

**Outside-in checks** (no vendor effort needed):

| ID | Check |
|---|---|
| OS-01 | Sanctions and adverse media screening of the legal entity and owners |
| OS-02 | Public TLS configuration of the vendor's endpoints |
| OS-03 | Email security records (SPF, DKIM, DMARC) |
| OS-04 | Certificate and domain hygiene |
| OS-05 | External security rating |
| OS-06 | Public breach history, last three years |
| OS-07 | Company registry: ownership and legal entity |
| OS-08 | Public subprocessor page |
| OS-09 | Credit and financial indicators |
| OS-10 | Security contact page (security.txt) |

**The bank's own actions** (customer-side controls the vendor assumes):

| ID | Action | Owner |
|---|---|---|
| BA-01 | Call-back check for any change of the vendor's bank details | Bank Finance |
| BA-02 | Conditional access and MFA policy for the platform application | Bank IT security |
| BA-03 | Quarterly access review of bank-side booker accounts | Bank HR and IT |
| BA-04 | Ingest vendor audit events into the bank's SIEM when streaming is available | Bank IT security |
| BA-05 | Weekly review of the allowance rate-table change log | Bank Finance |
| BA-06 | Runbook to disable the connector's service accounts at once | Bank IT security |
| BA-07 | Register of information entry and criticality record | Bank Compliance |
| BA-08 | Confirm whether the supervisor must be informed before signing | Bank Compliance |
| BA-09 | Decision on a data protection impact assessment | Bank DPO |
| BA-10 | Review the India transfer assessment | Bank DPO |
| BA-11 | Assign the 14 SOC 2 customer controls to bank owners | Bank TPRM |
| BA-12 | Fallback plan if the platform is unavailable (phone agent) | Bank HR |
| BA-13 | Incident contact list agreed with the vendor | Bank TPRM |

## 2. not requested, and why

| Item | Reason |
|---|---|
| Source code review or access to repositories | The analyst asks for evidence, not code. Branch rules and scan summaries are enough |
| Running scans or tests against the vendor | Not an analyst's job and not permitted without agreement. The penetration test letter covers it |
| On-site visit to the cloud provider's data centres | Controls are inherited. The provider's assurance reports are requested instead |
| Physical security details of every vendor site | Asked once for the India support site, as an if-applicable item |
| Environmental, social and diversity reporting | No link to a risk in this case |
| E-discovery and legal hold procedures | Not relevant to a travel platform. Data return is covered in the contract |
| Container and Kubernetes configuration exports | Posture report and scan summaries are enough unless a finding points here |
| Full application security standard verification | Out of proportion for an analyst. Scan, test and review evidence is requested instead |
| Red team reports | Not expected from a vendor of this kind. Penetration test retest letter requested |
