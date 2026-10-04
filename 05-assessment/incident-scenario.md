# Incident scenario: stolen connector credential (tabletop)

> **Fictional case study. The scenario, times and results are simulated.** Drafted with AI assistance (Claude), to be reviewed by the author. Regulatory deadlines are indicative. Check the current texts and the bank's own incident process.
>
> **Status:** Draft for author review.

## 1. Why this scenario

It tests the weakest links found in the assessment: wide access to connector credentials (FND-01), annual rotation (FND-02), no mutual TLS (FND-09), and slow vendor notification (FND-16). It also shows how the controls we required would change the outcome.

## 2. Scenario

An attacker compromises a vendor engineer's laptop and uses the break-glass route to read the bank's connector credentials. From inside the vendor's cloud, the attacker connects to the bank's HR system through the connector's allowed source addresses and downloads the employee roster (D1: ID, name, grade, cost centre, manager, status) several times.

## 3. Timeline: as found and after remediation

| Step | As found (simulated) | After remediation |
|---|---|---|
| Detection | The bank's security team sees roster downloads at about six times the normal volume. Detected 4 hours after the first one | The same alert, plus the vendor's alert on break-glass use (the approval log shows no approval) |
| Containment on the bank's side | The bank disables the read-only service account in its HR system within 1 hour. This works because the account belongs to the bank | The same |
| Rotating the other credentials | The bank asks the vendor to rotate the HR portal, expense and ERP queue credentials. The vendor needs up to 2 business days. The connector is down and bookings fall back to the phone agent | The bank revokes and rotates the credentials itself within hours |
| Vendor notification | The vendor tells the bank 60 hours after it found the problem. The bank had found it first | The vendor notifies within 24 hours |
| Finding out who read the secret | There is no approval record for break-glass access, so the review takes days | The approval log shows who read it and when |
| Scope of the exposure | Roster data for all staff. Logs kept for 13 months help | The same, with minimised fields |
| Regulatory steps | See section 4 | See section 4 |
| Recovery | Re-key, review other service accounts, restore the nightly sync, hold a review | The same, faster |

## 4. Regulatory and communication steps

| Step | Who | Note |
|---|---|---|
| Classify the incident | Bank IT security, using its ICT incident process | DORA requires major ICT-related incidents to be classified and reported to the supervisor. The first notice has a short deadline (hours). Check the current technical standards |
| Personal data breach assessment | DPO | GDPR Art 33: notify the supervisory authority without undue delay, where feasible within 72 hours of becoming aware, unless the breach is unlikely to cause risk. Art 34 applies if the risk to individuals is high |
| Inform staff, if required | HR and DPO | Names, grades and cost centres are exposed. Staff in other regions may fall under local rules (R9) |
| Brief management | TPRM and IT security | Business owner, risk committee |
| Ask the vendor for evidence | TPRM | Access logs, approval records, root cause, fixes |

The vendor's 72-hour commitment (FND-16) would leave the bank unable to meet its own short deadlines if it relied on the vendor to tell it first. That is why the memo asks for 24 hours.

## 5. What the exercise shows

| Observation | Finding | Fix |
|---|---|---|
| The bank could contain part of the damage alone | The bank owns the HR service account | Keep read-only accounts under the bank's control |
| The other credentials depended on the vendor | FND-02 | REM-02: rotation every 90 days, bank-side revoke |
| Nobody could say who read the secret | FND-01 | REM-01: approval and logging |
| The vendor was slow to tell the bank | FND-16 | REM-16: 24-hour notice |
| The attacker used allowed addresses | FND-09 | REM-09: mutual TLS |

Related indicators: KRI-01 (days since rotation) and KRI-12 (hours to notify).

## 6. Questions for discussion

1. Who at the bank decides to disable the service account, and how quickly can they do it?
2. How does the business keep booking travel while the connector is down?
3. What would we tell staff, and who decides?
4. Which contract clauses give the bank the right to evidence and a root-cause report?
5. Would the bank have found the problem first if its HR system did not log download volumes?
