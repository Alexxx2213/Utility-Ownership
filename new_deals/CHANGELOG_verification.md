# Verification log for the new deal lists (2026-11-23)

## `candidate_deals_verified.csv` (C01–C35)
Input was a first, unverified candidate list of 35 rows. The verified file keeps the same 35 rows, updates dates, buyers/sellers and stakes, and adds `source_type` and `verify_note`. Two passes; final result **30 Y, 5 partial, 0 N** (foreign-related 15 rows: 10 Y / 5 partial; domestic 20 rows: 20 Y).

### Corrections
| Row | Before | After |
|---|---|---|
| C05 Atmos Georgia → Liberty | closed 2014, announced 2013-04 | **closed 2013** (about 2013-04-01), announced 2012-08-08 |
| C08 Puget, Macquarie exit | announced 2017–2018 | announced 2018-08-08, completed 2019-04-17, 43.99%. After the deal: CPPIB 31.6 / OMERS 23.9 / BCI 20.9 / AIMCo 13.6 / PGGM 10 |
| C09 UPPCO → Axium | seller BBIP | seller **Basalt Infrastructure Partners** (BBIP was renamed Basalt in 2016 after Balfour Beatty exited; Balfour Beatty's LP interest went to a Wafra-controlled entity) |
| C10 Hawaii Gas → Argo | 2022-07-20 | **2022-07-21** (the old date was a URL number) |
| C11 Oncor 19.75% | investors incl. Cheyne Walk | no evidence for Cheyne Walk, removed; investors are OMERS/Borealis, GIC, Hunt (0.1975%) |
| C12 Duke Indiana / GIC | announced 2021-01-28 | announced 2021-01-19; closings 2021-09-08 (11.05%) and 2022-12-22 (8.85%) |
| C13 Duke Florida / Brookfield | — | signed 2025-08-04; first closing **2026-03-03**, Florida Progress 9.2%, about $2.8B (Duke 8-K); remaining payments through 2028-06-30 |
| C14 Puget 2022 | seller and stake unknown | seller CPP Investments, 31.57% to OTPP + Macquarie; WUTC order 2022-01-27 |
| C15 NorthWestern / BBI | MPSC decision 2007-05-22 | 05-22 only directed staff to draft a denial; MPSC refused to reconsider on 2007-07-24 and BBI terminated the same day |
| C19 Dominion Peoples → SteelRiver | announced 2010-01 | **announced 2008-07-02**; PA PUC approved 2009-11-19; closed 2010-02-01. Hope Gas (WV) was **not** part of this deal |
| C30 NIPSCO 19.9% | closed 2023-12-29 | completion announced 2024-01-02, `year` changed to 2024 |
| C35 TXNM / Blackstone | announced 2025-05-18 | 2025-05-19; outside date 2027-05-31, NMPRC hearing 2027-01-19 to 02-01 |
| C04 Atmos MO/IA/IL → Liberty | — | closed 2012-08-01 (Atmos 10-Q); announced 2011-05; about $128–129M, about 83–84k customers |
| C22 Sempra → Oncor | — | closed 2018-03-09 (Sempra 8-K); 80.25% = 80.03% via merger + 0.22% bought separately; about $9.45B |
| C01 RI gas → National Grid | — | National Grid USA SEC exhibit says New England Gas acquired "as of August 24, 2006"; agreement 2006-02-15 (date comes from a benefit-plan statement) |
| C20 Equitable Gas → SteelRiver | — | agreement 2012-12-19 (KY PSC case 2013-00163) |

Still partial: C05 and C06 (completion dates only from news), C09 (closing date only secondary), C11 (2008 closing date and investor list only secondary), C14 (closing date not found).

### Open coding questions for the group
- **Fund manager vs. LP origin.** C02/C10 Hawaii Gas (MIC, externally managed by a Macquarie subsidiary) and C06/C09 UPPCO (Basalt is a UK partner-owned firm, LPs include Kuwait-linked Wafra) are foreign or not depending on whether we code by manager or by LP. Main coding uses the manager (`control_country`).
- **C20 Equitable Gas:** the filing says investors were "mainly North American and European pension funds and insurers"; Dutch PGGM is named only in a press summary. Coded domestic fund (SteelRiver, US manager); LP note in comments.
- **C23 Peoples → Essential (2020):** at closing CPP Investments also invested $750M in Essential (parent-level minority stake).
- **C33 HECO / NextEra:** Hawaii PUC dismissed the application without prejudice, which differs from the substantive denials in other blocked deals.
- **C30:** "Blackstone Infrastructure LPs include Saudi PIF" is from memory and marked guess.

## `candidate_deals_additions.csv` (C36–C38, Mountaineer Gas)
Found while computing the PJM foreign share; Mountaineer is West Virginia's largest gas utility. Kept in a separate file so the 35-row main file stays unchanged.
- **C36** (group D, 2005, D→D fund): Allegheny sells Mountaineer to IGS and ArcLight. Only source is a 2004-08 signing report (NGI); closing year inferred from the EIA-176 operator ID change in 2004→2005. verified = N.
- **C37** (group A, 2011, D→F): iCON Infrastructure (London) enters. iCON's website lists purchases in Feb 2011, Feb 2012 and Apr 2017 and an exit in 2021. Seller and stakes not disclosed; control from 2011 is an assumption. verified = partial.
- **C38** (group A, 2021, F→D): UGI buys from iCON, closed 2021-09-01 (UGI 8-K exhibit). verified = Y.

## `domestic_mna_candidates.csv` (control group)
Covers domestic strategic M&A since 2000 (G1), blocked/terminated/pending deals (G2), and PE deals found along the way (G4). Listed first from memory, then every row checked against primary sources (mostly SEC 8-K/10-K). Result: 61 of 63 rows Y, 2 partial (D64, D65, whose 8-Ks were read via third-party copies).

Corrections:
- **F01–F03:** the PE buyer/seller for SEMCO (2007) and New Mexico Gas (2009, 2014) was **Lindsay Goldberg (US)**, not Macquarie; moved to the domestic fund group. This also corrected the seller on row 25 (SEMCO) of the original 49 (see `../original_49_deals/changelog.md`).
- **D05 KeySpan/Eastern:** agreement 1999-11, not 1998-11.
- **D06 Energy East:** CMP, CTG and Berkshire all closed 2000-09-01. Connecticut Energy (Southern CT Gas) closed 2000-02 and is not yet in the list.
- **D12 Atmos/MVG:** agreement 2001-09-21. **D14 Piedmont/NCNG:** announced 2002-10-16. **D19 Black Hills/Cheyenne:** agreement 2004-01-13. **D23 WPS/Aquila:** announced 2005-09-21, two closings (MI 2006-03-31, MN 2006-07-01).
- **D44/D46:** Willmut Gas was bought together with EnergySouth on 2016-09-12; D46 marked duplicate and not counted.
- **D63:** after the KCC denial on 2017-04-19 the deal was restructured as a merger of equals and refiled, i.e. D47 Evergy.
- **D64, D65, D66 completed:** Black Hills + NorthWestern combined as Bright Horizon Energy on 2026-11-16; Spire bought Piedmont's Tennessee business on 2026-03-31; National Fuel bought CenterPoint's Ohio gas business on 2026-10-01. All moved to G1.
- **D53 Unitil/Bangor Natural Gas:** confirmed, announced 2024-07-08, closed 2025-01-31.
- Still unconfirmed: original agreement dates for D36, D41, D43, D49, D63.
