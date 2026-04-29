---
title: "Methodology"
description: "How we collect, process, and verify data across 50 states — including what we can and cannot claim."
---

## What we are investigating

The Public Ledgers investigates financial relationships between economic development subsidy recipients and political donors. Specifically: do companies that receive government tax exemptions, grants, and abatements donate to the campaigns of officials who oversee those programs at higher rates than comparable businesses that do not receive subsidies?

We document these relationships from public records. We do not claim to prove causation.

---

## Data sources

We rely exclusively on public records. No anonymous tips, leaked documents, or paywalled sources are used.

### Federal sources (used across all states)

| Source | Description | Access |
|--------|-------------|--------|
| **FEC Individual Contributions** | Campaign donations to federal candidates and PACs, 2020–2024 cycles | Bulk download, fec.gov |
| **Good Jobs First Subsidy Tracker** | Economic development subsidies across all 50 states (grants, tax credits, abatements) | Web scrape, goodjobsfirst.org |
| **EPA ECHO** | Environmental compliance and penalty records for ~800,000 U.S. facilities | Bulk download, echo.epa.gov |
| **SBA PPP Loans** | Paycheck Protection Program loans ≥$150,000 through Sept. 30, 2024 | Bulk download, sba.gov |
| **SEC EDGAR** | Public company filings and officer identification | API + bulk download, sec.gov |
| **ICIJ Offshore Leaks Database** | Entities named in Panama Papers, Pandora Papers, and related datasets | API, icij.org |
| **Census County Business Patterns** | Employer establishment counts by state, used for control group baseline | API, census.gov |
| **Census F-33 School Finance Survey** | Annual school district revenue and property tax data (2022) | Download, census.gov |

### State campaign finance sources

| State | Source | Volume |
|-------|--------|--------|
| **New York** | NYS Board of Elections (Socrata API) | 12.49M records |
| **Ohio, Florida, Pennsylvania, Georgia, and 14 others** | Accountability Project S3 archive (University of Missouri) | 12–28M records per state |
| **Illinois** | IL State Board of Elections bulk download | 6.15M records (1994–2024) |
| **Texas** | Accountability Project S3 | 28.4M records |
| **Oklahoma** | Oklahoma Ethics Commission | 1.3M records |
| **Other states** | State-specific sources documented on each state page | Varies |

The [Accountability Project](https://publicaccountability.org/) at the University of Missouri maintains standardized state campaign finance datasets used by journalism and research organizations.

### Data vintage

Source datasets are downloaded during pipeline runs. The Git commit history at [github.com/The-Public-Ledger/thepublicledgers.org](https://github.com/The-Public-Ledger/thepublicledgers.org) records when each dataset was processed and published. All state pages display a "Last updated" date reflecting the most recent data run.

FEC data covers 2020–2024 election cycles. Good Jobs First data reflects awards reported as of the scrape date. Accountability Project campaign finance files reflect contributions through approximately late 2024. PPP data is a static FOIA release through September 30, 2024.

---

## Matching methodology

Beneficiary lists and campaign finance records use inconsistent entity names. "McDonald's Corporation," "McDonald's Corp," and "MCDONALD S CORP" all refer to the same company. We use a three-tier matching approach.

### Step 1: Normalization

All entity names are normalized before comparison:

- Convert to uppercase
- Remove punctuation and special characters
- Strip 11 business-type suffixes: LLC, INC, INCORPORATED, LP, LLP, CO, CORP, CORPORATION, LTD, PC, DBA
- Collapse whitespace

"McDonald's Corporation" and "MCDONALD S CORP" both normalize to "MCDONALD S" and match exactly.

### Step 2: Three-tier matching

**Tier 1 — Exact match**: Normalized strings are identical. Requires at least two words or ten characters to prevent matching single-word surnames or short abbreviations.

**Tier 2 — Word overlap**: At least 75% of meaningful words in the shorter name appear in the longer name. A list of generic terms is excluded before this comparison — organizational words (GROUP, HOLDINGS, VENTURES, SERVICES), geographic terms (AMERICA, NATIONAL, INTERNATIONAL), prepositions (OF, AND, THE, FOR), banking terms (SAVINGS, BANK, FEDERAL, CREDIT), and civic terms (CHAMBER, ASSOCIATION, COUNCIL). At least two meaningful words must remain after filtering. This prevents "United Services" from matching "United States."

**Tier 3 — Containment**: The shorter name appears entirely within the longer name, with the shorter name being at least ten characters and two words.

### Conservative reporting standard

Headline figures use Tier 1 matches only unless otherwise stated. Tier 2 and Tier 3 matches are included in full data downloads with confidence labels.

### False positive audit

We run a false positive audit on each state's results to identify and remove common-name collisions, geographic false positives, and matches that survive the length minimum but are still ambiguous. The Illinois analysis was revised from an initial $245.7M donation figure to $115.8M after a systematic audit identified seven categories of false positives (inflated by preposition-containing words and banking-sector generic terms being weighted as meaningful). This kind of revision is part of the methodology, not a correction to a published error.

---

## Statistical methodology

### Pre-award donation spike analysis

For each subsidized company that has a donation history, we test whether donations increased in the years immediately before the award year relative to that company's own historical baseline.

**Original test (states processed before April 2026):** We calculate a z-score comparing the award-year donation amount to the company's mean and standard deviation across all non-award years. A z-score above approximately 1.96 corresponds to p < 0.05 for that company in isolation.

Because we run this test for hundreds of companies simultaneously, some will appear significant by chance. We apply **Benjamini-Hochberg false discovery rate (FDR) correction** at q < 0.05 (Benjamini & Hochberg, 1995, *Journal of the Royal Statistical Society, Series B*, 57(1):289–300). This means: among the companies we flag as statistically significant, fewer than 5% are expected to be false positives.

**Updated test (states rerun April 2026 onward):** The z-score approach assumes donation amounts are approximately normally distributed within each company's history. For companies with few donation years or highly skewed distributions, this assumption is fragile. Beginning in April 2026, we are transitioning state-level spike analysis to a **nonparametric test** that does not assume normality. Under the nonparametric approach, spike detection uses rank-based methods with the same BH FDR correction at q < 0.05.

States rerun under the nonparametric test may show substantially different BH-significant spike counts compared to the original z-score results. For example, Illinois showed 116 BH-significant companies under the z-score test (March 2026) and 0 under the nonparametric test (April 2026). The ratio-based spike count (companies where award-year donations exceeded the historical mean) is unaffected by the test change. State dashboard pages indicate which test produced their current results.

Both the original z-score and the updated nonparametric results are valid applications of BH-corrected hypothesis testing; they differ in distributional assumptions. The transition is being applied state-by-state as pipelines are rerun.

**Aggregate timing: post-approval donation collapse confirmed.** *(Updated 2026-04-16.)* Using the Callaway-Sant'Anna (2021) doubly-robust difference-in-differences estimator — which avoids the "forbidden comparisons" problem in staggered treatment designs — we find an overall average treatment effect on the treated (ATT) of −3.11 log points (p<0.001). Donations surge in the 1-2 years before IDA approval (+0.88 to +1.66 log points at Tm1/Tm2), are near zero in the approval year, and collapse to −3.7 log points by year three, deepening to −6.1 log points over two decades.

The prior finding ("aggregate timing is not significant") was based on a two-way fixed effects (TWFE) event study. A Goodman-Bacon (2021) decomposition revealed that 95.7% of the TWFE's identifying variation came from treated-versus-treated comparisons — later IDA cohorts used as controls for earlier cohorts — rather than treated-versus-never-treated comparisons. This contamination rendered the TWFE estimate unreliable. A Rambachan-Roth (2023) sensitivity analysis confirmed that the TWFE confidence interval includes zero under any pre-trend violation magnitude.

The Callaway-Sant'Anna estimator uses "not-yet-treated" units as controls and explicitly excludes always-treated units, avoiding these forbidden comparisons. It is the primary causal estimate for donation timing. The Monte Carlo simulation (10,000 iterations, p=1.0) tested a different question — whether the pre/post ratio of 54% was anomalous — and its null result remains valid for that specific test. All timing findings are classified as exploratory (no prospective pre-analysis plan).

### Control group analysis

We compare the donation rate of subsidy beneficiaries to the baseline donation rate of all businesses in the state, using Census County Business Patterns (CBP) data as the denominator.

**This ratio is always an upper bound.** CBP counts employer establishments — businesses that file payroll taxes. It excludes sole proprietors, single-member LLCs, and other non-employer entities that appear in campaign finance records. The true baseline business donation rate is likely higher than CBP implies, which means the true beneficiary-to-baseline ratio is likely lower than what we report. We label all such ratios "upper bound" throughout the site.

**State-specific denominator notes:** North Carolina's control group ratio is approximately 0.1× — meaning beneficiaries donate at a *lower* rate than the CBP baseline. This is a denominator artifact: the NC GJF dataset contains a large number of small tax credit recipients (including many individual filers) that inflate the beneficiary count well above the universe of politically active businesses. The 574 matched donors and $46.3M donated are accurate; the ratio should not be interpreted as evidence that NC beneficiaries are less politically active than average. The per-company spike analysis (29 BH-significant companies) is unaffected by this denominator issue.

### What statistical significance means here

A company flagged as statistically significant had a donation pattern in the years around its award that is unlikely to be explained by random variation in its own historical giving. It does not mean the donation caused the award, that any official behaved improperly, or that the award was unwarranted. All individuals and entities are presumed to be engaged in lawful activity.

### Regression analysis (Stata)

In addition to the descriptive pipeline, we estimate formal regressions using Stata to test whether the donation gap survives statistical controls.

**Main result (OLS with individual-level controls):** Using 438,714 unique organization donors from the NYSBOE campaign finance database as a control group, we estimate that IDA subsidy recipients donate approximately 130% more than non-recipient organizations in the same county and era (OLS β = 0.83, p < 0.001, with county and decade fixed effects). This gap is robust across six specifications with different control sets.

<iframe src="/data/viz_coefficient_stability.html" width="100%" height="520" frameborder="0" style="max-width: 920px;"></iframe>

**Donation probability:** A logit model estimates that IDA recipients are 19 percentage points more likely to be substantive donors ($1,000+) than comparable non-recipient organizations (average marginal effect, p < 0.001).

<iframe src="/data/viz_donation_rate.html" width="100%" height="470" frameborder="0" style="max-width: 720px;"></iframe>

**Dose-response:** Among IDA recipients, larger subsidies are associated with larger donations (β = 0.057 per log-dollar of subsidy, p < 0.001). A 10% increase in subsidy amount is associated with a 0.6% increase in donation amount.

<iframe src="/data/viz_dose_response.html" width="100%" height="520" frameborder="0" style="max-width: 770px;"></iframe>

**Timing (event study):** An event study using monthly donation data around IDA approval dates finds no significant concentration of donations in the months immediately before approval. The donation gap is in *rate* (recipients donate more overall), not *timing* (donations are not clustered before approval). This result is reported as a valid negative finding.

<iframe src="/data/viz_event_study.html" width="100%" height="470" frameborder="0" style="max-width: 870px;"></iframe>

**School district panel:** A district-level panel analysis (2017–2022, 147,000+ district-year observations) found no statistically significant reduction in per-pupil property tax revenue associated with IDA exemptions after controlling for district fixed effects. This is consistent with districts adjusting tax rates to offset lost base — shifting the burden to homeowners rather than experiencing a budget cut.

**Caveats:** All regression results document correlation, not causation. The NYSBOE control group is composed of politically active organizations (those that appear in campaign finance records at all); comparing IDA recipients to this universe gives a lower bound on the gap relative to all businesses. Results are robust to exact-match-only (conservative) and placebo (random treatment) specifications.

---

## Reproducibility

All analysis uses Python with only the standard library. The Git repository at [github.com/The-Public-Ledger/thepublicledgers.org](https://github.com/The-Public-Ledger/thepublicledgers.org) contains all site data files and their complete change history — each data refresh is committed with a message describing what changed and when, providing a timestamped record of every published figure.

Analysis scripts are available on request at [editor@thepublicledgers.org](mailto:editor@thepublicledgers.org). All source data is publicly downloadable from the agencies listed above. No proprietary tool or paywalled source is required to reproduce our findings.

Aggregated outputs — county scorecards, beneficiary-donor crossref summaries, tax shift calculations — are available for download on the [Data page](/data/).

---

## How to cite this work

**For a specific state or county finding:**

> The Public Ledgers. "[State] IDA Accountability." *thepublicledgers.org/ida/states/[abbr]/*. Data current as of [date shown on page]. Accessed [your access date].

**For the methodology:**

> The Public Ledgers. "Methodology." *thepublicledgers.org/methodology/*. Accessed [your access date].

**For the national aggregate:**

> The Public Ledgers. "IDA Accountability: Multi-State Analysis." *thepublicledgers.org/ida/*. Accessed [your access date].

If you are using our data in a published work and want us to verify specific figures, contact [editor@thepublicledgers.org](mailto:editor@thepublicledgers.org).

---

## Malpractice Accountability {#malpractice}

### Data sources

The Malpractice Accountability investigation cross-references two federal datasets:

- **OIG LEIE** (List of Excluded Individuals/Entities): Physicians and other healthcare providers barred from participating in Medicare, Medicaid, and all federal healthcare programs. Maintained by the HHS Office of Inspector General. Available at oig.hhs.gov/exclusions/.
- **CMS NPPES** (National Plan and Provider Enumeration System): The national registry of all healthcare providers in the United States. Each provider has a unique 10-digit National Provider Identifier (NPI). Available at npiregistry.cms.hhs.gov/.

### What "active NPI" means and does not mean

An active NPI record means the provider's registration in the federal provider registry has not been deactivated. It does **not** confirm the physician is currently seeing patients. NPIs may remain active for:

- Billing and claims processing (the physician may be in a supervisory role)
- Research or academic appointments
- Teaching or administrative roles
- Credentialing purposes at hospitals or insurers
- Transition periods between practice settings

An active NPI after exclusion is a signal that warrants investigation — it means the registry has not been updated to reflect the exclusion. It is not proof of ongoing patient care.

### Matching methodology

Physician names in the LEIE and NPPES are matched using a three-step process:

1. **Name normalization**: Convert to uppercase, strip punctuation, remove common suffixes (MD, DO, Jr, Sr, etc.)
2. **Exact match**: Normalized names are identical
3. **Fuzzy match**: Word overlap above 85% threshold, with phonetic fallback for common name variants

Each match is assigned a **confidence score** (0–100). The site displays high-confidence matches only (score ≥ 80). Lower-confidence matches are available in the full data download on the [Data page](/data/).

### Exclusion types

Federal exclusions fall into two categories:

**Mandatory exclusions** (Section 1128(a) of the Social Security Act): Required by statute. Include convictions for: patient abuse or neglect, healthcare fraud, obstruction of a healthcare investigation, or unlawful distribution of controlled substances. These exclusions are indefinite (minimum 5 years for first offense).

**Permissive exclusions** (Section 1128(b)): Discretionary. Include license revocation or suspension by a state board, default on federal student loans, financial misconduct in federal health programs, and other offenses. Duration varies.

The site labels each match by exclusion type (1128(a)(1) = program-related crime/Medicare-Medicaid fraud, 1128(a)(2) = patient abuse, 1128(a)(3) = felony healthcare fraud, 1128(a)(4) = drug felony, 1128(b)(4) = license action).

### State board data

Where available, state medical board disciplinary records are cross-referenced against LEIE matches to identify physicians flagged by both federal and state authorities ("double-flagged"). State board data coverage varies; see individual state pages for details.

### Pharmaceutical payments

CMS Open Payments data (2018–2024) is cross-referenced against LEIE matches to identify excluded physicians who received payments from drug and medical device companies after their exclusion date.

---

## Corrections and methodology updates

Factual errors are corrected promptly. Corrections are noted at the top of the affected page with the date, what was wrong, and what is correct. Requests go to [editor@thepublicledgers.org](mailto:editor@thepublicledgers.org) with supporting documentation.

Methodology updates — where the analytical approach is refined rather than an error corrected — are logged here.

| Date | Change |
|------|--------|
| 2026-03-27 | North Carolina control group ratio (0.1×) documented as denominator artifact in state-specific notes. Georgia state dashboard updated to reflect state campaign finance totals ($7.78M to state committees); federal FEC donations ($13.5M) are tracked separately in the Georgia crossref outputs. |
| 2026-03-18 | Florida, Illinois, Ohio, and Pennsylvania state-level donor and donation totals updated. County-level CSV aggregation was undercounting: FL and IL county scorecard files do not include donation total columns; PA county scorecard lacks beneficiary location fields (all counties showed zero beneficiaries). State totals are now derived from beneficiary-donor crossref files, which are more complete. County-level figures are unchanged. |
| 2026-03-17 | Illinois donation total revised from $245.7M to $115.8M after systematic false positive audit. Pre-award spike count updated using unified pipeline with Benjamini-Hochberg correction: 116 companies BH-significant at q < 0.05. Prior figure of "30 of 103 at p < 0.01" was from a state-specific script without BH correction. |
| 2026-03-17 | Pre-award spike analysis rerun for Texas, North Carolina, Georgia, Michigan, and 14 additional states using the unified pipeline with BH correction. Prior state-specific results superseded. |
| 2026-04-08 | Illinois spike analysis rerun using nonparametric test with BH correction. Result: 196 ratio-based spikes, 0 BH-significant (was 116 under z-score test). Methodology section updated to document the z-score → nonparametric transition. |
| 2026-04-08 | Florida beneficiary-donor crossref rerun with canonical normalization. Match rate revised from 39.2% to 36.1%. |
| 2026-04-08 | Opioid headline allocation corrected from $5.6B to ~$5.4B after removing WV Wyoming County $274.6M data entry error (confirmed by WV First Foundation as erroneous in source PDF). |
