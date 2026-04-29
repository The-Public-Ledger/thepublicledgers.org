---
title: "IDA Subsidy Accountability"
description: "Tracking $185B+ in corporate tax subsidies across 24 states with data. We cross-reference subsidy recipients against campaign finance records to document correlations between public money and political donations."
layout: "list"
status: "beta"
featured: true
featured_weight: 1
hub_stat: "$185B+ in subsidies tracked across 24 states"
category: "money"
---

Industrial Development Agencies and similar subsidy programs operate across more than 30 states, granting billions in property tax exemptions with minimal public accountability. Our analysis cross-references subsidy beneficiaries against campaign finance records, lobbying disclosures, and federal enforcement actions.

### What we found

Across the 14 states with complete donor-subsidy crossref analysis, **22-28% of subsidy beneficiaries also donated to political campaigns** affiliated with the officials who control subsidy approvals. This rate is 2-3 times the baseline business donation rate in most states (derived from Census County Business Patterns; all ratios are upper bounds).

Formal regression analysis using 438,714 New York organization donors as controls estimates that subsidy recipients donate approximately **130% more than non-recipient organizations** in the same county and era (OLS, p < 0.001). A logit model finds recipients are **19 percentage points more likely** to be substantive donors ($1,000+). These findings document a correlation; they do not establish that donations caused approvals.

### Status and caveats

This investigation is in **beta**. Findings are sourced from public records and reproducible, but the project has not completed full peer review across all states. Specific caveats:

- **All control group ratios are upper bounds** — Census CBP covers employer establishments only; the true baseline donation rate is likely higher
- **State-level variance exists** — FL (36.1%) and CA (42.3%) are outliers above the 22-28% core range; CA is inflated by labor unions in CalAccess data
- **Donation timing: post-approval collapse confirmed** — Callaway-Sant'Anna doubly-robust estimator finds donations decline −3.11 log points after IDA approval (p<0.001), with a pre-approval surge in the 1-2 years before the vote. Prior TWFE event study was superseded after Goodman-Bacon decomposition showed 95.7% forbidden comparisons. *(Updated 2026-04-16.)*
- **Spike methodology is transitioning** — some states use z-score detection, others have been rerun with nonparametric tests (see [methodology](/methodology/#pre-award-donation-spike-analysis))

### Flagship analysis: New York

New York has the deepest data: 104 IDAs, $12.19B in tracked exemptions, 2,753 county-level scorecards. Read the [full New York investigation](/investigations/ida-accountability/) for detailed findings including the Erie County IDA case study, Harris Beach fee analysis, and school district revenue impact.
