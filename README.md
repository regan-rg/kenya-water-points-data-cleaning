# Kenya Water Points: Data Cleaning Project

A data cleaning project on real water point data for Kenya, built around a reusable 15-item cleaning checklist. The checklist was written from problems met on an earlier project, then run end to end on the Water Point Data Exchange (KEN) dataset (21,953 records, 54 columns). Every finding is logged, and every change is a fix, a flag, or a documented decision to leave the data alone.

## Dataset
- **Source:** Water Point Data Exchange (WPdx), shared on the Humanitarian Data Exchange: https://data.humdata.org/dataset/wpdx_ken
- **Files used:** wpdx_enhanced.csv (Kenya) for the cleaning; adm_analysis.csv (area summary) kept for reference
- **Size:** 21,953 records and 54 columns, plus a row of HXL tags that was removed from the working copy
- **Licence:** Creative Commons Attribution Share-Alike (CC BY-SA), as listed on the dataset page

## Data and licence
The data is the Water Point Data Exchange (KEN) dataset, published on the Humanitarian Data Exchange (https://data.humdata.org/dataset/wpdx_ken) under the Creative Commons Attribution Share-Alike (CC BY-SA) licence. Credit: Water Point Data Exchange (WPdx). The dataset page notes that it represents the best available information shared with the WPdx platform.

The original files in data/original are unchanged. The workbook in data/working is a modified version of that data. The changes are listed in its Findings Log and Run summary sheets: a row of tags removed, 22 spacing and 23 capitalisation fixes, 4 placeholder cells and 205 form-text cells relabelled, 13 empty columns deleted, and an install-year flag column added.In line with the share-alike term, that workbook, and the analysis workbook in the analysis folder (which contains a copy of the cleaned data), are also shared under CC BY-SA.The cleaning checklist and the write-up are my own work.

## The checklist
The checklist has 15 items in five groups: duplicates, blanks, consistency, data types and validation, plus process rules and a first look at the data. A running order sheet puts them in sequence: Prepare, Detect, Fix, Verify, Protect. It was improved five times while running it on this dataset, for example by adding wildcard searches for hidden placeholders, checks for numeric stand-ins like 0, and a check for capital-letter variants that filters cannot see.

## Tools Used
Microsoft Excel (COUNTBLANK, COUNTIF with wildcards, SUMPRODUCT, ISNUMBER, EXACT, TRIM, Find & Replace, Remove Duplicates, filters), Git and GitHub.

## Process
1. **Prepare:** kept the original CSV untouched, worked on a copy, and took a first look at the size, columns and definitions.
2. **Detect:** found missing data and placeholder text across all 54 columns using one row of formulas, confirmed with a second method.
3. **Detect:** checked data types, spacing, capitalisation, and values against expected lists.
4. **Detect:** checked for duplicate IDs and duplicate rows, with a planted duplicate to prove each check works.
5. **Detect:** checked for impossible values, including comparisons between related columns.
6. **Fix:** corrected what was safe to correct, flagged what was uncertain, and left alone what could not be known.
7. **Verify:** re-ran the checks to confirm nothing broke and the counts still reconcile.
8. **Document:** logged every finding and decision, and summarised the run.

## Key Findings
- 13 of the 54 columns hold no data at all, and 4 more are 84% to 92% blank.
- 277 rows have "Unknown" in status_id, and 1,028 rows use 0 as an activity ID.
- 11,571 of the 13,578 Non-Functional points (about 85%) also report water available in status_id. The two columns measure different things, so this was flagged and not changed.
- 8 of Kenya's 47 counties have no records, so results describe 39 counties.
- 9 rows have install years that cannot be right (installed after the report date, 2028, or 1900).
- No duplicate IDs and no duplicate rows.

## What was fixed, flagged and left alone
- **Fixed:** 22 cells with doubled spaces, 23 cells with capitalisation variants, 4 "unknown 7" cells, 205 leftover form-text cells (relabelled "Other (not specified)"), and 13 empty columns removed.
- **Flagged:** 9 rows with suspicious install years, using a new install_year_flag column. The years were not changed.
- **Left unchanged, with reasons logged:** the mostly blank columns, the Unknown values in status_id, mixed-type IDs, and timestamps stored as text.
- **Open questions for the data owner:** whether "World Vision" and "World Vision International Kenya" are the same organisation, and why so many Non-Functional points report water available.


## Analysis: where is repair needed most?
**Question:** Which counties have the most non-functional water points, in number and as a share of the points recorded there? "Non-functional" means status_clean = "Non-Functional" (no longer working, whatever the season). Counties with fewer than 30 points are listed but not ranked by share.

**What I found first:** 12 of the 15 data sources mark every one of their points Non-Functional. Those 12 sources hold 12,179 points (55% of all rows) and about 90% of all non-functional points. The largest, Evidence Action, has 10,850 points, all marked Non-Functional, yet 10,502 of them record that water was available (status_id = Yes). That pattern looks more like a default value than a measurement, and it accounts for most of the 11,571 status disagreements found during cleaning. I could not prove the values wrong, so I raised it as a question for the data owner.

**What I did about it:** I reported each county's share twice: using all sources (61.85% overall) and using only the 3 sources whose statuses vary (14.3% overall). I ranked counties on the second.

**Result:** Only 14 of 39 counties have 30 or more points from the varied sources. Their shares run from 4.2% (Kajiado) to 20.5% (Makueni). The top five (Makueni, Siaya, Kisumu, Busia, Migori) sit between about 16% and 20%, close enough that their order is not firmly established. Baringo, Trans Nzoia, Homa Bay and Samburu look worst when all sources are used, but have only 0 to 3 points from the varied sources, so their condition is unknown, not proven bad.

**Limits:** The data is what contributors shared, not a census of water points. 8 of Kenya's 47 counties have no records, only 14 counties can be ranked, and the varied sources may survey different kinds of points from the others.

![County chart](images/q1-county-chart.png)
![Sources table](images/q1-sources.png)
## Screenshots

![Run summary](images/run-summary.png)
![Findings log](images/findings-log.png)
![Checklist run](images/checklist-run.png)
![Cleaning checklist](images/cleaning-checklist.png)
*The screenshot shows the first items. The full 16-item checklist is in the checklist folder.*
## Files
- **checklist:** the reusable cleaning checklist (data-cleaning-checklist.xlsx)
- **data/original:** the downloaded CSV files, unchanged
- **data/working:** the cleaned workbook with the findings log, run summary and checklist run (wpdx-kenya-cleaned.xlsx)
- **analysis:** the analysis workbook (wpdx-kenya-analysis.xlsx) with the source and county tables, the ranking, the chart and the analysis log
- **images:** screenshots used in this README

## Author
Reagan, Civil Engineering student at JKUAT, building a data analytics portfolio