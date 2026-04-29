---
title: "Opioid Settlement Spending Tracker"
description: "Tracking $24B in opioid settlement allocations across all 50 states. $3.8B in documented spending — just 16% of funds allocated. 1,329 mission-drift flags."
date: 2026-03-24
status: "beta"
tags: ["opioid", "settlements", "public-money", "mission-drift", "accountability"]
layout: "deep-dive"
deep_dive_slug: "opioid_settlement"
category: "money"
hub_stat: "$24B tracked · only 16% of funds documented"
sources:
  - "State opioid settlement spending reports (8 states)"
  - "KFF Health News national allocation database"
  - "FEC Individual Contributions (2020-2024)"
  - "SBA PPP Loan Data"
---
Opioid settlement funds are intended for treatment, recovery, and prevention.
But with billions flowing through thousands of local governments and agencies,
tracking where the money actually goes requires vendor-level transparency that
most states do not yet provide.

This investigation extracts spending data from state reports — PDFs,
spreadsheets, and web portals — and cross-references recipients against
campaign finance and relief-fund databases to surface potential mission drift.

## Scale

We track opioid settlement spending at three levels of detail:

- **National:** ~$26B committed across all 50 states from 8 settlements (Distributor,
  Janssen, Teva, Walgreens, CVS, Allergan, Walmart, Kroger) to 6,297+ recipients
  (source: KFF settlement database)
- **Documented spending:** ~$5.4B in payments tracked across **46 states** (state-specific
  extractors + KFF disbursement data, filtered to ≤2025 payments)
- **Vendor-level detail:** **42 states** with processed recipient-level data ($2.4B
  allocation, $1.4B documented spend) from 10 state-specific PDF/spreadsheet extractions
  + KFF breakdowns

⚠️ **Coverage note:** 9 states lack vendor-level detail (AR, CA, DC, DE, FL, LA, NH, NV, OK).
Two top-10 overdose mortality states are among them: Delaware (53.0/100K) and Louisiana
(50.6/100K). The 42-state rollup is the authoritative processed dataset; other figures
are supplementary.

| Category | Amount | Share |
|----------|--------|-------|
| Direct service (treatment, recovery, harm reduction) | $149.8M | 53.8% |
| Review-worthy (consulting, capital, unclear) | $23.4M | 8.4% |
| Other tracked spending / KFF disbursements | $105.2M | 37.8% |

## States with Spending Data

| State | Allocated | Spent | Direct Service | Review-Worthy |
|-------|-----------|-------|----------------|--------------|
| PA | $65.3M | $65.3M | $40.9M | $10.5M |
| MI | $58.3M | $58.3M | $49.3M | $3.2M |
| VA | $148.0M | $33.8M | $0 | $6.4M |
| IN | $137.7M | $25.1M | $15.6M | $6.0M |
| MA | $114.3M | $17.3M | $7.7M | $4.7M |
| OR | $137.3M | $10.9M | $9.1M | $0.97M |
| SC | $25.0M | $10.9M | $0 | $0 |
| CT | $31.4M | $4.5M | $0 | $0 |
| NJ | $231.6M | $4.1M | $3.7M | $0.76M |
| WV | ~$70M | $3.2M | $0.87M | $2.3M |

## West Virginia: A Case Study in Mission Drift

A manual review of all 70 vendor-level spending rows in West Virginia confirmed
that the automated mission-drift classification is accurate:

| Category | Amount | Share |
|----------|--------|-------|
| Law enforcement equipment (radios, drones, vehicles, shooting range) | $1.48M | 46.3% |
| Unclear or questionable (general fund transfers, kitchen remodels) | $0.99M | 30.8% |
| Treatment, recovery, and prevention | $0.73M | 22.8% |

Notable line items:
- **$333K** for a county radio system upgrade
- **$208K** for a law enforcement shooting range
- **$133K** transferred to a city general fund "to pay bills, and make payroll"
  (categorized under "media campaigns to prevent opioid use")
- **$65K** to promote a part-time police officer to full-time
- **$500K** to Huntington's Quick Response Team — the only six-figure treatment expenditure

Only 22.8% of West Virginia's documented spending reaches treatment, recovery,
or prevention services. The majority funds police equipment under settlement
categories broad enough to technically qualify.

## Mission-Drift Flags

The pipeline flagged **1,329 spending transactions** for editorial review across
six categories: opaque descriptions (generic "services" or "support" labels),
capital/construction spending, legal and PR vendors, administrative overhead,
large non-direct expenditures, and consultant-heavy patterns.

These flags are **triage signals for journalists, not conclusions**. The West
Virginia spot-check (above) confirmed that flagged items warrant investigation.

## Caveats

- Vendor-level detail available for 10 states; KFF national data covers 35 states at disbursement level
- CT and SC report municipality totals only — no vendor visibility
- Mission-drift flags reflect category taxonomy, not confirmed misuse
- Spending data mixes FY2023-24 and FY2024-25 across states
- Vendor political-spending matches (155) include medium-confidence word-overlap

## Data Sources & Attribution

National spending data from the [KFF Health News opioid settlement database](https://kffhealthnews.org/news/article/opioid-settlement-funds-detailed-database-state-county-city-spending/),
a project of KFF Health News, Johns Hopkins Bloomberg School of Public Health,
and Shatterproof. Used under Creative Commons license for non-commercial purposes.

State-specific vendor-level data extracted from official state reports:
Michigan DHHS, Pennsylvania (via [Spotlight PA](https://www.spotlightpa.org/)),
Oregon OHA, Indiana FSSA, West Virginia First Foundation, Virginia VOAA,
New Jersey ELEC, Connecticut DMHAS, South Carolina SCORF, Massachusetts AG.

Campaign finance crossref uses FEC bulk individual contributions (2020-2024,
191M records). PPP crossref uses SBA FOIA data (968K loans).

**What this analysis adds beyond existing trackers:** KFF Health News and other
trackers categorize how settlement money is spent. This investigation additionally
cross-references settlement vendors against federal campaign finance and relief-fund
databases to identify political connections — and applies automated mission-drift
classification to flag spending that may not align with settlement intent.

## Downloads

- [State-level rollup (CSV)](/data/opioid_state_rollup.csv)
- [Top recipients by spending (CSV)](/data/opioid_top_recipients.csv)

For newsrooms: contact editor@thepublicledgers.org for the full dataset and
mission-drift flag file.

{{< source-note db="State opioid settlement reports, KFF Health News / Johns Hopkins / Shatterproof, FEC, SBA PPP" date="2026-03-24" >}}
