---
title: "Charges Watch: When Cases Disappear"
description: "Tracking criminal cases where charges were dropped or dismissed, cross-referenced against campaign finance records for defendants, prosecutors, and judges."
date: 2026-03-17
status: "pipeline-built"
tags: ["criminal-justice", "campaign-finance", "prosecutors", "courts"]
layout: "deep-dive"
deep_dive_slug: "charges_watch"
category: "governing"
hub_stat: "Dismissed charges matched to campaign donor records"
sources:
  - "CourtListener (court records API)"
  - "FEC bulk individual contributions"
  - "State court records"
  - "News archives"
---

This investigation tracks criminal cases in which charges were dropped or dismissed, then cross-references defendants, prosecutors, and judges against campaign finance databases.

The core question: do campaign contributions correlate with case outcomes?

## Infrastructure

A **4.8-million-record donor index** has been built from FEC contribution data, structured for fast fuzzy-matching against defendant and official names.

The pipeline is designed to flag:
- Defendants who appear in campaign finance records
- Prosecutors who received donations from defendants or their employers
- Judges appointed by officials who received donations from connected parties
- Cases where the same entity appears on both sides of a contribution relationship

## Status

The donor index is complete. Data ingestion pipelines for CourtListener and news archives are in development. This investigation page will be updated as leads are verified and published.

{{< source-note db="FEC, CourtListener" date="2026-03-17" >}}
