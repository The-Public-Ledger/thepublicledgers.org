---
title: "Charter School Financial Accountability"
description: "Registry covers 8,288 charter schools across 47 states enrolling 3,761,396 students"
date: 2026-04-03
status: "active"
tags: ["education", "charter-schools", "campaign-finance", "ppp"]
layout: "deep-dive"
deep_dive_slug: "charter-school"
sources:
  - "CMS NCES Common Core of Data (CCD)"
  - "FEC Individual Contributions (2019–2024)"
  - "SBA PPP Loan Data (150K+)"
  - "State charter authorizer records (NY, OH, PA)"
---
Charter schools receive public funding but operate with less financial oversight than
traditional public schools. This investigation cross-references charter school registries
against federal campaign finance records (FEC) and Paycheck Protection Program (PPP) loan
data to map the financial footprint of charter operators, management organizations, and
their affiliated entities.

## Political Spending

Charter-affiliated entities and individuals contributed $66K in documented federal
campaign contributions across multiple election cycles. The analysis matches school names,
operator names, and affiliated entity names against the FEC individual contributions
database using multi-tier entity resolution (exact match, containment, word overlap).

## PPP Loan Exposure

Charter-affiliated entities received $2.4M in PPP loans during 2020–2021. Cross-referencing
PPP borrower names against charter registries identifies overlap between publicly funded
schools and pandemic relief recipients.

## "Friends Of" Network

IRS Form 990 TEOS bulk data identifies five nominally independent nonprofit organizations
("Friends Of" entities) that collectively receive approximately $14 million per year in
rent from New York City charter schools and pass the money to private real estate
interests. Analysis is derived from manual extraction of IRS Part IX contractor rows,
not automated pipeline flags.

## Related-Party Lease Signals

Manual review of IRS 990 filings identifies schools where a landlord is named in
financial disclosures but the operator relationship is not documented — a signal
warranting further review. This analysis is preliminary; findings are leads, not
conclusions.

## Downloads

- [Charter political spending (CSV)](/data/charter_political_spending.csv)
- [Related-party lease signals (CSV)](/data/charter_lease_flags.csv)

For newsrooms: contact editor@thepublicledgers.org for the full dataset.

{{< source-note db="CMS NCES Common Core of Data (CCD), FEC Individual Contributions (2019–2024), SBA PPP Loan Data (150K+)" date="2026-04-03" >}}
