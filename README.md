# Evaluating Bank Distress from Regulatory and Market Data

Research assistantship with Prof. Jihad Dagher, Department of Economics, University of Southern California (April 2024 – June 2025). Part of the data layer for a study of whether brokered deposits make bank funding less stable, since published as *Beyond Hot Money: Brokered Deposits and Bank Funding Stability* (Dagher and Fuster, 2026, SFI Research Paper 26-22). The HMDA and DealScan work in this repository belongs to a separate strand of the same project.

Project page with the full write-up: https://twyla123.github.io/Digital_Portfolio_Twyla/projects/bank-distress.html

## At a glance

| | |
|---|---|
| **341 of 413** lender IDs matched to one institution each | tiered ID matching (holding company 242 → bank 15 → subsidiary walked up the ownership tree 3) plus a credit-union cross-check (81); the remaining 72 are listed as unresolved rather than forced |
| **10** regulatory and market datasets joined | FFIEC Call Reports, FR Y-9C, NIC relationships, FDIC, NCUA, NY Fed CRSP–FRB link, HMDA, CRSP/Compustat, LPC DealScan, plus a proprietary lines-of-credit file; totals checked against SEC 10-K filings |
| **12 years** of HMDA loan-level records standardized | 2012–2023 lender × MSA × year panel, aligned field by field across the 2018 reporting-standard break |
| **441 of 28,568** DealScan deals (1.54%) flagged | more distinct tranche-active dates than deal-input dates: a recording gap in the source that would inflate apparent time variation in firm-time fixed effects |

## Start here

| Question | Notebook | Output |
|---|---|---|
| How were the 413 lenders matched? | `LOC_Analysis_ID_Matching/LOC_Analysis.ipynb` (refined framework; `LOC_Analysis_old.ipynb` is the run that wrote the committed table) | `LOC_Analysis_ID_Matching/LOC_Matching_All.csv` (`Match_Type` column) |
| Which lenders are publicly traded? | same notebook, CRSP–FRB merge | `LOC_Public_Traded_Merged_Matched_Rows.csv` (132 rows) |
| How were names matched when IDs failed? | `LOC_Analysis_Name_Matching/LOC_Analysis_Name_Matching_0710.ipynb` | `LOC_*_Name_Matching.csv` |
| How do Call Reports link to FR Y-9C filers? | `background/matching.ipynb` | `call_FR_combined.csv`, `background/FR_Report.csv` |
| How was HMDA aligned across 2018? | `HMDA/Analyze.ipynb` (schema inventory, filters, verification) | `HMDA/column_names_summary.csv`, `HMDA/merged_panel_ts_files/`, `HMDA/report/` |
| Can DealScan support firm-time fixed effects? | `DealScan/tranche _explore_full_data.ipynb`, `tranche_sample.ipynb`, `consolidated_preprocess.ipynb` | notebook outputs cleared (licensed data); results recorded in the notebook text |

## Data

**Public, included or reproducible:** FFIEC Call Reports (`background/COM/`, 2017 quarterly `.xpt`), FR Y-9C (`background/HOLD/`), NY Fed CRSP–FRB link (`LOC Credit Union Data/crsp_20161231.csv`), NCUA credit-union roster, HMDA Panel and Transmittal Sheet merges (`HMDA/merged_panel_ts_files/`). HMDA LAR source files are multi-gigabyte public downloads from ffiec.cfpb.gov and are not committed.

**Licensed or proprietary, not included:** LPC DealScan (licensed through WRDS), CRSP/Compustat (WRDS), and the lines-of-credit file. The DealScan notebooks are kept with their outputs cleared; the summary figures they produced are quoted in the notebook text. No row-level licensed data is in this repository or its history.

## Method in one paragraph

Every source identifies a bank with its own key at its own level of the ownership tree: RSSD at bank level, RSSD at holding-company level, FDIC certificate, NCUA number, PERMCO, ticker, LEI, HMDA respondent ID, DealScan lender-parent ID. The work was deciding, pair by pair, what "the same institution" means, and making each decision auditable: every match carries a tier label, every ambiguous case is written out for inspection, and every filter has a verification pass that prints what survived. Rolled-up totals were compared against the FR Y-9C, FDIC and Call Report versions of the same quantity, and spot-checked against nine 10-K filings.

## Repository map

```
background/                    Call Report ↔ FR Y-9C linkage (matching.ipynb), raw 2017 quarterlies, MDRM dictionary
LOC_Analysis_ID_Matching/      tiered lender matching, the 413-row match table, publicly traded flags
LOC_Analysis_Name_Matching/    normalized and fuzzy name matching against Y-9C, Call Report, credit unions
LOC Credit Union Data/         NCUA roster, NY Fed CRSP–FRB link
HMDA/                          schema inventory across 2011–2023, Panel ⋈ Transmittal Sheet merges, verification reports
DealScan/                      cleaning and fixed-effects feasibility notebooks (outputs cleared), variable dictionaries
```

## Tools

Python (pandas, numpy, fuzzywuzzy, statsmodels). Formats handled: `.xpt`, `.dta`, `^`-delimited, `|`-delimited, tab-delimited, zipped bulk archives, `.xls`/`.xlsx`, a REST API.

## Changelog

- **2026-09-11** Removed licensed and proprietary data from the repository and its history (DealScan tranche extracts and quarterly summaries, `LOC.dta`); DealScan notebooks re-added with outputs cleared. README rewritten to match the project page; an unsupported figure about HMDA record counts was removed.
- **2026-09-11** Minimal fixes, no change of method: (1) `background/matching.ipynb`: `FR_Report.csv` is now written after the `parent_id` backfill instead of before it; the backfill rule from that cell (`parent_id = id` where `parent_id` was 0) was applied to the two committed copies of `FR_Report.csv` (root: 641 rows, 633 backfilled; `background/`: 4,597 rows, 4,302 backfilled); file paths made relative to the notebook's folder; the "10085 zero parent ids" note corrected to 4,302 for the single-quarter file. Known: the two committed `FR_Report.csv` files come from different variable lists and the saved notebook does not reproduce either exactly. (2) `LOC_Analysis_Name_Matching/LOC_Analysis_Name_Matching_0710.ipynb`, cell 21: exact matches carry `normalized_name` rather than `normalized_name_x`, so they were being listed as unmatched; fixed with a `fillna`; paths made relative. (3) `LOC_Analysis_ID_Matching/LOC_Analysis.ipynb`: paths made relative; the credit-union relabel now applies only to rows still unmatched, as its comment says; the `No Match` mask in the Call Report step is recomputed before the subsidiary pass so a row just labelled `Call_Parent` cannot be overwritten (no change to the committed counts). All three fixes were reviewed independently (Codex, read-only) the same day. Known, not yet fixed: match-rate counters in the name-matching notebook count merge rows rather than lenders; the DealScan feasibility notebook's live cells depend on a licensed file not in this repository.
