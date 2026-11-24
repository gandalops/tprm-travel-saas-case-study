# Vendor X travel platform: third-party risk assessment report

> **Fictional case study.** Example Bank and Vendor X are placeholders. The vendor's answers, evidence, dates and scores are invented, and legal references are indicative and must be checked against the official texts.

**To:** Head of HR (business owner), IT leadership, risk committee. **From:** Third-party risk analyst. **Position at:** 4 Dec 2026.

## 1. The request and our recommendation

- HR asked us to replace travel booking by email and spreadsheet with a corporate travel management platform. Vendor X is the platform we assessed.
- We ran the assessment with IT security, the network and identity teams, the data protection officer, Legal, Compliance, Finance and business continuity. This report brings their input together.
- **Our recommendation: keep the conditional approval, and do not clear go-live on 1 February 2027 yet.** The decision gate is 15 January 2027.
- Two High findings are still open. The first is audit rights (FND-05): the vendor offers two on-site audits a year with 10 working days' notice, and we are recommending that the bank holds out for unrestricted rights with sensible guardrails. The second is backups in the US (FND-23): the vendor's own diagram shows copies of our data replicated to a US region since 2025. That contradicts its EU-only commitment, and we need the deletion certificate before go-live.
- We are not recommending rejection. Once the vendor produced evidence, most findings moved the right way: access to the connector credentials is controlled, break-glass accounts are vaulted, executive itineraries are masked, and the AI assistant is switched off for the bank.
- In numbers: inherent risk 25 of 27. Findings went from 22 to 33, with 22 open (2 High, 13 Medium, 7 Low). Of the original 17 risks, those rated High or above fell from 6 to 3. Four of the ten go-live conditions are met or met with a residual.

## 2. Why this service needed a deeper review

- **The data is sensitive.** The platform holds passport details, dates of birth, visa documents and special requests that can reveal health or religion, for about 20,000 employees across the EU, Asia, wider EMEA, the US and Mexico.
- **It reaches into our systems.** Four connections open into the bank's HR system, HR portal, expense system and finance system.
- **It touches money.** It issues virtual cards, sends monthly invoices and holds the daily allowance rate table.
- **It carries people risk.** Executive itineraries are a physical-safety and market-sensitive matter, and staff abroad rely on its insurance and assistance.
- **The score confirmed it.** Eight of nine inherent risk factors scored the maximum, giving 25 of 27 and Tier 1, the deepest assessment. Only substitutability scored low, because many travel platforms exist. We classified the service as a critical or important function and as outsourcing. That is a judgement, and some banks would treat a booking tool as non-critical, so we confirmed the reasoning with HR on the process and fallback, and with Compliance on the classification.

## 3. Vendor profile and claims

- Vendor X Travel Platform Ltd is an Irish company founded in 2012, with about 900 staff and offices in Ireland, India, Singapore and Mexico. It has about 600 clients, around 40 of them banks, and it has been private-equity owned since 2021 and profitable since 2024.
- It is delivered as SaaS on a major cloud provider in two EU regions. The vendor operates the connector to our systems, in a dedicated instance for the bank.
- We recorded 13 vendor claims, among them ISO 27001 certification, a SOC 2 Type II report, PCI DSS compliance, an annual penetration test, recovery within 4 hours, data stored only in the EU, connector secrets held in a vault, and no use of customer data to train AI models. Each stays a claim until we see evidence.
- Some claims worried us from the start: the SOC 2 audit period ended ten months before our review, it was unclear whose PCI attestation applied, secrets were rotated "annually or on request", and subprocessor changes were only posted on a website.
- The vendor relies on eleven suppliers of its own, and the bank has a contract with almost none of them. We went through financial health and ownership with Procurement, and agreed with IT security which reports to request.

## 4. How the platform connects to the bank

- Four connections open into the bank, all started from the vendor's cloud: the nightly HR roster pull, the HR portal, the expense system and the finance system. The bank decides which source addresses it allows.
- The connector holds credentials for several bank systems in one place. If that place is compromised, an attacker reaches several systems at once.
- Invoices go straight from the vendor to the finance system and bypass the connector, so the connector's controls do not cover them.
- Vendor support staff in Ireland and India can reach production data, including executive itineraries, and the email and monitoring providers are in the US.
- We reviewed this with enterprise architecture and the network team. Each of the twelve observations became a risk, and then a control requirement the vendor has to meet.

## 5. Due diligence questionnaire

- We built 87 questions in 20 areas. Every question traces back to a flow, an observation or a vendor claim, and to a control requirement. We derived the controls from the risks first and mapped DORA, GDPR and ISO 27001 afterwards.
- Answers did not stay with us. IT security read the SOC 2 scope and exceptions, the penetration test and the encryption. The network and identity teams reviewed source addresses, mutual TLS, sign-on and leavers. The data protection officer took data locations, transfers, retention and subprocessors. Legal and Procurement took the contract. Compliance took the register of information, supervisor notification, gifts and sanctions. Finance took invoices, the allowance rate table and the liability cap. Business continuity took recovery targets, tests and exit. IT operations took the monitoring feed, change notices and runbooks.
- We assessed 64 priority questions first. After the vendor replied we asked 65 new questions in 18 areas and re-asked 23 that were not yet assessed, which makes 152 in total.
- We checked what we could without the vendor: ten outside-in checks from public information, such as sanctions screening, TLS and email security records. We also listed thirteen actions the bank must perform itself, such as the invoice call-back check.
- We kept the request proportionate. We did not ask for source code, did not test the vendor's systems and did not visit data centres.

## 6. Claims tested against evidence

- We rate each answer by the strength of its evidence: strong (an independent report, a dated export or something we observed), medium (a dated screenshot or small sample) or weak (a policy or a statement).
- A promise does not lower a risk. It counts only once it is delivered and verified. A vendor commitment to mask data by April 2027 is a tracked action, not a lower score.
- The EU-only claim did not survive the vendor's own architecture diagram, which showed cold backups replicated to the US. A document showed us what no questionnaire answer did.
- One early question showed that the chat assistant sends data to a US model provider that was missing from the vendor's supplier list. We had the feature switched off for the bank, and the bank watched the test.
- Evidence that held up included the SOC 2 bridge letter and the vaulted break-glass accounts. The masking of executive profiles is the strongest of all, because the bank's IT team observed it working.

## 7. Findings

- The initial assessment produced 22 findings: 5 High, 16 Medium and 1 Low.
- The five High findings were: eleven vendor staff could read the connector credentials, those credentials rotated only once a year, 22 India-based staff had standing access to production data, an AI provider was undisclosed, and audit rights were too narrow.
- Of those 22, eight are closed with verified evidence, two are closed for our scope (AI assistant off, EU rollout first), one is accepted with a signed sign-off (no mutual TLS), six are partly closed and five are still open.
- Deeper questions found 11 new findings, one of them High (the US backups). A deeper review finds more, so we read this as the follow-up doing its job.
- That gives 33 findings in total, of which 22 are open: 2 High, 13 Medium and 7 Low. The technical findings were reviewed with IT security, and the backup and transfer findings with the data protection officer.

## 8. Residual risk and how we treat it

- Residual risk is what is left after controls. For each risk we keep four scores: inherent, current, verified after the follow-up, and the target after remediation.
- Of the original 17 risks, those rated High or above fell from 6 to 3. Counting four new risks, the verified picture is 1 Very high, 3 High, 13 Medium and 4 Low among 21. If every remaining action is delivered, nothing stays above Medium.
- Four risks are still High or above: the US backups (Very high, 16), audit and exit rights (High, 15), support access from India (High, 12) and late incident notice with a low liability cap (High, 12).
- We choose a treatment for each risk. We mitigate by closing actions, avoid by keeping the AI assistant off, transfer through contract terms and insurance, and accept only with a named owner. IT security signed off compensating controls for the missing mutual TLS, and that is the one acceptance of note.
- Transfer does not remove the bank's own responsibility to its supervisor. Anything unresolved at the deadline goes to the risk committee.

## 9. Fourth parties and concentration

- The vendor depends on eleven suppliers: airlines, hotels, visa agencies, a card provider, the cloud host, email and monitoring providers, and the AI provider. The bank cannot audit them.
- Control therefore sits in the vendor's contract: a full supplier list, 30 days' notice of any change and a right to object. The vendor agreed this in the redline, but it is not signed yet.
- The AI provider was missing from the supplier list at first. It is on the list now, and the feature stays off.
- Visa agencies in destination countries receive passport copies, so deletion after use is a point we are pursuing in the contract, together with the data protection officer.
- The platform runs on one cloud provider. The vendor can fail over to a second EU region and has tested it, but it has no plan for an outage of the whole provider. That gap stays on our list.

## 10. Contract and exit

- We checked 24 required terms from DORA Article 30, the GDPR processor rules and our own liability needs. One is agreed in the contract draft, six in the negotiation redline, one is in negotiation, three are partly met, three are not met and ten are not yet assessed.
- The three that are not met are audit rights, the GDPR audit right (the same position) and data location. No term is signed yet, and we aim to sign by 15 January 2027.
- The liability cap is 12 months of fees, about EUR 0.4 million, against EUR 10 million of vendor cyber cover. We are asking for a separate, higher cap for data breach and confidentiality.
- The vendor offers incident notice within 48 hours, with a preliminary notice within 24 hours for major incidents. We asked for 24 hours, and the vendor's own 2024 incident took 52 hours to report.
- The exit plan lists seven triggers, such as insolvency, serious breach and a supervisor instruction. It sets out the steps to cut access within 24 hours, take our data back and obtain a deletion certificate, and names the team for each step. We will test it by 30 June 2027.

## 11. Ongoing monitoring

- After go-live we track 13 key risk indicators, among them days since the last credential rotation, open High findings, platform availability, hours to notify an incident and the age of the vendor's assurance reports.
- We also track 11 service level metrics, such as 99.9% availability and incident notice within 24 hours. These targets are proposals until the contract fixes them.
- The review rhythm is monthly for indicators and open findings, quarterly for a governance meeting with the vendor, every six months for remediation and evidence, and yearly for a full reassessment.
- When the vendor changes something material, such as a new supplier, a new region or a new module, we go back to the relevant team and reassess.
- The first checks after go-live are the second credential rotation in February 2027, the support access logs and the arrival of the signed contract. Medium actions must close by 30 April 2027.

## 12. Limits of this assessment and the decision we ask for

- We did not test the vendor's systems, review its code or visit its sites. We relied on documents, exports and the few items the bank observed itself.
- Risk scores are our judgement of likelihood and impact on a 1 to 5 scale. They are not calibrated with data.
- The critical-function classification is a judgement that another bank might make differently.
- Ten of the 24 contract terms have not been reviewed yet. They are not gaps, but they are not cleared either.
- Some defaults, such as 90-day credential rotation and 24-hour incident notice, are our proposals until the contract and the bank's policy fix them.
- **Decision requested from the risk committee:** hold out for unrestricted audit rights, require the deletion certificate for the US backups, and keep go-live open until 15 January 2027.
