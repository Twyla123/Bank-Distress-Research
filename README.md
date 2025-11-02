# Bank Distress Analysis Project

## Overview
This project analyzes bank distress by integrating and classifying complex financial datasets from various banking institutions. The goal is to create a comprehensive understanding of bank structures and assess the financial health and stability of publicly traded banks. The project focuses on data matching, classification, and merging from multiple layers of financial reporting.

---

## Features

### Key Contributions:
- **Bank Data Matching:**
  - Merged data from the Consolidated Reports of Condition and Income (*Call Reports*) with FR Y-9C reports.
  - Established detailed links between bank holding companies and their subsidiaries, providing a clear view of organizational structures.

- **Lines of Credit (LOC) Data Matching and Classification:**
  - Matched LOC data with Call Reports and FR Y-9C reports, assigning each match to one of three accuracy levels.
  - Cross-referenced unmatched entries with credit union data to ensure dataset completeness.
  - Merged LOC data with the Federal Reserve Bank of New York’s Banking Research Datasets to identify publicly traded banks.

- **HMDA (Home Mortgage Disclosure Act) Integration:**
  - Processed over **100 million mortgage application records per year** using chunked reading to efficiently handle large datasets.
  - Standardized variable names and formats across schema changes (pre- and post-2018), harmonizing the **Transmittal Sheet (TS)** and **Loan Application Register (LAR)**.
  - Merged TS and LAR datasets by lender identifiers (LEI and Respondent ID) and linked them to census tract and county codes.
  - Produced a consistent **2011–2023** mortgage-lending panel aligned with Call Report institutions, enabling analysis of origination trends around major policy and market shifts.

- **DealScan (Syndicated Loan Market Panel):**
  - Cleaned and organized **Refinitiv LPC DealScan** data to track bank–borrower lending relationships over time.
  - Defined loan start and maturity windows using *Tranche Active Dates* and handled multi-tranche deals to avoid double counting.
  - Expanded event-level records into quarterly panels aggregated at the **bank × borrower × quarter** level.
  - Captured lending dynamics (new loans, amendments, renewals, maturities) and cross-validated with Call Reports to check consistency between market and regulatory sources.

---

## Dataset Information

The project utilized the following datasets:
1. **Call Reports**: Consolidated Reports of Condition and Income for bank holding companies.
2. **FR Y-9C Reports**: Detailed financial data from bank holding companies.
3. **Lines of Credit Data**: Information on bank-issued lines of credit.
4. **HMDA (Home Mortgage Disclosure Act)**: Mortgage applications and originations from 2011–2023.
5. **DealScan**: Syndicated-loan transactions and tranche-level lending data.
6. **Credit Union Data**: Cross-referenced for unmatched entries.
7. **Banking Research Datasets**: Publicly available data from the Federal Reserve Bank of New York, used to identify publicly traded banks.

### Data Sources:
- [Federal Financial Institutions Examination Council (FFIEC)](https://www.ffiec.gov/)
- [Federal Reserve Bank of New York](https://www.newyorkfed.org/)
- [Refinitiv LPC DealScan](https://www.refinitiv.com/)
- [Consumer Financial Protection Bureau (CFPB) HMDA](https://ffiec.cfpb.gov/)
