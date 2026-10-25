# 01. Classification Register: KLP BANKS

**Purpose:** Decide which of the three levels (Public, Internal, Confidential) each type of information at the fictional bank **KLP BANKS** belongs to, and show the reasoning.
**Companion documents:** [Handling matrix](02_handling_matrix.md) (what to do at each level), [Practical examples](03_practical_examples.md), [Staff checklist](04_staff_checklist.md).

> KLP BANKS is a fictional organisation created for this exercise. No real customer, employee or bank data is used anywhere in this repository.

---

## 1. Level definitions

| Level | Definition | Typical harm if disclosed |
|---|---|---|
| **Public** | Formally approved by its owner for release to anyone. | None from reading it. The risk is *tampering* (integrity) and *unavailability*, not secrecy. |
| **Internal** | For KLP staff and contracted partners under NDA. Not approved for public release. | Limited and recoverable: embarrassment, easier social engineering, minor commercial insight for an attacker. |
| **Confidential** | Disclosure could seriously harm customers, staff, the bank's cash or physical safety, the security of its systems, or breach the law. | Serious: fraud, identity theft, robbery, regulatory penalties, loss of customer trust. |

## 2. How an item is classified (the method)

For every data type we ask four questions, in order:

1. **What is it?** (data type and its owner)
2. **What would an attacker want from it, and what could they do with it?**
3. **Who is harmed, and how badly?** (customers, staff, the bank, the public; also legal impact)
4. **Which level does that harm justify?**

![Classification decision flow](../diagrams/classification_decision_flow.png)

**Principles applied**

- **Classify by content, not by container.** A blank cheque form is Public; the table mapping customers to cheque-book serial numbers is Confidential.
- **Avoid over-classification.** If everything is Confidential, staff stop noticing the difference and the label loses meaning (ISO/IEC 27002 guidance on classification warns about both over- and under-classification).
- **Classification can change over time.** Interest rates are Confidential until announced and Public afterwards. The data owner (not the person holding the file) approves reclassification.
- **Drafts take the level of their content** until release is approved.
- **Aggregates and logs take the level of the most sensitive thing they contain.**

## 3. The register

| # | Data type | What an attacker wants / can do | Who is harmed and how | Level |
|---|---|---|---|---|
| 1 | Customer identity and financial records (KYC, account numbers, balances, transactions) | Steal identity; open fraudulent accounts; run phishing, SIM-swap and payment-fraud scams | Customers lose money and privacy; the bank faces DPDP breach duties, penalties, loss of trust | **Confidential** |
| 2 | Employee personal records (Aadhaar, PAN, address, salary, contact details) | Impersonate staff; craft targeted phishing; attempt account takeover | Employees face fraud and privacy loss; bank carries legal liability | **Confidential** |
| 3 | Daily cash position and cash-in-transit schedules | Learn when and where the most cash sits; plan robbery or insider-assisted theft | Physical danger to staff and customers; direct financial loss | **Confidential** |
| 4 | Locker holder identities and locker access records | Target holders for coercion or burglary | Holders' physical and financial safety | **Confidential** |
| 5 | Mapping of customers to passbook / cheque-book serial numbers | Forge or intercept cheques; tamper with deliveries | Customers lose money; bank liable for fraud | **Confidential** |
| 6 | Authentication secrets (admin passwords, API keys, encryption keys, certificates) | Gain direct system access; decrypt stored data | Everything above is exposed at once | **Confidential** |
| 7 | Security architecture and test results (network diagrams, firewall rules, VAPT reports) | Skip reconnaissance and go straight to known weaknesses | Systems compromised; the report becomes a ready-made attack map | **Confidential** |
| 8 | Unannounced strategic plans (rates before announcement, new branches, deals) | Trade on the information; time scams around launches | Competitive and financial harm; scam risk around launches | **Confidential until announced** |
| 9 | Former customer and former employee records kept past their purpose | Same as #1 and #2, against people who no longer deal with the bank | Same harm, plus a breach of the DPDP duty to delete when the purpose ends | **Confidential** |
| 10 | Security, access and system logs | Learn usernames, IPs, system names and behaviour; erase evidence | Reconnaissance for attackers; tampering hinders investigations; may contain employee browsing data | **Confidential** (admin-restricted) |
| 11 | Infrastructure expenditure and budgets | Infer weak spots (for example, little spent on security) | Limited commercial and targeting insight | **Internal** |
| 12 | Org charts, staff directory, internal circulars, SOPs | Map who to impersonate or target for social engineering | Raises phishing success; little direct loss on its own | **Internal** |
| 13 | Funding and investor agreements | Learn commercial terms and counterparties | Commercial damage, not safety or fraud | **Internal** *(judgement call; see note 3)* |
| 14 | Published schemes, announced rates, offers, brochures | Nothing useful | None | **Public** |
| 15 | Branch addresses, contact numbers, working hours | Nothing useful | None | **Public** |
| 16 | Blank forms, annual report, regulatory disclosures | Nothing useful | None | **Public** |
| 17 | Public notices and customer security-awareness tips | Nothing useful | None | **Public** |

**Distribution:** 10 Confidential, 3 Internal, 4 Public. The weighting towards Confidential is realistic for a bank, and each Confidential entry names a specific serious harm.

## 4. Notes on judgement calls

1. **Logs (#10).** Logs are classified Confidential and restricted to authorised administrators and security staff. The security reasons are: logs give attackers free reconnaissance, they are evidence (so integrity matters), and they can contain personal data about employees' activity. A separate rule applies: *systems must never write passwords, keys or full customer data into logs.* Classifying logs as Confidential is a second line of defence against that mistake, not a substitute for fixing it at the source.
2. **Former records (#9) versus logs (#10).** These are different things with different retention logic. Old personal records should be deleted when their purpose ends (unless a law requires keeping them). Security logs are deliberately kept for a defined period to support breach detection and reporting.
3. **Funding agreements (#13).** Placed at Internal because the damage is commercial. A reviewer could reasonably argue for Confidential if the agreements contain sensitive terms. This is a documented design choice.
4. **Aadhaar numbers (#2).** Aadhaar handling has its own legal restrictions in India. The rules for storing, masking and displaying it must be checked against the primary legal texts before any real deployment (see the limitations in the technical report).
5. **Locker contents (#4).** The register covers holder identities and access records. Whether a bank knows what is inside a locker depends on the applicable RBI locker rules and should be verified; none is assumed here.

## 5. Reclassification

- The **data owner** approves any change of level, for example Confidential to Public when rates are announced.
- Record the date, the approver and the reason.
- When in doubt, keep the **higher** level until the owner decides.
