# The Public Ledgers — Changelog

All notable changes to [thepublicledgers.org](https://thepublicledgers.org) are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Changed (2026-11-11 — Malpractice refreshed on the November NPI registry; Faith FEC floor refreshed)
- Malpractice headline 2,953 → **2,945** excluded providers with MD/DO credentials and active NPI records (high-confidence 2,703 → 2,694, medium 250 → 251), re-matched on the CMS NPI registry's November 2026 release with the same OIG exclusion list (2026-11-01) and state-board files. Nine excluded physicians' NPI records left the registry extract. Dependent figures: patient abuse 149, healthcare fraud 211, drug felonies 544, moved state after exclusion 757 (25.7%), double-flagged 1,092, industry payments $18,741,590 to 1,214 physicians (64,896 records), of which $3,212,351 (544 physicians, 10,518 payments) was paid after exclusion.
- The named-record check now runs in the matcher and uses each provider's registered other names. The record first flagged as a possible different person matches under the provider's registered professional name and is listed again; four records without corroborating names remain withheld from named listings until verified.
- Faith: federal contributions floor 63,428 → 63,427 records ($6.76M unchanged at the precision shown), on the FEC's November 8 republication of the 2022 and 2024 cycles.

### Fixed (2026-11-11 — named-record identity check; Faith explorer scope)
- **Malpractice: five physician records withheld from named listings pending identity verification.** An identity check of every named record found five where the name published (from the CMS NPI registry) shares no name with the name on the OIG exclusion record for that NPI. *Correction, same day:* this entry first said one of the five was a different physician; it is the same person, whose NPI registry record lists the exclusion-record name as an official professional name. All five were removed from the search explorer, the state priority and payment lists and the top-50 download until each is verified at oig.hhs.gov; headline counts are unchanged. Names no longer show a stray "nan" where a middle name is missing.
- **Faith: the data explorer now says which counties have an ER.** It described all 68 rows as counties where the only emergency room is religious-operated; in 5 the only hospital is religious but has no ER. The description now states 68 / 63 / 5, and a new "ER status" column marks each row.

### Fixed (2026-11-10 — Faith: 68-county totals attached to the 63-county claim)
- The Faith page said religious hospitals "receive $34.5B annually … as the sole emergency room provider in 63 counties … covering 3,073,802 residents". Both totals are 68-county figures (63 counties where every ER is religious, plus 5 where the religious hospital is the only hospital but has no ER). Corrected: **63 counties / 25 states / 2,824,567 residents / $30.2B a year** for the only-ER claim, with the 68-county total ($34.5B / 3,073,802) stated as such. The same mis-scope was in the stat bar ("$35B public funding to sole religious ERs" → $30B) and the page's hub stat (shown on /investigations/) and description — all fixed. (`key_stats.desert_residents` also feeds the `at-a-glance` partial, which no layout currently renders.) Figures unchanged in substance; only their scope was wrong. Reproduced from the pinned March 2026 inputs; CLAIMS rows 18–19. Exporter `34_export_hugo_faith.py` now derives the 63-county subset itself so a re-export cannot revert it.

### Changed (2026-11-09 — Malpractice November refresh, promoted by the editor after the Phase B audit)
- Malpractice headline 2,884 → **2,953** excluded providers with MD/DO credentials and active NPI (HIGH 2,703 + MEDIUM 250), re-matched on OIG LEIE 2026-11-01 (8,255 currently-excluded physicians, +82) and the August-2026 NPPES dissemination; same matcher and thresholds. Dependent figures regenerated through the full chain: patient abuse 150 (unchanged), healthcare fraud 207 → 212, drug felonies 548 → 546, cross-state migrants 732 → 758 (25.7%), double-flagged 979 → 1,095 (CA 530 / FL 194 / NY 371 adverse actions on 1,250 state-board matches — the June per-state split was not preserved, so the composition of the +116 is recorded as unverified in CLAIMS row 16), industry payments $18,560,052 / 1,155 physicians / 61,252 records → **$18,967,581 / 1,215 / 65,271** (post-exclusion $3,199,304 → $3,212,427 / 10,526 payments). 52 state dashboards, the explorer (2,703 HIGH-confidence records) and the static CSVs re-exported.
- Two refresh-pipeline defects fixed upstream the same day and recorded in the project ERROR_LOG: the November LEIE file's new `0` no-date sentinel had been parsed as "reinstated" for every physician (would have zeroed the headline), and the Open Payments streamer could overwrite its last good output with a fragment on a timeout. Audit record: `audits/2026-11-09/phase-b/`.

### Fixed (2026-11-09 — Phase A portfolio audit, test M2: retired figures on live surfaces)
- **Water deep-dive: retracted framing removed.** The "Demographic disparities" section stated the result retracted on 2026-06-22 as the finding — β=0.031 (p<0.001) "stable across five robustness specifications", and "POC predicts *fewer* detected health violations … the opposite of the under-enforcement hypothesis" (the 0.63x composition artifact). Replaced with the peer-reviewed re-estimate (SDWA-only, N=2,993, β=0.0146, p=0.032, POC null) and a dated correction paragraph that says what was wrong and why. `data/water/summary.json` no longer carries `poc_health_disparity_ratio: 0.63` (key replaced by a retraction note; no layout read it). CLAIMS rows 49/61.
- **Nursing-home deep-dive: superseded roster removed.** `nursing_home.json` carried the 2026-03-29 owner-FEC figures (775 owners / $12,509,417, "high-confidence") three re-derivations after they were superseded; now 704 PRIMARY owners / $13,190,299 at the declared 2019–2024 scope (CLAIMS row 90, re-derived 2026-08-03). Page description and the About page said 14,710 facilities; the registry has been 14,700 since 2026-06-13 (the JSON already said so — page/data inconsistency).
- Audit record: `audits/2026-11-09/phase-a/` in the project repo.

### Changed
- Erie County, NY and its five town IDA dashboards (Amherst, Clarence, Concord, Hamburg, Lancaster) restored as uniform pipeline output with an inline candidacy disclosure (withheld 2026-06-09 → 2026-09-06). Data regenerated 2026-09-06 — same underlying figures as the 2026-06-13 export; Erie rows re-added to the New York state county list. The Erie-specific investigation article and the Erie call-outs on the IDA overview remain withheld under the researcher's candidacy recusal; see the root project `CLAUDE.md` 2026-09-06 amendment.
- NYS Power deep-dive card synced to CLAIMS: state campaign contributions $8.13M / 44 entities / 8,397 donations (was $8.32M / 46 / 8,465), NY rate 25.19¢/kWh (was 26.49, a 2025 provisional figure), and the FEC federal-contributions total replaced — the withdrawn $32.2M is now $18.55M across 148,680 contributions (CLAIMS row added 2026-09-06), with a body paragraph stating that this is individual giving aggregated by self-reported employer, not corporate or PAC money.

### Fixed
- Deep-dive data explorers restored. Five pages rendered blank tables from two independent key-drift bugs: `deep_dive_slug` on nursing-home and water named the URL slug rather than the data-file key (so `index site.Data.deep_dives $slug` returned nil and the entire page body was skipped), and 13 of 26 declared explorer column keys named CSV headers that do not exist (the partial renders a missing key as an em-dash). Root cause fixed upstream in `export_hugo_deep_dives.py`; both classes now gated by `check_deep_dive_surfaces.py` in `make check`.
- Nursing-home Hugo export refreshed to the corrected CLAIMS figures (14,700 facilities / 5,893 low-rated / $462,082,018 penalties), replacing pre-2026-06-13 registry numbers.

### Changed
- Nursing-home explorer now shows entity-level political spending (owner LLCs, parent orgs, facilities) instead of the 775-row per-owner FEC table, which would have named individuals on an investigation with no right-of-reply outreach logged.
- Water's low-income health-violation ratio labelled as unadjusted for water-system mix and explicitly not an under-enforcement finding, per the 2026-06-18 peer review.
- Deep-dive page subheadings normalized to sentence case (20 headings across 7 pages), matching the `investigations/` section convention; proper nouns preserved

### Deploy notes
- **2026-08-26 — deployed with `make export-gate` red, deliberately.** The gate failed on one publication blocker: an open P0 covering a named nursing-home owner awaiting right-of-reply outreach (opened 2026-04-17; that outreach is its only remaining action). The blocker predates this change and is unaffected by it — this deploy *reduces* named exposure by removing the 775-person table from the rendered page. It did not close the P0: the underlying owner-FEC CSV was still served at that point and still named individuals. Override authorized by the editor. Not a precedent — the gate stays authoritative.

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
