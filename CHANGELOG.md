# The Public Ledgers — Changelog

All notable changes to [thepublicledgers.org](https://thepublicledgers.org) are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Fixed
- Deep-dive data explorers restored. Five pages rendered blank tables from two independent key-drift bugs: `deep_dive_slug` on nursing-home and water named the URL slug rather than the data-file key (so `index site.Data.deep_dives $slug` returned nil and the entire page body was skipped), and 13 of 26 declared explorer column keys named CSV headers that do not exist (the partial renders a missing key as an em-dash). Root cause fixed upstream in `export_hugo_deep_dives.py`; both classes now gated by `check_deep_dive_surfaces.py` in `make check`.
- Nursing-home Hugo export refreshed to the corrected CLAIMS figures (14,700 facilities / 5,893 low-rated / $462,082,018 penalties), replacing pre-2026-06-13 registry numbers.

### Changed
- Nursing-home explorer now shows entity-level political spending (owner LLCs, parent orgs, facilities) instead of the 775-row per-owner FEC table, which would have named individuals on an investigation with no right-of-reply outreach logged.
- Water's low-income health-violation ratio labelled as unadjusted for water-system mix and explicitly not an under-enforcement finding, per the 2026-06-18 peer review.
- Deep-dive page subheadings normalized to sentence case (20 headings across 7 pages), matching the `investigations/` section convention; proper nouns preserved

### Deploy notes
- **2026-08-26 — deployed with `make export-gate` red, deliberately.** The gate failed on one publication blocker: the open P0 *"Nursing Home: [owner name withheld pending right-of-reply] named without right-of-reply outreach"* (opened 2026-04-17; RoR outreach is its only remaining action). The blocker predates this change and is unaffected by it — this deploy *reduces* named exposure by removing the 775-person table from the rendered page. It does not close the P0: `/data/nursing_home_owner_fec.csv` is still served and still names Qazi and [owner name withheld pending right-of-reply]. Override authorized by the editor. Not a precedent — the gate stays authoritative.

## [v1.3.0] — 2026-03-20

### Added
- UX overhaul: search-first homepage design with accessibility improvements and plain-English summaries across IDA pages
- Keyboard navigation support for the interactive US tile map
- Data visualizations (bar charts, donut charts) on malpractice landing page

### Changed
- IDA state and county pages rewritten in plain English for general audiences
- Navigation cleanup across all sections
- `params.version` added to `hugo.toml`

### Fixed
- Unmapped taxonomy codes in malpractice specialty analysis resolved

## [v1.2.0] — 2026-03-19

### Added
- **Malpractice Accountability** investigation section — 2,855 excluded/disciplined physicians with active NPI records across 52 states and territories
- Malpractice tab added to the interactive data explorer
- Open Payments data backfilled for 2023 gap — now covers 7 years (2018–2024), $23.9M in industry payments

### Changed
- Malpractice dataset updated with Florida state board data: 302 new matches, 1,202 double-flagged providers total

### Fixed
- Site-wide CSS audit: consistency fixes, data directory corrections
- SEO improvements (meta tags, structured data) and responsive layout fixes

## [v1.1.0] — 2026-03-18

### Added
- Interactive US tile map on the homepage with live stats totals
- US territories added: DC, PR, VI, GU, AS, MP
- Stub pages for 20 previously missing states (fixes 404s from tile map links)
- Committee/timeline stats and county tables added to 17 partial-coverage states
- California and Nevada promoted to partial coverage with full advanced-phase data
- Per-tab filtering in the data explorer
- Expanded methodology page with multi-state coverage details and credibility documentation
- Deep Dives section with three investigations: NYS Power (utility rate capture), Epstein Network (FEC/SEC crossref), and Charges Watch (dropped charges x campaign donations)

### Changed
- **13 states promoted to Tier 1 (full county scorecards):** Alabama, Colorado, Georgia, Indiana, Kentucky, Maryland, Michigan, Minnesota, Missouri, North Carolina, Oklahoma, Virginia, Washington — now 18 Tier 1 states / 1,606 counties total
- All 50 state JSON files refreshed with corrected FL/IL/OH/PA stats — county-level CSV aggregation was undercounting; state totals now derived from beneficiary-donor crossref files
- Illinois state page updated with BH-corrected pre-award spike count (116 companies at q < 0.05)
- GA, TX, OK, MO, MI state page descriptions updated with real pipeline data
- Arkansas, North Dakota, Utah updated with committee/timeline stats from completed pipelines
- Minnesota county data completed (55 of 61 counties)
- Google Analytics enabled (G-JN2882LHD9)

### Fixed
- Illinois donation total corrected from $245.7M to $115.8M after systematic false positive audit (seven categories of common-name collisions identified and removed)
- Pre-award spike analysis rerun for TX, NC, GA, MI, and 14 additional states using the unified pipeline with Benjamini-Hochberg correction; prior state-specific results superseded
- TX `pct_beneficiaries_donating` corrected — duplicates removed by beneficiary
- `pct_beneficiaries_donating` across all states corrected — denominator changed to total beneficiaries
- Aggregate timing analysis language clarified: the beneficiary-group-level pre-award pattern is not statistically significant

## [v1.0.0] — 2026-03-16

### Added
- **Initial launch of thepublicledgers.org**
- Site scaffold: Hugo static site with custom layouts, CSS design system, vanilla JS filtering
- IDA Accountability dashboard with 30-state coverage
- Real IDA data populated for all 50 states and 439 counties
- Interactive data explorer with county filtering and state-to-county drill-down
- Donorbox donation widget on the support page
- GitHub Actions workflow for automatic deployment to GitHub Pages

### Fixed
- Default static Pages workflow removed (was overwriting Hugo build output)
