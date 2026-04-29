---
title: "Water & Environmental Justice"
description: "289,767 EPA-regulated facilities tracked across 3,120 counties"
date: 2026-04-14
status: "active"
tags: ["water", "environment", "epa", "enforcement", "environmental-justice"]
layout: "deep-dive"
deep_dive_slug: "water-environmental-justice"
sources:
  - "EPA ECHO Enforcement and Compliance History"
  - "EPA SDWIS Safe Drinking Water Information System"
  - "EPA TRI Toxics Release Inventory"
  - "Census ACS (demographics by county/tract)"
  - "FEC Individual Contributions (2019–2024)"
  - "Senate LDA Lobbying Disclosure (2017–2025)"
  - "USASpending.gov (EPA grants)"
---
The EPA regulates 289,767 facilities across 3,120 counties under the Clean Water Act,
Safe Drinking Water Act, and related statutes. This investigation cross-references EPA
enforcement data (ECHO), demographic data (Census ACS), and political spending records
to map the overlap between environmental enforcement gaps, demographic vulnerability,
and political influence.

## Enforcement Gaps

EPA penalty and enforcement data reveals systematic variation in how environmental
violations are addressed. Total penalties assessed: $2.8B. The analysis identifies
counties where enforcement intensity (penalties per violation) falls below the national
median despite above-average violation rates.

## Demographic Disparities

Census demographic data overlaid on EPA facility and violation records documents
environmental justice disparities:

- **Income is the dominant predictor of environmental health violations.** County-level
  regression (N=2,963, state fixed effects) shows low-income communities have significantly
  more detected health violations per facility (β=0.031, p<0.001). This finding is stable
  across five robustness specifications.
- Higher-POC communities show a descriptive 2.2x penalty ratio, but this likely reflects
  larger industrial facilities in those areas. When controlling for income, POC predicts
  **fewer** detected health violations and **higher** penalties — the opposite of the
  under-enforcement hypothesis. The enforcement-gap model is null for both race and income.

## Polluter Political Spending

Cross-referencing major violators against FEC campaign finance records and Senate lobbying
disclosures maps the political spending of companies with the worst environmental records.

## Downloads

- [Top 50 violators (CSV)](/data/water_top_50_violators.csv)
- [Enforcement gaps by state (CSV)](/data/water_enforcement_gaps_by_state.csv)
- [Demographic disparity analysis (CSV)](/data/water_demographic_disparity.csv)
- [Polluter political donations (CSV)](/data/water_polluter_donations.csv)

For newsrooms: contact editor@thepublicledgers.org for the full dataset.

{{< source-note db="EPA ECHO Enforcement and Compliance History, EPA SDWIS Safe Drinking Water Information System, EPA TRI Toxics Release Inventory" date="2026-04-03" >}}
