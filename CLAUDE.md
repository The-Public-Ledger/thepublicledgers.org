# The Public Ledgers — Hugo Site

## Overview
**thepublicledgers.org** — Independent data journalism tracking public money, corporate influence, and government accountability through public records. Hugo static site deployed to GitHub Pages.

- **Repo**: `github.com/The-Public-Ledger/thepublicledgers.org`
- **Local path**: `/Users/zachbeaudoin/projects/public-ledger/site/v1/the-public-ledgers/`
- **Hugo version**: 0.153.1 extended
- **Deployment**: GitHub Actions on push to `main` → GitHub Pages
- **Domain**: thepublicledgers.org (CNAME in `/static/CNAME`)

## Tech Stack
- Hugo static site generator (no themes, fully custom layouts)
- Vanilla JS for client-side filtering/search (no npm, no webpack)
- CSS custom properties design system in `assets/css/bundle.css`
- All data as Hugo `/data/` JSON or `/static/data/` JSON/CSV for client-side fetch
- GitHub Pages via GitHub Actions (`.github/workflows/deploy.yml`)

## Build & Dev
```bash
# Dev server
/opt/homebrew/bin/hugo -s /Users/zachbeaudoin/projects/public-ledger/site/v1/the-public-ledgers server

# Production build
/opt/homebrew/bin/hugo -s /Users/zachbeaudoin/projects/public-ledger/site/v1/the-public-ledgers --minify

# Deploy: push to main — GitHub Actions auto-deploys
git push
```

**Always use the `-s` flag or `cd` into the site directory before running hugo.** The binary is at `/opt/homebrew/bin/hugo`.

**IMPORTANT**: Do not use `lang.FormatNumberCustom` in templates — it is broken on Hugo 0.153. Use `printf "%.Nf"` or `lang.FormatNumber` instead.

## Directory Structure
```
the-public-ledgers/
├── hugo.toml                        # Site config, menus, taxonomies
├── CLAUDE.md                        # This file
├── assets/
│   └── css/bundle.css               # Full design system (CSS custom properties)
├── content/
│   ├── _index.md                    # Homepage
│   ├── investigations/              # Narrative investigations (stories)
│   │   ├── _index.md
│   │   ├── ida-accountability.md    # IDA overview piece (LIVE)
│   │   └── erie-county-schools.md   # Erie County flagship (LIVE)
│   ├── ida/                         # IDA data dashboards
│   │   ├── _index.md                # IDA landing with national stats
│   │   ├── states/
│   │   │   ├── _index.md            # State listing
│   │   │   └── {abbr}.md            # One per state (50 + territories)
│   │   └── counties/
│   │       └── {abbr}/
│   │           ├── _index.md        # County listing per state
│   │           └── {slug}.md        # One per county (1600+ Tier 1)
│   ├── malpractice/                 # Malpractice Accountability dashboards
│   │   ├── _index.md                # Landing page with national stats + US map
│   │   └── states/
│   │       ├── _index.md            # State listing (sortable by rate)
│   │       └── {abbr}.md            # One per state (52 total)
│   ├── deep-dives/                  # Long-form investigation cards
│   │   ├── _index.md                # Deep-dive listing
│   │   ├── malpractice.md           # Malpractice deep-dive (LIVE)
│   │   ├── epstein-network.md       # Epstein network (active)
│   │   ├── nys-power.md             # NY utility rates (active)
│   │   ├── charges-watch.md         # Dropped charges (pipeline-built)
│   │   ├── charter-school.md        # Charter school accountability
│   │   ├── nursing-home.md          # Nursing home accountability
│   │   └── water-environmental-justice.md  # Water & environmental justice
│   ├── epstein/                     # Epstein investigation stub
│   ├── insider-trading/             # Insider trading stub
│   ├── about/, methodology/, privacy/, standards/, support/
│   └── data/                        # Interactive data explorer
├── data/
│   ├── national/                    # ida_summary, bad_deals, triple_dippers,
│   │   │                              multi_state_companies, school_districts
│   ├── states/
│   │   └── {abbr}.json              # 50+ state JSON files (IDA data)
│   ├── counties/
│   │   └── {abbr}/
│   │       └── {slug}.json          # 1600+ county JSON files (Tier 1 states)
│   ├── malpractice/
│   │   ├── national_summary.json    # National malpractice headline stats
│   │   └── states/
│   │       └── {abbr}.json          # 52 state malpractice JSON files
│   └── deep_dives/                  # NOTE: underscore, not hyphen
│       ├── malpractice.json
│       ├── epstein.json
│       ├── nys_power.json
│       ├── charges_watch.json
│       ├── charter_school.json
│       ├── nursing_home.json
│       └── water.json
├── layouts/
│   ├── baseof.html                  # Master template (OG, Twitter, GA4)
│   ├── index.html                   # Homepage
│   ├── _default/single.html         # Article template
│   ├── _default/list.html           # Section list template
│   ├── data/list.html               # Interactive explorer (6 datasets, vanilla JS)
│   ├── ida/
│   │   ├── list.html                # IDA landing
│   │   ├── state-dashboard.html     # State template (reads .Params.state_abbr)
│   │   ├── county-dashboard.html    # County template (reads state_abbr + county_slug)
│   │   └── states/list.html         # State listing
│   ├── malpractice/
│   │   ├── list.html                # Malpractice landing (national stats + map)
│   │   ├── malpractice-state.html   # Per-state dashboard
│   │   └── states/list.html         # State listing
│   ├── deep-dives/
│   │   ├── list.html                # Deep-dive card grid
│   │   └── single.html              # Deep-dive detail (layout: "deep-dive")
│   ├── epstein/list.html + single.html
│   ├── insider-trading/list.html + single.html
│   ├── _partials/                    # Common partials (header, footer, nav, investigation-card)
│   ├── _partials/ida/                # IDA-specific partials:
│   │   │                              breadcrumb, coverage-badge, stat-card, flag-badge,
│   │   │                              finding-card, source-citation, last-updated,
│   │   │                              data-table, filter-bar, totals-bar, us-map, us-tile-map
│   ├── _partials/malpractice/        # Malpractice partials:
│   │   │                              breadcrumb, us-map
│   └── shortcodes/
│       ├── donorbox.html             # Donorbox widget (campaign="public-ledger")
│       ├── ida-metric.html
│       ├── key-finding.html
│       ├── source-note.html
│       ├── coverage-status.html
│       └── ida-link-explore.html
├── static/
│   ├── CNAME                         # thepublicledgers.org
│   └── data/                         # Client-side datasets (fetched by explorer JS)
│       ├── ida_county_scorecards.csv
│       ├── ny_district_impact.csv
│       ├── tax_shift_by_county.csv
│       ├── malpractice_state_rates.csv
│       ├── malpractice_top_50.csv
│       ├── malpractice_migration_corridors.csv
│       ├── charter_*.csv             # Charter school data CSVs
│       ├── nursing_home_*.csv        # Nursing home data CSVs
│       ├── water_*.csv               # Water/environmental justice CSVs
│       ├── power_*.csv               # NYS power company CSVs
│       └── *.json                    # JSON datasets for explorer
└── .github/workflows/deploy.yml     # Hugo 0.153.1 → GitHub Pages
```

## Data Architecture

### Hugo /data/ (build-time, server-rendered)
Templates access data via `{{ site.Data.states.ny }}`, `{{ site.Data.national.ida_summary }}`, `{{ site.Data.malpractice.states.ny }}`, `{{ site.Data.deep_dives.malpractice }}`, etc.

**IMPORTANT**: Data directory `deep_dives/` uses underscores (not hyphens). Hugo maps both `deep-dives/` and `deep_dives/` to `site.Data.deep_dives`, but only use the underscore directory to avoid confusion.

**IDA Coverage tiers** (drives what IDA templates render):
- `"coverage_status": "full"` — full county scorecards + crossref data
- `"coverage_status": "partial"` — state-level crossref, no county scorecards
- `"coverage_status": "placeholder"` — metadata only, data collection in progress

**IDA Tier 1 states** (full county data): NY, OH, FL, IL, PA, AL, AZ, CA, CO, CT, GA, IN, KY, MD, MA, MI, MN, MO, NC, NV, OK, TX, VA, WA — 1600+ county JSON files
**IDA Tier 3 states** (placeholder): remaining states

**Malpractice**: All 52 state JSON files contain real data (excluded counts, priority cases, migration, payments).

### Refreshing data

**IDA data:**
```bash
python3 /Users/zachbeaudoin/projects/public-ledger/ida/scripts/export_hugo_data.py
```

**Malpractice data:**
```bash
cd /Users/zachbeaudoin/projects/public-ledger/deep-dive/patients/malpractice-accountability
python3 scripts/08_export_hugo_malpractice.py
```

**Deep-dive data (charter school, nursing home, water):**
```bash
python3 /Users/zachbeaudoin/projects/public-ledger/ida/scripts/export_hugo_deep_dives.py
```

Run these any time new pipeline outputs land. Zero Hugo changes needed — just run the script and push.

### Change Tracking

- **Site changelog**: `CHANGELOG.md` — all notable changes to thepublicledgers.org
- **Data lineage**: `../../DATA_LINEAGE.md` — maps how data flows from analysis to published pages
- **Data licenses**: `../../DATA_LICENSES.md` — license/terms for all data sources
- **IDA decisions**: `../../ida/DECISIONS.md` — analytical methodology decisions

### /static/data/ (client-side, fetched at runtime)
Large files for the interactive explorer + downloadable CSVs. Includes IDA county scorecards, school district data, and malpractice state rates / top 50 / migration corridors.

## Front Matter Patterns

**IDA State** (`content/ida/states/ny.md`):
```yaml
---
title: "New York"
state_abbr: "ny"
state_name: "New York"
layout: "state-dashboard"
---
```

**IDA County** (`content/ida/counties/ny/erie.md`):
```yaml
---
title: "Erie County"
state_abbr: "ny"
state_name: "New York"
county_slug: "erie"
county_name: "Erie County"
layout: "county-dashboard"
---
```

**Malpractice State** (`content/malpractice/states/ny.md`):
```yaml
---
title: "New York"
state_abbr: "ny"
state_name: "New York"
layout: "malpractice-state"
---
```

**Deep Dive** (`content/deep-dives/malpractice.md`):
```yaml
---
title: "Malpractice Accountability"
description: "..."
date: 2026-03-19
status: "active"      # active | complete | pipeline-built
deep_dive_slug: "malpractice"  # must match key in data/deep_dives/
layout: "deep-dive"
sources:
  - "OIG LEIE"
  - "CMS NPPES"
---
```

## CSS Design System

**BEM naming convention** for stat cards:
- `.stat-grid` — grid container (auto-fit, minmax 200px)
- `.stat-card` — card container
- `.stat-card__value` — large number
- `.stat-card__label` — description text
- `.stat-card--danger` — red value (patient abuse, etc.)

**Data visualization components** (pure CSS/SVG, zero JS):
- `.bar-chart` — horizontal bar chart container
- `.bar-chart__row` / `__label` / `__track` / `__fill` / `__value` — bar chart elements
- `.bar-chart__fill--accent` (green) / `--warm` (amber) / `--danger` (red)
- `.donut-section` / `.donut-chart` / `.donut-svg` — SVG donut chart
- `.donut-legend` / `__item` / `__color` / `__label` / `__count`

**UX components** (search, results, callouts):
- `.doctor-search` — physician name search bar
- `.result-card` / `--high` / `--medium` — search result cards with severity border
- `.context-callout` — explanatory callout block (left accent border)
- `.action-box` — "what to do" guidance box (blue background)
- `.no-results` — empty state message

**Exclusion badges** (malpractice):
- `.exclusion-badge--1128a2` (red — patient abuse)
- `.exclusion-badge--1128a3` (orange — fraud)
- `.exclusion-badge--1128a4` (yellow — drugs)
- `.exclusion-badge--1128b4` (gray — license)

**Accessibility utilities**:
- `.sr-only` — visually hidden, screen reader only
- `abbr[title]` — dotted underline for inline definitions
- `@media (prefers-reduced-motion: reduce)` — disables all animations

**Responsive breakpoints**: 1024px (tablet), 768px (mobile), 480px (small mobile)

**Color contrast**: `--color-text-muted` is `#5a6578` (passes WCAG AA on all backgrounds)

## Navigation Menu (hugo.toml)

**Main nav:** Investigations, Subsidies, Data, About, Accountability Index, Search

**Footer nav:** Methodology, Corrections, Editorial Standards, Ethics, Legal, Contact, Privacy, Support This Work

## Shortcodes (for use in markdown)
```
{{< donorbox >}}                              # Donation form
{{< ida-metric label="..." value="..." >}}   # Inline metric
{{< key-finding number="$12.19B" label="..." >}}
{{< source-note db="NYSBOE" date="2024-11-01" >}}
{{< coverage-status state="ny" >}}
{{< ida-link-explore state="NY" flag="triple-dipper" >}}
```

## Investigation Sections
- **`/investigations/`** — Narrative stories (Erie County flagship, IDA overview)
- **`/ida/`** — Subsidy data dashboards (state/county scorecards) — nav label "Subsidies"
- **`/malpractice/`** — Malpractice Accountability (search + 52 state dashboards + visualizations)
- **`/deep-dives/`** — Long-form investigation cards (7 active)
- **`/data/`** — Interactive explorer (7 filterable datasets including malpractice tab)
- **`/epstein/`** — Epstein network investigation (stub)
- **`/insider-trading/`** — Insider trading pipeline (stub)

## Content Standards (CRITICAL — read before writing or editing any investigation)

### The Core Rule

**Present what the data shows. Do not tell readers what to conclude.**

Every published piece must be defensible if read by the subject of the investigation, a hostile editor, or a lawyer. The standard is not "is this true?" — it is "can every claim be traced directly to a named public record, and is every interpretive leap clearly labeled as interpretation?"

---

### What Every Investigation MUST Include

1. **Named primary sources** — every factual claim cites a specific public record (Comptroller audit number, PARIS dataset ID, NYSBOE filing date, statute citation). "Public records show" is not sufficient; name the record.
2. **Baseline comparisons** — rates and percentages must include context. "40% of beneficiaries donated" requires a comparison to the general business baseline (13% for NY, per Census CBP). A number without a denominator or comparison is incomplete.
3. **Methodology note** — every investigation page links to `/methodology/` and lists the specific datasets used with record counts.
4. **Limitations acknowledged** — if matching is approximate, if data is incomplete, or if correlation cannot establish causation, say so. The limitations section is not optional.
5. **Bipartisan framing** — where the pattern crosses party lines, document it. Single-party framing of a structural problem is editorially inaccurate and legally exposing.
6. **Attribution for all quotes** — every quote tied to a named source, date, and document. No paraphrasing of quotes.
7. **"Last updated" date** — all investigation pages carry a visible last-updated date.

---

### What Every Investigation Must NOT Include

1. **First-person voice** — investigations are not op-eds. Do not write "I found" or "what I found was." Use third person: "The analysis found," "Public records show," "The Comptroller audit concluded."
2. **Editorial verdicts stated as findings** — "This isn't economic development. It's a rubber stamp" is an opinion. The Comptroller's audit findings are facts. Quote the findings; let readers draw the verdict.
3. **Intent attribution** — do not write that a company or official "directed" donations to influence outcomes, that fees are "hidden," or that a system was "designed" to benefit insiders. Document the correlation; do not assert the motive.
4. **"The data says"** — data does not say anything. Analysis draws conclusions from data. Write "the record shows" or "the analysis finds," not "the data says no."
5. **Guilt by association** — naming a family relationship (parent on court, child on board) without documenting the specific overlap in jurisdiction or decision-making implies a conflict that may not be documentable. Either cite the specific overlap or omit.
6. **Concealment language without evidence of concealment** — "invisible," "hidden," "buried" imply deliberate suppression. Use structural explanations: "does not appear in agency procurement filings because fees are paid directly by applicant companies."
7. **Loaded characterizations** — "rubber stamp," "pay to play," "slush fund," "machine" are editorial labels. If a subject used these words themselves (e.g., Poloncarz calling the Harris Beach arrangement "pay to play at its base level"), quote them with attribution. Do not apply the label as your own characterization.
8. **Predictions or projections stated as fact** — "this will result in" or "this means schools will lose" requires a source or model. Document what has happened; do not project what will happen.
9. **Emojis, sarcasm, or rhetorical questions as conclusions** — the closing question ("before we cut services, should we keep giving tax breaks...?") crosses from documentation into advocacy. Frame as documented facts, not rhetorical appeals.

---

### Author/Byline Disclosure

**Any investigation authored by someone with a direct political stake in the subject must carry a prominent disclosure at the top of the piece, not only at the bottom.**

- Byline disclosure at bottom is insufficient when the author is a candidate for office whose district or opponent is the subject.
- The disclosure should appear in a callout box immediately below the headline, before the body text begins.
- Format: *Disclosure: [Name] is a candidate for [Office]. This investigation is based solely on public records; all methodology is documented at [link].*
- This is not optional. It is the minimum standard for credibility with journalists, opposing campaigns, and readers who may share the piece.

---

### Language: Prohibited Phrases and Required Alternatives

| Prohibited | Required alternative |
|------------|---------------------|
| "The data says no / yes" | "The public record documents X" |
| "directed donations to" | "contributed to committees affiliated with" |
| "invisible / hidden fees" | "fees that do not appear in agency procurement filings because [structural reason]" |
| "This is a rubber stamp" | "The Comptroller found no formal evaluation criteria and zero clawbacks" |
| "pay-to-play" (as author's characterization) | Quote from a named source who used those words, with attribution |
| "I found / What I found" | "The analysis found / Public records show" |
| "These numbers mean X" | "These figures represent X" (factual) |
| "the same families control" | "public board rosters document family members holding [specific roles]" |
| "a system designed to benefit insiders" | "a structure in which [documented mechanism]" |
| "never says no" (as headline/subhead) | "approved 100 percent of reviewed projects, per [audit]" |
| "X percent is alarming / troubling" | Present the figure with baseline; let comparison speak |

---

### Rates and Percentages: Baseline Requirement

No percentage may appear in a published investigation without a comparison baseline. This is non-negotiable.

- If 40% of beneficiaries donated: compare to the general business donor rate (13% for NY, per Census CBP 2022; ratio = 3.1x).
- If a firm received $X in fees: compare to the agency's total spending or to peer agencies.
- If a county ranks 26th out of 104 on pay-to-play metrics: explain what the metric measures and what ranks 1st and 104th mean.
- If zero clawbacks were executed: note whether peer IDAs have executed clawbacks (context for whether this is anomalous or typical).

---

### Correlation vs. Causation

The standard language for IDA donor-beneficiary findings:

> "Companies that donated to political committees affiliated with IDA-appointing officials received $X in tax exemptions. This analysis documents a correlation between donations and exemptions; it does not establish that donations caused approvals."

This disclaimer is required on every investigation page that presents donor-beneficiary data. It belongs in the methodology note, not buried in a footnote.

---

### What the Comptroller and Other Government Audits Can Establish

Government audit findings are facts — cite them directly and attribute them precisely:
- "The NYS Comptroller audit (S9-15-70) found that ECIDA approved 100 percent of the 30 projects reviewed, had no formal evaluation criteria, and recaptured zero dollars from the 14 project owners who missed job creation targets."
- Do NOT paraphrase audit language into stronger characterizations.
- Do NOT use an audit finding about one IDA to characterize the system statewide without additional evidence.

---

### Investigation vs. Opinion: The Test

Before publishing, apply this test to every paragraph:

1. **Fact paragraph**: Every sentence cites a specific public record. No characterization of intent. No loaded adjectives. ✓ Publish.
2. **Analysis paragraph**: The paragraph draws a conclusion from documented facts. The conclusion is proportionate to the evidence. The paragraph acknowledges alternative explanations. ✓ Publish with care.
3. **Opinion paragraph**: The paragraph tells readers what to think, uses loaded language, or draws conclusions beyond what the evidence establishes. ✗ Do not publish in an investigation. Move to a clearly labeled editorial/commentary section.

---

## UX Design Principles (established 2026-03-20)
- **Search-first**: Malpractice landing shows physician search bar before any stats
- **Plain English first**: No jargon in user-facing labels. Abbreviations use `<abbr>` with tooltips.
- **Context before data**: Explanation text appears before stat cards and tables
- **"What should I do?"**: Action boxes with OIG hotline on every malpractice page
- **"No results" explains**: Empty search results explain what absence means
- **Visualizations over tables**: Bar charts and donut charts for overview data; tables for detail
- **Two audiences**: Regular users get plain English; journalists get full data in explorer

## Accessibility (WCAG 2.1 AA)
- ARIA tab pattern: `tabpanel`, `aria-controls`, roving `tabindex`, arrow key navigation
- Sort headers keyboard-operable (Enter/Space + focus restoration after re-render)
- `aria-live="polite"` on dynamic content (row counts, search results)
- Table `<caption class="sr-only">` on all data tables
- `scope="col"` on all `<th>` elements (both static and JS-rendered)
- Tile map: keyboard focus shows tooltip (focus/blur handlers)
- Flag badge `title` tooltips explain each flag type
- `prefers-reduced-motion` media query disables transitions
- Search input debounced (300ms) to avoid screen reader announcement spam
- Skip link, semantic HTML, breadcrumb `role="list"`

## Key Design Decisions
- `/investigations/` = stories, `/ida/` & `/malpractice/` = data dashboards
- Partials in `layouts/_partials/` (non-standard but existing convention — do not move)
- CSS custom properties: `--color-primary`, `--color-accent`, `--color-surface-alt`, `--font-size-*`
- No Node.js, no npm — Hugo only; `hugo --minify` is the only build step
- Data visualizations built as inline SVG/CSS at Hugo build time — zero JS charting libraries
- Donorbox campaign: `public-ledger` at donorbox.org
- `og:image` defaults to `/og-default.png` (placeholder — replace with actual image)

## Current Page Count
~3,285 pages (as of 2026-04-04):
- 50+ state IDA dashboard pages (pyramid layout with summary + stat cards + small multiples)
- 2,753 county dashboard pages (pyramid layout with benchmarks + narratives + CSV downloads)
- 52 malpractice state dashboard pages
- 7 deep-dive pages (malpractice, epstein, nys-power, charges-watch, charter-school, nursing-home, water-environmental-justice)
- IDA landing, state listings, county listings, malpractice landing
- Glossary page (`/glossary/`)
- Investigations, data explorer, search page, about, methodology, etc.

## Site Features (as of 2026-04-04)
- **Map toggle**: Tile grid (default, equal-weight) + choropleth (geographic toggle) on homepage, IDA landing, malpractice landing; `map-toggle.html` partial with ARIA radiogroup
- **County pyramid layout**: 5-layer structure — plain-language narrative → contextual stat cards (with rank, percentile gauge) → benchmark comparison bars (county vs state median) → findings/flags → data table → methodology disclosure
- **State pyramid layout**: Summary → headline stat cards → small multiples county grid (24 shown, expandable) → findings/committees/timeline → full county table → methodology disclosure
- **Auto-generated narratives**: Export script pre-computes benchmarks (state rank, percentile, medians) and narrative strings per county; stored in county JSON `benchmarks{}` and `narrative{}` fields
- **CSV download buttons**: Per-county JS blob download + bulk static CSV link on every county page; CC-BY licensed
- **Dark mode**: `prefers-color-scheme: dark` auto-detect; full custom property override (off-white text, dark bg, reduced shadows, adjusted badges/tiles/tables); no toggle button
- **Glossary**: `/glossary/` page with 25 terms in 4 categories; `{{< term >}}` shortcode for inline click-activated popovers with glossary deep-links
- **Community lookup**: Homepage widget; state→county dropdown; fetches `/data/lookup/{abbr}.json`; shows cross-investigation metrics per county
- **Data explorers**: Per-investigation embedded tables on deep-dive pages (water, charter, nursing home, opioid, nys_power, faith); `data-explorer.html` partial
- **Pagefind search**: `/search/` page; full-site index built post-deploy in CI; `data-pagefind-meta` on all investigation layouts
- **Accessibility gate**: `scripts/check_a11y.py` (axe-core JSON → exit 0/1/2); `make a11y` target; wired into ship workflow
- **Accountability Index**: Cross-investigation entity scoring (1,530 entities)

## New Partials (added 2026-04-04)
- `_partials/map-toggle.html` — tile grid ↔ choropleth toggle with ARIA radiogroup
- `_partials/ida/county-summary.html` — plain-language narrative for county pages
- `_partials/ida/stat-card-contextual.html` — stat card with context line + percentile gauge
- `_partials/ida/benchmark-bar.html` — county vs state median comparison bars
- `_partials/ida/small-multiples.html` — grid of mini county cards for state dashboards
- `_partials/ida/state-summary.html` — auto-generated state narrative summary
- `shortcodes/term.html` — inline term definition with click-activated popover

## Contact
- Email: editor@thepublicledgers.org
- Donorbox: donorbox.org/public-ledger
