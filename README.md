# Data Classification and Handling Guide (KLP BANKS)

**RedKross Research Foundation: Cybersecurity Internship, Task 1 (Data Handling)**
**Intern:** ISHAAN BANSAL | **Intern ID:** 2436 | **Batch:** October 2026

> **Explanatory video:** [ADD YOUR YOUTUBE (UNLISTED) OR GOOGLE DRIVE LINK HERE]

---

## 1. Objective

Create a **classification and handling guide** that tells staff how to treat **Public**, **Internal** and **Confidential** information, with rules for **storage, sharing, access, retention, disposal and incident reporting** at each level. The guide is built for a fictional Indian bank, **KLP BANKS**, and every rule is tied to a specific cybersecurity threat.

## 2. Approach

1. Researched the relevant standards and Indian regulations (see below).
2. Listed the data a bank holds, including security-specific data (credentials, security reports, logs).
3. Classified each data type by asking: *what would an attacker want, what could they do, who is harmed, how badly?*
4. Wrote handling rules for Confidential first, then relaxed them step by step for Internal and Public.
5. Tested the rules on paper against eight realistic security scenarios.
6. Condensed everything into a one-page staff checklist.

## 3. What is in this repository

```
redkross-data-handling-guide/
├── README.md                          <- you are here
├── report/
│   ├── Technical_Report.md            <- mandatory technical report
│   └── Technical_Report.pdf           <- PDF version of the report
├── deliverables/
│   ├── 01_classification_register.md  <- 17 data types, attacker/harm analysis, levels
│   ├── 02_handling_matrix.md          <- 3 levels x 6 rule areas
│   ├── 03_practical_examples.md       <- 8 security scenarios
│   ├── 04_staff_checklist.md          <- one-page checklist (source)
│   └── 04_staff_checklist.pdf         <- one-page checklist (print version)
└── diagrams/
    ├── classification_decision_flow.png
    └── classification_decision_flow.dot   <- Graphviz source
```

**Start here:** read the [classification register](deliverables/01_classification_register.md), then the [handling matrix](deliverables/02_handling_matrix.md), then the [examples](deliverables/03_practical_examples.md). Staff should only need the [checklist](deliverables/04_staff_checklist.pdf).

## 4. The three levels at a glance

| Level | Meaning | Examples at KLP BANKS |
|---|---|---|
| **Public** | Approved for anyone. Protect integrity and availability | Announced rates, branch addresses, blank forms |
| **Internal** | Staff and NDA partners only | Org charts, circulars, budgets |
| **Confidential** | Disclosure would seriously harm customers, staff, cash, systems or break the law | Customer and employee records, cash positions, lockers, credentials and keys, security reports, logs |

![Classification decision flow](diagrams/classification_decision_flow.png)

## 5. Key design ideas

- **Classify by content, not container.** A blank cheque form is Public; the customer-to-cheque-book mapping is Confidential.
- **Avoid over-classification.** If everything is Confidential, nothing stands out.
- **Levels change over time.** Rates are Confidential until announced.
- **Logs are Confidential**, and systems must never write secrets into them.
- **Disposal is a programme with evidence** (NIST SP 800-88 Rev. 2: clear, purge, destroy).
- **Legal clocks shape internal rules:** CERT-In 6 hours, DPDP Board report 72 hours.
- **Public data still needs security:** protect who can *change* it.

## 6. Standards and regulations used

ISO/IEC 27001:2022 Annex A (5.12, 5.13, 5.14, 5.15, 8.3, 8.10) and ISO/IEC 27002:2022; NIST SP 800-88 Rev. 2; FIPS 199 and NIST SP 800-60; India's DPDP Act 2023 and DPDP Rules 2025; CERT-In Directions (28 April 2022); RBI cyber security requirements for banks; CWE-532. Full IEEE-style references are in the [technical report](report/Technical_Report.md).

## 7. Testing and honesty statement

- This is a **policy and design project**. **No software was built and no security testing was done** on any system.
- The rules were checked **on paper** with a traceability check and eight scenario walkthroughs.
- Values marked **◆** (for example, review intervals and reporting deadlines) are design choices, not legal requirements.
- Some legal details (RBI reporting window, log-retention periods, record-keeping rules, Aadhaar handling) come from secondary sources and must be verified against primary texts before any real use.
- KLP BANKS is **fictional**. No real personal data, credentials or confidential information is included in this repository.
- This guide is not legal advice.
- AI assistance was used in preparing this work (see Section 11 of the technical report).

## 8. How to use

1. Read the register to find the level of a piece of information.
2. Look up that level in the handling matrix for the six rules.
3. Use the checklist before storing, sharing, keeping, disposing or reporting.
4. To adapt the guide to another organisation, rewrite the register, then adjust ◆ values and legal references with your compliance team.

## 9. Limitations

See Section 8 of the [technical report](report/Technical_Report.md). In short: fictional organisation, no live testing, some legal figures unverified, three levels only.

## 10. Author

ISHAAN BANSAL: B.Tech Cybersecurity, VIT Chennai. GitHub: [Gitishaan1](https://github.com/Gitishaan1)
