# Project Charter: GLP-1 Cost Watch

> Portfolio exercise. Not affiliated with any organization.

| Version | Date | Author |
| --- | --- | --- |
| v1 | Nov 10, 2026 | Rohit |

---

## 1. Purpose

Since 2020, Medicaid spending on GLP-1 drugs has increased quickly.
This project helps a state Medicaid budget team decide whether to keep, restrict, or drop GLP-1 weight-loss coverage, and how much money to plan for in 2027.

## 2. Business question

Which state Medicaid programs face the biggest GLP-1 cost risk,
what is driving that cost (more prescriptions, higher cost per prescription, or a shift to pricier drugs),
and what early changes appear in states that stopped covering GLP-1s for weight loss?

## 3. Stakeholder

- **Main reader:** the Pharmacy Budget Director of a state Medicaid program
- **Decision they make:** whether to keep, restrict, or drop GLP-1 weight-loss coverage next budget year, and how much money to plan for these drugs in 2027
- **Example state:** Missouri. **Comparison state:** Illinois.

## 4. Scope

**In scope**

- Medicaid outpatient drug data (meaning: prescriptions picked up at a normal pharmacy)
- By state and by quarter, 2020 to 2025 (+2026 if posted)
- Fee-for-service and managed care (why both: we need both to see all spending without missing an important part)
- State coverage policy dates (why: to see when each state started and stopped paying for GLP-1s for weight loss)

**Out of scope**

| Item | Why it is out |
| --- | --- |
| Patient health outcomes | The data has no patient information |
| Net cost after rebates | Rebates are secret; the data shows gross spending only |
| Individual doctors or pharmacies | The data is per state, and the decision is a state budget decision |
| Deep Medicare analysis | Medicare is a different program with a different budget |

## 5. Success criteria

1. My national 2024 GLP-1 gross spending is within 15% of KFF's ~$9B, or I can explain the gap.
2. By Jan 3, the dashboard has 5 pages, and every number matches the dbt mart tables.
3. By Jan 3, the price, volume and mix parts add up exactly to the total change (a dbt test checks this).
4. By Jan 9, I can explain every dbt model out loud without AI help.

## 6. Milestones

| Date | What is finished |
| --- | --- |
| Nov 15 | Setup done: repo, board, charter, tools installed, SDUD 2020 to 2025 downloaded |
| Dec 6 | Scope freeze: core analysis and first 2 dashboard pages; no new data sources after this date |
| Dec 13 | Minimum version on GitHub: README, 2 dashboard pages, charter, risk log |
| Dec 20 | Analysis done: coverage change test and 2027 cost scenarios |
| Jan 3 | Design done: 5-page dashboard, memo draft, video walkthrough |
| Jan 15 | Release: final README, memo PDF, dashboard PDF, LinkedIn post |

## 7. Top risks

| Risk | Effect | Plan |
| --- | --- | --- |
| Suppressed values (under 11 are hidden) | Totals are too low, especially for small states | Keep a suppression flag; never treat blanks as zero; report the share suppressed per state |
| National-total rows mixed in with state rows | Dollars are counted twice | Find and remove them in the staging model; compare totals before and after |
| Drug names cut to 10 characters | Some GLP-1 rows are missed or wrong drugs are included | Build a GLP-1 drug list seed and check unmatched names |
| 2026 data not posted in time | Coverage change test has no "after" period | Use the fallback: North Carolina, or states that added coverage in 2024 to 2025 |
| Not enough time during finals (Dec 7 to 13) | Dec 13 milestone slips | Only 30-minute tasks that week; buffer week Jan 11 to 15 |

Full list: see `risk_log.md`.

## 8. Assumptions

1. We assume the states report their drug data correctly, apart from known suppression and later revisions.
2. We assume the enrollment data covers the same states and quarters as the drug data.
3. We assume I have about 11 hours per week (1 hour on weekdays, 3 hours on weekend days).
