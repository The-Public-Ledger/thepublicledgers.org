---
title: "Nursing Home Accountability"
description: "Registry covers 14,710 nursing home facilities across 53 states"
date: 2026-04-03
status: "active"
tags: ["healthcare", "nursing-homes", "campaign-finance", "ppp", "patient-safety"]
layout: "deep-dive"
deep_dive_slug: "nursing-home"
sources:
  - "CMS Care Compare (Nursing Home Provider Info)"
  - "CMS Nursing Home Ownership Data"
  - "CMS Payroll-Based Journal (PBJ) Staffing"
  - "FEC Individual Contributions (2019–2024)"
  - "SBA PPP Loan Data (150K+)"
---
Nursing homes receive billions annually from Medicare and Medicaid, yet enforcement of
quality standards remains uneven. This investigation cross-references CMS nursing home
data (quality ratings, penalties, ownership, staffing) against federal campaign finance
records and PPP loan data to map the political and financial footprint of nursing home
operators.

## Quality and Enforcement

CMS Care Compare data documents facility quality ratings, deficiency citations, and civil
monetary penalties. Facilities with persistent low ratings and repeat penalties are flagged
for further investigation. Total penalties across registered facilities: $480.1M.

## Political Spending

Nursing home owners, operators, and parent organizations contributed $45K in documented
federal campaign contributions. The pipeline matches facility names, owner names, and
parent organization names against FEC individual contributions using multi-tier entity
resolution.

## PPP Loan Exposure

Nursing home entities received $650K in Paycheck Protection Program loans during 2020–2021.
Cross-referencing PPP borrower records against CMS ownership data identifies the overlap
between facilities collecting public healthcare payments and those receiving pandemic relief.

## Ownership Chains

CMS ownership data documents the corporate structures behind nursing homes — including
parent organizations, management companies, and individual owners with interests in
multiple facilities. These ownership chains are cross-referenced against political spending
and PPP records.

## Downloads

- [Nursing home political spending (CSV)](/data/nursing_home_political_spending.csv)
- [Spending by entity role (CSV)](/data/nursing_home_spending_by_role.csv)

For newsrooms: contact editor@thepublicledgers.org for the full dataset.

{{< source-note db="CMS Care Compare (Nursing Home Provider Info), CMS Nursing Home Ownership Data, CMS Payroll-Based Journal (PBJ) Staffing" date="2026-04-03" >}}
