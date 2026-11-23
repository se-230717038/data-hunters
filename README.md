# Data Hunters – SE3513 ML Project
Estimating contract prices in EU public procurement and detecting overpriced tenders.

## Data
- Source: OpenML ID 42163 (public_procurement, version 6)
- Raw file: data/raw_public_procurement.parquet (shared via Google Drive)
- MD5: 6a72ecce154c09b1956bb87de94e9443

## Setup
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

## Clean data
- File: data/clean_public_procurement.parquet (shared via Google Drive)
- MD5: 0eab8eb71af6503ede35b2e461a1041d
- 365,203 rows x 22 columns (removed 199,954 rows without award value and 6 rows with zero value)
- Group IDs: data/group_ids.parquet (same row order, 111,479 unique notices), use for group-based train/test split
- Column decisions and reasons: reports/column_decisions.csv
- Derived columns: cpv_div (2-digit CPV division, string), nuts2 (NUTS-2 region)
- Not applied (must be fit on training data only): imputation, encoding, log transform

## Data quality flags (from EDA)
- File: data/quality_flags.parquet (Google Drive), same row order as the clean data
- NOT model features: they are derived from the target (leakage). Use only for analysis and interpretation
- is_repeated_value: 8,683 rows in notices where every lot has exactly the same value (likely copied totals)
- is_suspect_low: 17,052 rows below EUR 100 (likely unit prices); 769 of them below EUR 1
- is_suspect_high: 10 manually reviewed records, see reports/top20_review.csv
- Figures: reports/figures/
