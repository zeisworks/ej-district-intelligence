# Edward Jones District Intelligence — Missouri

Interactive congressional district map for Edward Jones government-relations
work, built by ZeisGroup. Mirrors the Edward Jones district report series
**REP-3979T-A-E-OP** (2025 edition): a statewide view plus all eight Missouri
districts, each with office locations, report stats, and the current
representative.

**Prototype — internal review only.**

## Files

| File | Purpose |
|---|---|
| `index.html` | The app: layout, styling, and rendering logic |
| `mo-data.js` | Data: district boundaries, branch locations, city labels |

## Data sources

| Data | Source | Vintage |
|---|---|---|
| Office & client counts | Edward Jones district reports (REP-3979T-A-E-OP) | As of 2 Sep 2025 |
| Branch locations (pins) | Edward Jones branch location dataset (`FullBranchLocations_Cleaned.csv`), 745 MO locations | 2025 |
| District boundaries | U.S. Census Bureau (119th Congress), via the Lewis `congressional-district-boundaries` dataset | 2024 |
| Representatives & committees | [`unitedstates/congress-legislators`](https://github.com/unitedstates/congress-legislators) (public domain) | 119th Congress |
| City label coordinates | GeoNames | — |
| Representative photos | clerk.house.gov (by bioguide ID) | — |

Note on counts: the reports count **offices** (916 statewide); the branch
dataset counts **unique locations** (745) — multiple offices can share a
location. Stat lines use the report numbers; pins use the location dataset.
Statewide cluster bubbles are derived from branch locations by proximity and
will not exactly match the hand-clustered numbers on the printed state map.

## Refresh cadence

The source reports are dated "as of 2 Sep 2025" and expire **31 Dec 2026**
(per the compliance footer). Expect a new report series (and branch data
refresh) around September 2026. To refresh:

1. Get the new district report PDFs and branch location CSV.
2. Update the stats in the `D` object in `index.html` (values are labeled
   per district).
3. Regenerate the `offices` block of `mo-data.js` from the CSV
   (filter `STATE_ABBR == 'MO'`, group by `CDFIPS`, round to 5 decimals).
4. If districts are redrawn (next expected after the 2030 census), replace
   the `geo` block from the Census cartographic boundary files.

## Brand notes (per Edward Jones materials and proofing guidance)

- Always "Edward Jones" — never abbreviate to "EJ" in any displayed text.
- "ZIP code", not "zip-code". Current Congress is the 119th.
- Palette: Edward Jones yellow `#FFD520`, graphite `#414042`, white.
- The brand typeface is proprietary **EJ Sans** (embedded in the PDFs);
  the app uses Inter as the closest free approximation, with the body set
  light (300) to match EJ Sans Text Light. If EJ Sans webfonts can be
  licensed for this project, swap the Google Fonts link in `index.html`.
- Compliance line (REP number, expiration, ©, AECSPAD, Member SIPC) is
  carried in the footer band.
