# Utility Ownership

Research on US electric and gas utilities that changed hands between domestic and foreign owners, and how those changes affect rates, investment, reliability and regulation.

## Contents

| Folder | What it is |
|---|---|
| `original_49_deals/` | The 49 deals from the starter brief, checked against primary sources. |
| `new_deals/` | Deals found after the brief (nationwide sample, Mountaineer Gas, domestic M&A control group) and a combined table of all deals. Not yet discussed by the group. |

## `original_49_deals/`

| File | What it is |
|---|---|
| `deals_seed.csv` | The original 49-deal list that came with the brief. Kept unchanged for reference. |
| `deals_verified.csv` | **Verified version of the same 49 rows.** Same columns as the seed, plus `source_type`, `flag`, `count_in_stats` and `meeting_note`. |
| `changelog.md` | What was checked, every correction to the seed, and how the counts reconcile with the brief. |

### How to read `deals_verified.csv`
- `verified`: `Y` (43 rows) means a primary document (SEC filing, FERC or state PUC order, or the company's closing release) supports the closing or decision date. `partial` (6 rows) means the year is supported but not the exact day, or only a secondary source was found.
- `count_in_stats = N` marks 6 rows that stay in the file but are left out of all counts for now: the 5 water utility rows (Aquarion and American Water) and Pine Tree Power (a ballot measure, not a deal). `meeting_note` says what the group needs to decide about each.
- Counting only `count_in_stats = Y`: 39 completed electric/gas deals (25 D→F, 5 F→D, 5 F→F, 3 D→F minority stakes, 1 D→F partial), 3 blocked (Avista, PNM, Kentucky Power) and 1 pending (AES).
- For blocked deals, `close_date` is the termination date; the regulator's decision date is in `notes`.
- Main corrections to the seed are listed in `changelog.md` (e.g. Aquarion → Macquarie closed 2007 not 2006, Duquesne/GIC 2011 not 2010, Puget's buyers were Australian and Canadian with no Dutch investor, New Mexico Gas → Bernhard has closed, SEMCO's seller was a US PE fund).
