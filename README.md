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

### Skills Developed:
- Advanced data integration and classification techniques.
- Handling and analyzing large-scale financial datasets with multiple reporting layers.
- Gaining insights into the banking sector, with a focus on the financial health and structures of publicly traded banks.

---

## Dataset Information

The project utilized the following datasets:
1. **Call Reports**: Consolidated Reports of Condition and Income for bank holding companies.
2. **FR Y-9C Reports**: Detailed financial data from bank holding companies.
3. **Lines of Credit Data**: Information on bank-issued lines of credit.
4. **Credit Union Data**: Cross-referenced for unmatched entries.
5. **Banking Research Datasets**: Publicly available data from the Federal Reserve Bank of New York, used to identify publicly traded banks.

### Data Sources:
- [Federal Financial Institutions Examination Council (FFIEC)](https://www.ffiec.gov/)
- [Federal Reserve Bank of New York](https://www.newyorkfed.org/)

---

## Technologies Used

- **Languages:**
  - Python
  - R
- **Libraries:**
  - Pandas
  - NumPy
- **Tools:**
  - Jupyter Notebook
  - GitHub for version control
