---
title: "Water & Environmental Justice"
description: "289,767 EPA-regulated facilities tracked across 3,120 counties"
date: 2026-04-14
status: "active"
tags: ["water", "environment", "epa", "enforcement", "environmental-justice"]
layout: "deep-dive"
deep_dive_slug: "water"
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

## Enforcement gaps

EPA penalty and enforcement data reveals systematic variation in how environmental
violations are addressed. Total penalties assessed: $2.8B. The analysis identifies
counties where enforcement intensity (penalties per violation) falls below the national
median despite above-average violation rates.

## Demographic disparities

Census demographic data overlaid on EPA facility and violation records documents
environmental justice disparities:

- **Income, not race, is the defensible predictor of drinking-water health violations.**
  A county-level model restricted to public water systems (N=2,993 counties, state fixed
  effects, rural control) finds a higher health-violation rate per water system in
  lower-income counties (β=0.0146, p=0.032). The estimate is exploratory — no pre-registered
  analysis plan — and was re-estimated on 2026-06-22 after an independent peer review.
- Higher-POC communities show a descriptive 2.2x penalty ratio, which likely reflects
  larger industrial facilities in those areas. Once income is controlled, race does not
  predict health violations (null, p=0.26). The enforcement-gap model is null for both race
  and income.
- **Correction (2026-06-22).** An earlier version of this page reported that high-POC
  communities had *fewer* detected health violations (0.63x) and presented this as evidence
  against the under-enforcement hypothesis. That result was an artifact of attaching
  water-system violations to geocoded industrial facilities, which cannot incur them; it has
  been retracted. Restricted to water systems, the descriptive gradient runs the other way
  (1.38x, Q1→Q5), with the magnitude indicative only.

## Polluter political spending

Cross-referencing major violators against FEC campaign finance records and Senate lobbying
disclosures maps the political spending of companies with the worst environmental records.

## Downloads

- [Top 50 violators (CSV)](/data/water_top_50_violators.csv)
- [Enforcement gaps by state (CSV)](/data/water_enforcement_gaps_by_state.csv)
- [Demographic disparity analysis (CSV)](/data/water_demographic_disparity.csv)
- [Polluter political donations (CSV)](/data/water_polluter_donations.csv)

For newsrooms: contact editor@thepublicledgers.org for the full dataset.

{{< source-note db="EPA ECHO Enforcement and Compliance History, EPA SDWIS Safe Drinking Water Information System, EPA TRI Toxics Release Inventory" date="2026-04-03" >}}
