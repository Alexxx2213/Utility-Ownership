# Changelog: deal list verification

**Date:** 2026-11-23
**Input:** `Ownership/deals_seed.csv` (49 rows, not modified)
**Output:** `Ownership/verified/deals_verified.csv` (same 49 rows and columns, plus `source_type` and `flag`)

## How rows were verified
- `verified = Y`: a primary document supports the closing (or decision) date. Primary means an SEC filing (8-K, 10-K, 6-K, U-5-S, Rule 24 certificate), a FERC or state PUC order or docket, or the company's own closing release.
- `verified = partial`: the year is supported but the exact closing day isn't, or the only source is secondary.
- For blocked deals, `close_date` holds the termination date and the regulator's decision date is in `notes`.
- FERC eLibrary and ferc.gov can't be reached from this environment. FERC docket numbers come from FERC orders mirrored on ferc.gov PDFs found via search, or from filings that cite them. Many rows still have no FERC EC docket number.
- Results: 43 rows Y, 6 partial, 0 unverified.

## Priority checks
| Deal | Seed said | Finding |
|---|---|---|
| 1 Vermont Gas → Gaz Métro | 1986, from memory | **Confirmed.** Closed 1986-12-30. Gaz Métro bought 100% of Northern New England Energy Corp., the parent of VGS (VT PSB Docket 7213 order, Findings 1 and 12). The seller is not identified. |
| 5 Aquarion → Kelda | 2000, from memory | **Confirmed but partial.** Closed 2000-01-07 according to a company-history reference and Kelda's own timeline. One history source says 1999, which is probably the announcement year. No primary document was found. |
| 12 Aquarion → Macquarie | 2006, from memory | **Year corrected to 2007.** Announced 2006-02-24. NH PUC approved it 2006-10-31 (DW 06-094, Order 24,691). Kelda reports the sale as completed in 2007. The exact day wasn't found because the NY PSC order could not be fetched. |
| 26 New England Gas → Liberty | 2013, seller Southern Union, from memory | **Confirmed.** Seller was Southern Union, an Energy Transfer subsidiary. Liberty took over Laclede's purchase rights. Announced 2013-02-11, closed 2013-12-20. |
| 44 New Mexico Gas → Bernhard | approved, closing not confirmed | **Closed.** Bernhard's release of 2026-08-12 announces the closing. NM PRC final order 2026-07-30 (24-00266-UT). Status changed to `completed`. |

## Other corrections to the seed and brief
- **18 Puget Sound Energy:** the brief says "Canadian and Dutch pensions," but no Dutch investor appears. FERC EC08-40-000 lists Macquarie funds (51.4% combined), CPPIB 28.1%, bcIMC 14.1% and AIMCo 6.3%. Buyer country is now Australia/Canada.
- **22 Duquesne Light, GIC stake:** year changed from 2010 to 2011. The PA PUC approved the transfer from DUET to GIC (Epsom) on 2011-08-11, giving a 28.95% stake (stake changed from 29). Wikipedia's "2010" seems to be the agreement year.
- **17 American Water exit from RWE:** year changed from 2008 to 2009. RWE sold its last shares in November 2009. The April 2008 IPO wasn't separately verified, so this row needs a decision on which date counts as "control changed."
- **40 Avangrid minority buyout:** Iberdrola owned 81.6% before the deal and bought 18.4%. The brief says about 81.5% and 18.5%.
- **16 Energy East:** closed 2008-09-17.
- **41 Dominion gas utilities:** this was three closings: East Ohio Gas 2024-03-06, Questar Gas 2024-05-31 and PSNC 2024-09-30. The row uses the first date. Splitting it into three rows is recommended.
- **45 AES:** final FERC approval came 2026-11-17 and closing is scheduled for 2026-12-02. It is still pending today; recheck after Dec 2.
- **43 ALLETE:** the closing date comes from the 2025-12-15 completion release. The 60/40 GIP/CPP split is not stated in that release, so it is unverified.
- **Blocked deals:** Avista (WUTC denied 2018-12-05, terminated 2019-01-23 with a US$103M fee), PNM (NM PRC rejected 2021-12-08 in 20-00222-UT, terminated 2023-12-31), Kentucky Power (FERC denied in EC22-26-000 in Dec 2022, refiled 2023-02-13, terminated 2023-04-17).
- **Brief link labels:** the FirstEnergy link in the brief is the 2024 sale of 30%, not the 2022 sale of 19.9%. The 19.9% sale closed 2022-05-31 (SEC 8-K exhibit now cited on row 38).

## Count reconciliation (brief says about 40: 28 D→F, 7 F→D, 5 F→F)
The CSV's 43 "completed" rows are not the same set as the brief's 40.
- The brief's 40 equals **Table 1 including New Mexico Gas**. That is 28 D→F (counting ALLETE as partial), 7 F→D and 5 F→F. It **includes the 5 water rows** and **excludes** the four PJM Table 3 rows (FirstEnergy Transmission 2022 and 2024, AEP transmission 2025, Duquesne GIC).
- The seed CSV's 43 completed rows equal Table 1 without New Mexico Gas (39 rows, since it was coded "approved") plus those 4 Table 3 rows.
- After verification there are **44 completed rows**: 27 D→F, 7 F→D, 6 F→F, 3 D→F (minority) and 1 D→F (partial).
- Without the 5 water rows there are 39: 25 D→F, 5 F→D, 5 F→F, 3 minority and 1 partial.
- Without water and without the 4 minority stakes there are 35 changes of control: 26 D→F (including ALLETE), 5 F→D and 4 F→F.

## Flags (column `flag`)
- `WATER`: rows 5, 10, 12, 17 and 34 (Aquarion three times, American Water twice). These are water utilities, outside the electric and gas question. They are kept in the file and flagged; whether to count them is still open.
- `NOT_A_DEAL`: row 49, Pine Tree Power. Maine Question 3 failed on 2023-11-07, with 69.74% No and 30.26% Yes (certified). It was a ballot measure, not a proposed sale blocked by a regulator, so coding it as `blocked` next to Avista, PNM and Kentucky Power is misleading. It is kept and flagged pending a decision.

## Still open
- Exact closing day for Aquarion → Macquarie (2007) and ITC (Oct 2016).
- A primary source for Kelda's purchase of Aquarion (2000).
- FERC EC docket numbers for most electric deals before 2008 (eLibrary not reachable from here).
- EIA utility IDs (`eia_utility_ids`) were not filled in; that is Week 2 work.

## 2026-11-23, decision on the flagged rows
Kevin decided: keep the 5 water rows (5, 10, 12, 17, 34) and Pine Tree Power (49) in the file, but leave them out of all counts and annotate them for discussion at a later meeting.
- New column `count_in_stats`. It is N for those 6 rows and Y for all others.
- New column `meeting_note`. It explains, for each of the 6 rows, why the row is excluded and what the meeting needs to decide.
- With these rows excluded, the counts are as follows. There are 39 completed electric/gas rows: 25 D→F, 5 F→D, 5 F→F, 3 D→F minority stakes and 1 D→F partial (ALLETE). There are 3 blocked deals: Avista, PNM and Kentucky Power. There is 1 pending deal: AES.

## 2026-11-23, correction to row 25 (SEMCO Energy Gas → AltaGas, 2012)
Kevin approved this correction.
- **Seller** changed from "Public company" to "Continental Energy Systems LLC (Lindsay Goldberg, US private equity)".
- Why: Cap Rock Holding Corp (Continental Energy Systems, owned by Lindsay Goldberg) took SEMCO private on 2007-11-09 (SEMCO 8-K: https://www.sec.gov/Archives/edgar/data/0000277158/000027715807000062/pr110907-acqdone.htm). AltaGas bought SEMCO Holding Corp from Continental (Cravath deal note; Lindsay Goldberg release of 2012-02-01).
- **announce_date** filled in: 2012-02-01. Close date 2012-08-30 unchanged.
- Direction stays D→F. For event studies, note that the owner before AltaGas was a domestic PE fund, not public shareholders.
- The 2007 take-private is in `Ownership/candidates_nationwide/domestic_mna_candidates.csv` as row F01.
