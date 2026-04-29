---
title: "Subsidy Clawback Tracker"
description: "1,657 companies received public subsidies and later filed WARN Act mass layoff notices, affecting 145,000 workers across 48 states. $39.2B in subsidy exposure."
date: 2026-03-24
status: "beta"
tags: ["subsidies", "clawback", "WARN-act", "jobs", "accountability"]
layout: "deep-dive"
deep_dive_slug: "subsidy_clawback"
category: "money"
hub_stat: "1,657 companies received subsidies then filed mass layoffs"
sources:
  - "WARN Act notices (CA, FL, NY, TX state DOL databases)"
  - "Good Jobs First Subsidy Tracker (48 states)"
  - "BLS QCEW (2019-2023)"
---
Companies receive billions in public subsidies with promises to create and maintain jobs.
When those jobs disappear, clawback provisions should return taxpayer money — but
enforcement is rare. This investigation cross-references subsidy beneficiaries against
WARN Act mass layoff notices to identify companies that took public money and later
cut workers.

## Scale

Across 48 states, **1,657 companies** that received public subsidies later filed WARN
Act layoff notices, affecting **145,241 workers**. Combined subsidy exposure: **$39.2B**.

Of these, **152 companies** are flagged as high-priority clawback candidates — cases where
the layoff came within 5-10 years of the subsidy award and the subsidy exceeded $100,000.
**71 of 152** received programs with explicit job-creation commitments (grants, MEGADEALs,
training reimbursements), giving the strongest legal basis for clawback enforcement.

## Top States by Worker Impact

| State | Companies | Workers | Subsidy Exposure |
|-------|-----------|---------|-----------------|
| TX | 126 | 48,988 | $8.2B |
| FL | 63 | 24,942 | $16.2B |
| NY | 105 | 21,245 | $13.7B |
| CA | 63 | 15,832 | $4.1B |

## Methodology

- Subsidy data from Good Jobs First Subsidy Tracker (48 states)
- WARN Act mass layoff notices from state DOL databases (100+ worker threshold)
- Entity matching via 3-tier normalization (exact, word-overlap, containment)
- Worker counts deduplicated by (company, date, workers) to prevent cross-state inflation
- Subsidy exposure deduplicated per company

## Caveats

- WARN Act only covers layoffs of 100+ workers — smaller reductions go unreported
- Absence of public clawback enforcement evidence does not prove no enforcement occurred
- Some matches reflect subsidiary-level layoffs at companies with parent-level subsidies
- FL WARN data embeds addresses in company names (~17.8% of rows), which may inflate match scores

## Downloads

- [High-priority clawback candidates (CSV)](/data/clawback_candidates.csv)
- [FOIA target list (CSV)](/data/clawback_foia_targets.csv)

For newsrooms: contact editor@thepublicledgers.org for the full dataset and FOIA templates.

{{< source-note db="Good Jobs First Subsidy Tracker, WARN Act State DOL Databases, BLS QCEW" date="2026-03-24" >}}
