# New deals (beyond the original 49)

Everything here was found after the starter brief, when the sample was widened from New England / New York / PJM to all US electric and gas utilities. **The original 49 deals are not in this folder** (see `../original_49_deals/`), except in the combined table, which puts all lists side by side.

| File | What it is | Status |
|---|---|---|
| `candidate_deals_verified.csv` | **Main file.** 35 new deals (`C01`–`C35`): foreign control changes, foreign minority stakes, a blocked foreign deal, and domestic PE/infrastructure-fund deals, plus domestic deals that were blocked or are pending. | 30 rows Y, 5 partial |
| `candidate_deals_additions.csv` | 3 rows added later (`C36`–`C38`): Mountaineer Gas (WV), missed by both lists. 2005 sale to IGS/ArcLight, 2011 entry of iCON (London), 2021 sale to UGI. Same columns as the main file. | C36 N, C37 partial, C38 Y |
| `domestic_mna_candidates.csv` | Control group: domestic **strategic** utility M&A since 2000 (`D01`–`D66`, `F01`–`F03`). | 61 rows Y, 2 partial; D46 is a duplicate of D44 and not counted |
| `all_deals_combined.xlsx` (+ `.csv`) | All four lists in one 150-row table (the 49 + the 35 + the 3 + the 63). `in_sample` says which rows to use. | — |
| `CHANGELOG_verification.md` | Corrections made while verifying these lists, and open coding questions. | — |

## Groups
`candidate_deals_verified.csv`, column `group`:
- A: foreign change of control (10 rows)
- B: foreign minority stake (4)
- C: foreign deal blocked (1, NorthWestern / Babcock & Brown)
- D: domestic fund change of control, including fund exits to strategic buyers (14)
- E: domestic fund minority stake (1)
- F: domestic deal blocked or pending (5)

`domestic_mna_candidates.csv`: G1 completed strategic M&A; G2 blocked, terminated or pending; G4_domestic_fund for PE deals found along the way (SEMCO 2007, New Mexico Gas 2009/2014, all Lindsay Goldberg).

## Coding of ownership country
- `control_country` (main coding): headquarters country of whoever makes the decisions, i.e. the strategic buyer's parent, or the fund's GP/manager.
- `manager_registered_country`: where the manager or acquisition vehicle is registered, for robustness checks.
- `known_foreign_lp`: known foreign investors in the fund (`unknown` if not found, `n/a` for strategic or listed buyers).
- Cells containing "guess" are inferences without a source.

## Verification standard (same as for the 49)
`Y`: a primary source (SEC filing, regulator order or release, or a party's own announcement) supports the closing date or regulator decision date. `partial`: the year is supported but the exact date or the stake split relies on a secondary source. `N`: not yet checked.

## Combined table (`all_deals_combined.xlsx` / `.csv`)
One row per deal, 150 rows. The first columns tell you how to use each row:

| Column | Meaning |
|---|---|
| `source_list` | Which list the row comes from: `Original 49`, `New: nationwide candidates (C01-C35)`, `New: Mountaineer Gas additions (C36-C38)`, `New: domestic M&A control group (D/F rows)`. |
| `original_id` | The row's ID in its source file. |
| `in_sample` | `yes` (131 rows) = a completed or pending electric/gas ownership change to use in the analysis. `no` (19 rows) = kept for reference only. |
| `exclusion_reason` | Why a row is `no`: deal blocked or terminated (12), water utility (5), not a transaction (Pine Tree Power ballot measure, 1), duplicate of D44 (1). Blocked deals are kept because they may be useful as a comparison group. |
| `coding_uncertain` | `yes` (8 rows) = the ownership coding is a judgment call; `uncertainty_note` says why. Pending or partly closed deals (45 AES, C35 TXNM, C13 Duke Florida) are in this group and stay in the sample. |
| `counted_in_original_49_stats` | Original 49 only: whether the row was counted in the summary statistics of `original_49_deals/` (which count blocked deals separately). |

To get the analysis sample, filter `in_sample = yes`. The Excel file has the same table on the `All_deals` sheet plus: `Columns` (column definitions), `Summary` (row counts), `Size_cutoffs`, `Uncertain_coding` and `Duplicate_check`. `related_rows` links different transactions involving the same utility; `Duplicate_check` explains each pair.

The table also has firm size: retail customers in the year before closing (`cust_electric_pre`, `cust_gas_pre`, `customers_pre_total`, from EIA-861 and EIA-176), a size class and below-cutoff flags (counts in the `Size_cutoffs` sheet). Caveats are in `size_note`: Texas wires companies (Oncor, TNMP Texas) are missing from EIA-861, pre-2001 electric deals use 2001 counts, and transmission-only and water rows have no count.
