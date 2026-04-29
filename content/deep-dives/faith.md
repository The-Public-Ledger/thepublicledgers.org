---
title: "Faith & Public Services"
description: "Mapping the $34.5 billion overlap between religious hospitals, federal social service grants, and the lobbying campaigns that protect the arrangement."
date: 2026-03-21
status: "active"
tags: ["healthcare", "religion", "lobbying", "campaign-finance", "reproductive-health"]
layout: "deep-dive"
deep_dive_slug: "faith"
category: "patients"
hub_stat: "$34.5B in public funding to religious health systems"
sources:
  - "CMS Provider of Services File"
  - "CMS Hospital Cost Reports (HCRIS 2022-2024)"
  - "USASpending.gov (direct awards 2015-2026)"
  - "NY SPARCS Hospital Inpatient Discharges (2024)"
  - "Senate LDA Lobbying Disclosure API (2017-2025)"
  - "NY JCOPE Lobbying (2011-2025)"
  - "IRS EFILE XML (Form 990 Part VII, FY2023)"
---

*Disclosure: Zach Beaudoin, who conducted this analysis, is a candidate for Erie County Legislature, District 11. The Erie County case study below documents patterns in Erie County governance. All findings are derived from public records; methodology is at [/methodology/](/methodology/).*

---

Religious hospitals, social service agencies, and family planning grantees receive tens of billions of dollars in annual public funding. In 63 counties, a religious organization operates the **only emergency room** (68 total including 5 hospital-only counties). In 50 of those counties, the same religious institutional network also receives direct federal grants for WIC, Head Start, refugee resettlement, or other social services — creating circumstances where families in those counties encounter only religiously operated providers across multiple publicly funded service categories.

## The Hospital Desert

A "hospital desert" means the county's only emergency room is operated by a religious organization that follows doctrine-based clinical guidelines, such as the Catholic Church's *Ethical and Religious Directives* (ERDs). The ERDs prohibit sterilization, contraception, emergency contraception, and abortion at all facilities that operate under them.

New York state billing data (SPARCS) confirms these restrictions are reflected in actual care: Catholic hospitals document zero tubal ligations at a rate 46.8 percentage points higher than secular peers — 75% of religious hospitals record zero vs. 28.2% of secular peers — even at facilities performing 800+ C-sections annually.

## The Double Capture

In counties where the only hospital is religious, low-income families often also encounter religious organizations when accessing federally funded services. Catholic Charities — the social service arm of the Catholic Church — received $3.9B in federal grants since 2015 for refugee resettlement, Head Start, housing, and nutrition programs (WIC). When the same diocesan authority governs both the hospital and the social service network, families may face no secular alternative within the county across multiple publicly funded service categories.

## Lobbying

Religious health systems spent $35.2M in reported federal lobbying (2017-2025). The largest filers include Ascension Health ($16.4M), CHA ($6.9M), and Trinity Health ($6.7M). At the state level in New York, JCOPE records document 162 lobbying filings (2011-2025), including 54 related to certificate-of-need law — the regulatory framework that governs hospital closures and expansions.

## Case Studies

### Finney County, Kansas — Triple Capture

Finney County is the only "triple capture" county in the dataset. St. Catherine Hospital (Catholic, Diocese of Dodge City) is the sole ER for 38,000 residents in Garden City — a meatpacking hub with a large immigrant and refugee workforce. Catholic Charities of Southwest Kansas administers HUD housing and emergency services ($4.2M, USASpending). Head Start serves 272 children in the county.

A pregnant woman in Garden City delivers at a hospital that follows the Ethical and Religious Directives, receives food and housing assistance from Catholic Charities, and sends her children to a publicly funded Head Start — with no secular alternative at any point. Total Medicare and Medicaid revenue to the sole ER: $343M.

### Clermont County, Ohio — Suburban Cincinnati

Clermont County (pop. 209,000) is the largest confirmed-Catholic sole-ER county in the dataset. Trinity Health's Mercy Health - Clermont Hospital is the only emergency room, receiving $850M in Medicare and Medicaid revenue. This is a suburban county — not a remote rural community — where over 200,000 residents have no secular ER alternative.

Trinity Health is the same parent company that operates Catholic Health in Buffalo, NY. The system appears across multiple states in the dataset. Catholic Charities operates social services in Ohio ($8.3M statewide in AmeriCorps, HUD housing, and refugee resettlement).

### Erie County, New York — Billing Data Confirmation

Erie County offers the deepest documentation because New York provides granular billing data through the SPARCS inpatient discharge database.

- **Catholic Health** (Trinity Health affiliate): closed Kenmore Mercy Hospital (2021); Sisters of Charity Hospital (Catholic) is now the nearest ER for Kenmore and North Tonawanda; Mercy Hospital of Buffalo remains open — both Catholic Health hospitals document zero tubal ligations
- **Catholic Charities of Buffalo**: confirmed WIC local agency ($66.2M cumulative, USASpending); Bishop Fisher named Chairman on IRS Form 990
- **Single authority chain**: IRS XML confirms Bishop Fisher governs Catholic Charities directly and exercises indirect board authority over Catholic Health through his diocesan representative (Monsignor Robert Zapfel)
- **Procedure restriction confirmed**: Sisters of Charity: 863 C-sections/year, **zero tubal ligations**; Mercy Hospital of Buffalo: 622 C-sections/year, **zero tubal ligations** (NY SPARCS 2024)

## Downloads

- [Hospital desert counties (CSV)](/data/faith_deserts.csv) — all 63 ER-desert counties with funding, system, and denomination
- [Double-capture counties (CSV)](/data/faith_double_capture.csv) — 50 counties with hospital + social service overlap
- [NY procedure gap — SPARCS (CSV)](/data/faith_procedures.csv) — facility-level procedure rates
- [Federal lobbying filings (CSV)](/data/faith_lobbying.csv) — by organization and issue code

For newsrooms: contact editor@thepublicledgers.org for the full dataset.

{{< source-note db="CMS, USASpending, SPARCS, LDA, JCOPE, IRS EFILE" date="2026-04-13" >}}
