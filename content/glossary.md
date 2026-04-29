---
title: "Glossary"
description: "Definitions of terms used across Public Ledger investigations."
layout: "single"
---

## Subsidy & Tax Terms

<dl class="glossary">

<dt id="ida">IDA (Industrial Development Agency)</dt>
<dd>A public authority created by state or local governments to attract and retain businesses through tax exemptions, tax-exempt bond financing, and other incentives. IDAs operate in approximately 30 states.</dd>

<dt id="pilot">PILOT (Payment in Lieu of Taxes)</dt>
<dd>A negotiated payment made by a tax-exempt entity (typically an IDA beneficiary) to local taxing jurisdictions instead of full property taxes. PILOTs are often lower than the taxes that would otherwise be owed.</dd>

<dt id="485-b">485-b Exemption</dt>
<dd>A New York Real Property Tax Law provision granting partial property tax exemptions on improvements to commercial and industrial properties. The exemption phases out over 10 years.</dd>

<dt id="tif">TIF (Tax Increment Financing)</dt>
<dd>A public financing mechanism where future property tax revenue increases from a designated district are captured to finance current improvements within the district.</dd>

<dt id="chapter-313">Chapter 313 (Texas)</dt>
<dd>A Texas Tax Code provision (expired December 31, 2022) that allowed school districts to grant property tax abatements to attract investment. Total abatements exceeded $32 billion.</dd>

<dt id="clawback">Clawback Provision</dt>
<dd>A contractual clause requiring a subsidy recipient to return some or all public funds if job creation or investment commitments are not met.</dd>

<dt id="cost-per-household">Cost per Household</dt>
<dd>Total tax exemptions in a county divided by the number of households (Census ACS estimate). Represents the per-household share of forgone tax revenue, though the actual burden depends on how local governments compensate for lost revenue.</dd>

</dl>

## Statistical Terms

<dl class="glossary">

<dt id="bh-correction">BH Correction (Benjamini-Hochberg)</dt>
<dd>A statistical method that adjusts p-values when running many tests simultaneously, controlling the expected proportion of false discoveries. When testing 500+ companies for donation spikes, roughly 5% would appear significant by chance alone; BH correction accounts for this.</dd>

<dt id="q-value">q-value (BH-corrected p-value)</dt>
<dd>The adjusted significance threshold after applying Benjamini-Hochberg correction. A q-value below 0.05 means the finding is likely real, not a false positive from multiple testing. Our rank-based test has limited power with 3-5 baseline years.</dd>

<dt id="z-score">z-score (Effect Size)</dt>
<dd>A measure of how many standard deviations a value is from the mean. In our analysis, z-scores indicate the magnitude of a pre-award donation spike relative to baseline giving. Higher z-scores indicate larger spikes. Z-scores are used for ranking, not for determining statistical significance.</dd>

<dt id="nonparametric-test">Nonparametric Rank-Based Test</dt>
<dd>A statistical test that does not assume data follows a normal distribution. Used for donation spike detection because campaign contribution data is zero-inflated (most years have zero donations) and right-skewed (a few very large donations). The minimum possible p-value with <em>n</em> baseline years is 1/(<em>n</em>+1).</dd>

<dt id="control-group-ratio">Control Group Ratio (CBP Baseline)</dt>
<dd>The rate at which subsidy recipients donate to campaigns compared to the general business population (from Census County Business Patterns). A ratio of 3.0x means recipients are 3 times more likely to donate. These ratios are <strong>upper bounds</strong> because CBP undercounts non-employer firms.</dd>

<dt id="spike-ratio">Pre-Award Spike Ratio</dt>
<dd>The ratio of donations in the 2 years before a subsidy award to the average annual donations in the preceding baseline period. A ratio of 5.0x means donations were 5 times higher in the pre-award window.</dd>

</dl>

## Data Source Terms

<dl class="glossary">

<dt id="gjf">Good Jobs First (GJF) Subsidy Tracker</dt>
<dd>A national database of economic development subsidies maintained by Good Jobs First, a non-profit policy resource center. Covers grants, tax credits, property tax abatements, and other incentives across all 50 states.</dd>

<dt id="fec">FEC (Federal Election Commission)</dt>
<dd>The independent regulatory agency that administers and enforces federal campaign finance law. FEC bulk data includes all individual contributions over $200 to federal candidates and committees.</dd>

<dt id="echo">EPA ECHO (Enforcement and Compliance History Online)</dt>
<dd>An EPA database tracking facility-level environmental compliance, including inspections, violations, and penalties under the Clean Air Act, Clean Water Act, and RCRA.</dd>

<dt id="ppp">PPP (Paycheck Protection Program)</dt>
<dd>An SBA loan program created during COVID-19 to help businesses keep their workforce employed. Loans were forgivable if used for eligible expenses. Total disbursements exceeded $800 billion.</dd>

<dt id="leie">LEIE (List of Excluded Individuals/Entities)</dt>
<dd>The OIG's database of healthcare providers excluded from participation in Medicare, Medicaid, and other federal healthcare programs due to fraud, patient abuse, licensing issues, or other violations.</dd>

<dt id="npi">NPI (National Provider Identifier)</dt>
<dd>A unique 10-digit identification number issued to healthcare providers by CMS. An "active NPI" for an excluded provider does not prove current billing but is an indicator that the provider may still be practicing.</dd>

</dl>

## Investigation Terms

<dl class="glossary">

<dt id="crossref">Crossref (Cross-Reference)</dt>
<dd>The process of matching entities across two or more datasets to identify overlaps. For example, matching subsidy recipients against campaign donors. Uses 3-tier name matching: exact, word-overlap (75% threshold), and containment.</dd>

<dt id="confidence-tier">Confidence Tier (HIGH / MEDIUM / LOW)</dt>
<dd>A quality rating for entity matches. HIGH confidence matches are verified against secondary sources (corporate filings, SEC EDGAR). MEDIUM matches have strong name overlap but no secondary verification. LOW matches are suggestive and not used in publication.</dd>

<dt id="triple-dipper">Triple Dipper</dt>
<dd>A company that appears in three or more public subsidy programs simultaneously (e.g., state tax exemption + PPP loan + federal contract).</dd>

<dt id="round-trip">Round-Trip Flow</dt>
<dd>A pattern where a company both donates to and receives payments from the same political committee — money flowing in both directions between the same entities.</dd>

<dt id="bundling">Bundling Cluster</dt>
<dd>Three or more subsidy recipients making campaign contributions to the same committee on the same day, suggesting coordinated giving.</dd>

<dt id="stacking">Subsidy Stacking</dt>
<dd>When a company receives benefits from multiple public programs simultaneously (e.g., IDA tax exemption + EPA consent decree + PPP loan + FEC federal donations).</dd>

</dl>
