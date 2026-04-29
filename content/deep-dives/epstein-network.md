---
title: "Epstein Network: Financial Mapping"
description: "Cross-referencing court documents, bankruptcy filings, and federal campaign finance records to map the financial architecture of the Epstein network."
date: 2026-03-17
status: "active"
tags: ["epstein", "campaign-finance", "fec", "financial-networks"]
layout: "deep-dive"
deep_dive_slug: "epstein"
category: "governing"
hub_stat: "Court records, SEC filings, FEC data cross-referenced"
sources:
  - "FEC bulk individual contributions (2020–2024 cycles)"
  - "SEC EDGAR corporate filings"
  - "Southern District of New York court records"
  - "USVI civil proceedings"
  - "Bankruptcy court filings"
---

This investigation maps the financial networks documented in court records, bankruptcy filings, and public disclosures connected to Jeffrey Epstein and his associates. All findings are derived from public records.

## Methodology

Names and entities were extracted from court documents using structured text parsing. Each name was normalized and cross-referenced against FEC federal campaign contribution records (2020–2024 cycles, 191M rows) using the standard three-tier matching pipeline: exact match → word overlap → containment.

The result is a dataset of **430 FEC contribution records** linked to persons and entities appearing in court documents.

A knowledge graph maps entity relationships — corporate ownership structures, shared addresses, officer overlaps — derived from SEC EDGAR filings and court exhibits.

## Current Status

Initial FEC crossref is complete. SEC EDGAR parent-subsidiary mapping and additional court document extraction are ongoing. Congressional recipient analysis is in progress.

This investigation is active. Findings will be published as analysis is completed and verified.

{{< source-note db="FEC, SEC EDGAR, SDNY court records" date="2026-03-17" >}}
