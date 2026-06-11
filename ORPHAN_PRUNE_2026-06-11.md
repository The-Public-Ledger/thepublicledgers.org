# Orphan County-Page Prune — 2026-06-11

P2-b remediation from the 2026-06-09 IDA peer review. The exporter
(`ida/scripts/export_hugo_data.py`) writes 2,726 county JSONs per run, but
`data/counties/` held 2,986 — 317 orphans the exporter no longer regenerates
(frozen at their last write). Detection method: snapshot all county-JSON
mtimes, run the exporter (idempotent), diff — any file with an unchanged
mtime is an orphan. 317 orphans found; 316 pruned (JSON + matching content
stub), 1 kept pending an upstream fix. Additionally, 24 pre-existing content
stubs with NO data JSON at all (broken/empty dashboards) were pruned.

Result: `data/counties/*.json` 2,986 → 2,670; `content/ida/counties/*.md`
(excl. `_index.md`) → 2,670. Data JSONs and content stubs now correspond 1:1.

**Untouched (protected):** `data/counties/ny/erie.json` +
`content/ida/counties/ny/erie.md` (COI tombstone — must stay). NY had zero
orphans; the exporter still writes all 104 NY county files.

---

## KEPT-PENDING-UPSTREAM (1)

| Path | Why kept | Upstream fix that restores it |
|------|----------|-------------------------------|
| `data/counties/ok/oklahoma.json` (+ `content/ida/counties/ok/oklahoma.md`) | Oklahoma County carried **$250,972,052 total_subsidy** in `ok_county_scorecards.csv` (v1) but is ABSENT from `ok_county_scorecards_v2.csv` — the v2 rebuild mislabels the row as **"Oklahoma City"** (a city, not a county), so the exporter now writes `ok/oklahoma-city.json` instead. Real county with real data; deleting it would drop legitimate coverage. Page currently serves stale v1-era data. | Fix county attribution in the OK step-19 `county_scorecards.py` run so the row reads "Oklahoma" (county); regenerate `ida/states/oklahoma/outputs/ok_county_scorecards_v2.csv`; re-run exporter. Then `ok/oklahoma-city.json` + its stub become the orphans to prune. Same v2 run shows other city names contaminating the county column in NE ("Beatrice", "Blair", "Benkelman", "Fairbury", "Pilger", "Lyons", "Kearney"…) — same upstream bug, those rows currently mint bogus "county" pages. |

---

## PRUNED — class (b) defunct pages (316 JSONs + 316 stubs)

Every entry below = BOTH `data/counties/{st}/{slug}.json` AND
`content/ida/counties/{st}/{slug}.md` deleted.

### Pennsylvania — 67 (state demoted from county coverage)

Reason: PA county parser + scorecard path REMOVED from the exporter
2026-04-12 — `pa_county_scorecards.csv` was stub data (all zeros), see
`audits/2026-04-12/`. Exporter now reports "no scorecard path defined for pa"
and writes zero PA county files; all 67 pages were frozen stale stubs.
Upstream CSV no longer carrying them: `ida/states/pennsylvania/outputs/pa_county_scorecards.csv` (delisted from `COUNTY_SCORECARD_PATHS`).
Note: `content/ida/counties/pa/_index.md` retained (section index; harmless empty list).

adams, allegheny, armstrong, beaver, bedford, berks, blair, bradford, bucks,
butler, cambria, cameron, carbon, centre, chester, clarion, clearfield,
clinton, columbia, crawford, cumberland, dauphin, delaware, elk, erie (PA's
Erie County — NOT the protected NY tombstone), fayette, forest, franklin,
fulton, greene, huntingdon, indiana, jefferson, juniata, lackawanna,
lancaster, lawrence, lebanon, lehigh, luzerne, lycoming, mckean, mercer,
mifflin, monroe, montgomery, montour, northampton, northumberland, perry,
philadelphia, pike, potter, schuylkill, snyder, somerset, sullivan,
susquehanna, tioga, union, venango, warren, washington, wayne, westmoreland,
wyoming, york

### Zero-subsidy counties dropped in the v1 → v2 scorecard migration — 240

Reason: the exporter's `COUNTY_SCORECARD_PATHS` now points at each state's
`*_county_scorecards_v2.csv`, which only carries counties with subsidy data.
Verified: every county below had **$0 total_subsidy** in the v1 CSV (so the
frozen pages showed empty dashboards anyway). v1 row → v2 row counts:
MO 115→18, NE 101→40, OK 77→20, UT 28→11, ND 53→50, AK (Hoonah-Angoon $0 row
dropped).

**MO — 97** (upstream: `ida/states/missouri/outputs/mo_county_scorecards_v2.csv`):
adair, atchison, audrain, barry, barton, bates, benton, bollinger, butler,
caldwell, callaway, camden, carroll, carter, cedar, clark, clinton, cooper,
dade, dallas, daviess, dekalb, dent, douglas, dunklin, gentry, grundy,
harrison, henry, hickory, holt, howell, iron, jefferson, knox, laclede,
lafayette, lawrence, lewis, lincoln, linn, livingston, macon, madison,
maries, marion, mcdonald, mercer, miller, mississippi, moniteau, monroe,
montgomery, morgan, new-madrid, newton, nodaway, oregon, osage, ozark,
pemiscot, perry, pettis, phelps, pike, platte, polk, pulaski, putnam, ralls,
randolph, ray, reynolds, ripley, saline, schuyler, scotland, scott, shannon,
shelby, st-charles, st-clair, st-francois, st-louis, ste-genevieve, stoddard,
stone, sullivan, taney, texas, vernon, warren, washington, wayne, webster,
worth, wright

**NE — 62** (upstream: `ida/states/nebraska/outputs/ne_county_scorecards_v2.csv`):
antelope, arthur, banner, blaine, boone, boyd, brown, butler, cass, cedar,
chase, cherry, clay, cuming, deuel, dixon, dundy, fillmore, franklin,
frontier, furnas, garden, garfield, gosper, grant, greeley, harlan, hayes,
hitchcock, holt, hooker, howard, jefferson, johnson, keith, keya-paha,
kimball, knox, logan, loup, mcpherson, merrick, morrill, nance, nuckolls,
pawnee, perkins, phelps, pierce, polk, richardson, rock, sheridan, sherman,
sioux, stanton, thayer, thomas, thurston, valley, webster, wheeler

**OK — 57** (upstream: `ida/states/oklahoma/outputs/ok_county_scorecards_v2.csv`):
adair, alfalfa, atoka, beaver, beckham, blaine, bryan, caddo, canadian,
carter, cherokee, choctaw, cimarron, cleveland, coal, comanche, cotton,
craig, creek, custer, delaware, dewey, ellis, garvin, grady, grant, greer,
harmon, harper, haskell, hughes, jackson, jefferson, johnston, kay,
kingfisher, kiowa, latimer, le-flore, lincoln, logan, love, major, mayes,
mcclain, mccurtain, mcintosh, osage, pawnee, pontotoc, pottawatomie,
pushmataha, roger-mills, sequoyah, tillman, wagoner, woods
(ok/oklahoma excluded — see KEPT-PENDING-UPSTREAM)

**UT — 18** (upstream: `ida/states/utah/outputs/ut_county_scorecards_v2.csv`):
beaver, box-elder, daggett, duchesne, emery, garfield, grand, juab, kane,
millard, morgan, piute, rich, san-juan, sevier, uintah, wasatch, wayne

**ND — 4** (upstream: `ida/states/north-dakota/outputs/nd_county_scorecards_v2.csv`):
adams, golden-valley, lamoure, slope

**AK — 1** (upstream: `ida/states/alaska/outputs/ak_county_scorecards_v2.csv`):
hoonah-angoon (v1 row "HOONAH ANGOON" had $0 subsidy; dropped in v2)

### "Statewide" pseudo-county pages — 5

Reason: v1 generic scorecards carried a STATEWIDE aggregate row that the
generic parser exported as a fake county page; the v2 CSVs no longer emit it.
- al/statewide (upstream: `al_county_scorecards_v2.csv`)
- az/statewide (upstream: AZ v2 scorecard)
- md/statewide (upstream: `md_county_scorecards_v2.csv`)
- mn/statewide (upstream: MN v2 scorecard)
- mo/statewide, ok/statewide (counted in the MO/OK lists' upstream CSVs above)

### Renamed slugs (duplicate pages superseded by the current slug) — 4

| Deleted | Superseded by (current exporter output) |
|---------|------------------------------------------|
| ia/o-brien | ia/obrien.json |
| il/dewitt | il/de-witt.json |
| nm/doña-ana | nm/dona-ana.json |
| nv/carson | nv/carson-city.json |

---

## PRUNED — pre-existing content stubs with NO data JSON (24 stubs, no JSON existed)

These were not part of the orphan-JSON set: stubs Hugo would render as
broken/empty dashboards because no data JSON has ever matched them.

- **az/ — 13 cross-state contamination** (CO and AL county names that never
  belonged to Arizona; no AZ scorecard row, no JSON): baca, bent, boulder,
  chaffee, cheyenne, clear-creek, conejos, costilla, marion, mobile,
  montgomery, talladega, tuscaloosa
- **ca/ — 2 aggregate pseudo-counties** (CA parser explicitly skips these
  rows): multiple-counties, statewide
- **ct/ — 9 planning regions** (site uses CT's 8 legacy counties; no
  planning-region JSONs exist): capitol-planning-region,
  greater-bridgeport-planning-region,
  lower-connecticut-river-valley-planning-region,
  naugatuck-valley-planning-region, northeastern-connecticut-planning-region,
  northwest-hills-planning-region, south-central-connecticut-planning-region,
  southeastern-connecticut-planning-region, western-connecticut-planning-region
  (if CT ever migrates to Census planning-region county-equivalents upstream,
  the exporter will recreate these stubs automatically)

---

## Verification

- Exporter run (orphan detection): the summary line reports "Total county
  JSON files: 2726", but that counter sums per-state `counties_with_data`
  (which includes ECHO-only counties that live in the state JSON's `counties`
  array without a per-county file). The mtime diff shows 2,669 distinct
  on-disk county JSONs were actually (re)written, 0 new files created.
  On-disk truth post-prune: 2,670 JSONs (2,669 exporter-written + 1 kept
  ok/oklahoma.json) / 2,670 stubs (1:1).
- 1:1 pairing verified post-prune: 2,670 json/stub pairs, 0 json-only,
  0 stub-only.
- Hugo rebuild PENDING — the agent session executing this prune could not
  invoke `hugo` (tool permission denied). Run
  `/opt/homebrew/bin/hugo -s site/v1/the-public-ledgers --minify` to drop the
  stale pages from `public/` (expected: ~3,265 → ~2,925 pages under
  /ida/counties/; pruned URLs like /ida/counties/pa/erie/ and
  /ida/counties/mo/adair/ should 404; /ida/counties/ny/erie/ and
  /ida/counties/ok/oklahoma/ must still render).
- Note: county data JSONs and county content stubs are gitignored — these
  deletions do not appear in git status and need no commit.
