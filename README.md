# Investigating Crisis Call Volumes: Eugene vs. Springfield (2015–2025)

**Author:** Ilhan Haniff  
**Course:** DSCI 410L — Data Science for Social Justice, University of Oregon  
**Last Updated:** June 2025

---

## Overview

This project analyzes temporal patterns in emergency response call volumes across Eugene and Springfield, Oregon, using Computer-Aided Dispatch (CAD) and Springfield Police Department (SPD) responding unit data from 2015–2025. The central focus is on how demand shifted across agencies following the discontinuation of CAHOOTS (Crisis Assistance Helping Out On The Streets) alternative crisis response services in Eugene on **April 7, 2025**.

---

**Output files are attached**

## Research Questions

- **Main RQ:** How did call volumes and agency demand patterns in Eugene change after CAHOOTS discontinued services on April 7, 2025, and what does this suggest about whether former CAHOOTS calls were redistributed to other agencies?
- **Sub RQ:** How do temporal call volume patterns differ between Eugene and Springfield across agencies, and what does this reveal about the distinct roles these agencies play in each city's emergency response system?

---

## Repository Structure

```
investigating_crisis_call_volumes/
│
├── data/                              # Raw and cleaned data files
│   ├── EugeneCAD2015noloc.csv         # Raw Eugene CAD data (one file per year)
│   ├── EugeneCAD2016noloc.csv
│   ├── ...
│   ├── EugeneCAD2025noloc.csv
│   ├── 2015-2025_SPD_Responding_Units.xlsx   # Raw SPD data (multi-sheet Excel)
│   ├── cad_clean_2015_2025.csv        # Cleaned Eugene CAD output (generated)
│   └── spd_clean_2015_2025.csv        # Cleaned SPD output (generated)
│
├── figures/                           # All output visualizations (generated)
│
├── cad_cleaning.ipynb                 # Step 1: Clean Eugene CAD data
├── spd_cleaning.ipynb                 # Step 2: Clean SPD data
├── analysis.ipynb                     # Step 3: EDA, temporal analysis, pre/post analysis
├── statistical_tests.ipynb            # Step 4: Formal hypothesis testing
│
└── README.md
```

---

## Dependencies

Python 3.8+ is required. Install all dependencies with:

```bash
pip install pandas numpy matplotlib seaborn scipy openpyxl
```

| Package     | Purpose                                      |
|-------------|----------------------------------------------|
| `pandas`    | Data loading, cleaning, and aggregation       |
| `numpy`     | Numerical operations                          |
| `matplotlib`| Base plotting                                 |
| `seaborn`   | Statistical visualizations (KDE plots, etc.)  |
| `scipy`     | Statistical tests (t-test, chi-square)        |
| `openpyxl`  | Reading the SPD multi-sheet Excel file        |

---

## How to Run

Run the notebooks **in order**. Each notebook depends on the output of the previous one.

### Step 1 — Clean Eugene CAD Data
Open and run **`cad_cleaning.ipynb`**

- **Input:** `data/EugeneCAD{year}noloc.csv` for years 2015–2025
- **Output:** `data/cad_clean_2015_2025.csv`
- Combines all 11 yearly CSV files, standardizes columns, extracts temporal features, and classifies each call as `EPD`, `CAHOOTS`, or `UNKNOWN` using the `classify_unit()` function.

### Step 2 — Clean SPD Data
Open and run **`spd_cleaning.ipynb`**

- **Input:** `data/2015-2025_SPD_Responding_Units.xlsx`
- **Output:** `data/spd_clean_2015_2025.csv`
- Reads each yearly sheet and the Designator Notes sheet, standardizes columns, extracts temporal features, and classifies units using the `classify_spd_unit()` function.

### Step 3 — Run Analysis
Open and run **`analysis.ipynb`**

- **Input:** `data/cad_clean_2015_2025.csv`, `data/spd_clean_2015_2025.csv`
- **Output:** All figures saved to `figures/`
- Covers: EDA summary statistics, yearly and hourly temporal trends, pre/post discontinuation analysis, EPD and UNKNOWN deep dives.

### Step 4 — Run Statistical Tests
Open and run **`statistical_tests.ipynb`**

- **Input:** `data/cad_clean_2015_2025.csv`, `data/spd_clean_2015_2025.csv`
- **Output:** Printed test results + figures saved to `figures/`
- Covers: Welch's t-test (EPD daily volume), chi-square test (agency share), t-test (Springfield CAHOOTS as control). All comparisons use the matched seasonal window: **April 7 – December 31, 2024 vs. April 7 – December 31, 2025**.

---

## Key Parameters

| Parameter | Value | Location |
|-----------|-------|----------|
| CAHOOTS discontinuation date | `2025-04-07` | `analysis.ipynb`, `statistical_tests.ipynb` |
| Pre-window | Apr 7 – Dec 31, 2024 | `statistical_tests.ipynb` |
| Post-window | Apr 7 – Dec 31, 2025 | `statistical_tests.ipynb` |
| CAHOOTS unit pattern (pre-2022) | `'J'` in `primeunit` | `cad_cleaning.ipynb → classify_unit()` |
| CAHOOTS agency label (2022+) | `agency == 'CAHE'` | `cad_cleaning.ipynb → classify_unit()` |

---

## Output Figures

All figures are saved to the `figures/` folder by `analysis.ipynb` and `statistical_tests.ipynb`.

### Temporal Analysis (`analysis.ipynb`)
| File | Description |
|------|-------------|
| `eugene_yearly_call_volume.png` | Yearly call volume by agency in Eugene, 2015–2025 |
| `spd_yearly_call_volume.png` | Yearly call volume by unit type in Springfield, 2015–2025 |
| `hourly_call_volume_comparison.png` | Raw hourly call volume: Eugene vs. Springfield |
| `hourly_call_distribution_kde.png` | KDE of hourly call distributions: Eugene vs. Springfield |
| `timeline_epd_cahoots.png` | Monthly EPD and CAHOOTS call volume with discontinuation marker |
| `agency_share_pre_post.png` | Agency share of total calls: before vs. after discontinuation (full period) |
| `epd_avg_daily_pre_post.png` | Average daily EPD call volume: full pre vs. post periods |
| `epd_avg_daily_2024_vs_2025.png` | Average daily EPD call volume: matched 2024 vs. 2025 windows |
| `epd_hourly_kde_2024_vs_2025.png` | EPD hourly KDE: matched 2024 vs. 2025 windows |
| `cahoots_eugene_vs_spd_2024_vs_2025.png` | Average daily CAHOOTS: Eugene vs. Springfield, 2024 vs. 2025 |
| `unknown_avg_daily_2024_vs_2025.png` | Average daily UNKNOWN call volume: 2024 vs. 2025 |
| `unknown_share_2024_vs_2025.png` | UNKNOWN share of total calls: 2024 vs. 2025 |
| `unknown_hourly_kde_2024_vs_2025.png` | UNKNOWN hourly KDE: 2024 vs. 2025 |
| `spd_cahoots_hourly_kde_2024_vs_2025.png` | Springfield CAHOOTS hourly KDE: 2024 vs. 2025 |

### Statistical Tests (`statistical_tests.ipynb`)
| File | Description |
|------|-------------|
| `test1_epd_daily_distribution.png` | KDE of daily EPD call counts — T-test visualization (p = 0.39) |
| `test2_agency_share.png` | Agency share by matched window — Chi-square visualization (p < 0.001) |
| `test3_spd_cahoots_daily_distribution.png` | KDE of daily Springfield CAHOOTS — Control T-test visualization |

---

## Data Sources

- **Eugene CAD Data:** City of Eugene Public Records — Public 911 Computer-Aided Dispatch system (2015–2025)
- **SPD Responding Units Data:** Springfield Police Department Public Records (2015–2025)

> **Note:** Raw data files are included in this repository for reproducibility. They are publicly available records.

---

## Notes on Classification Logic

**Eugene CAD (`classify_unit()`):** CAHOOTS is explicitly labeled via `agency == 'CAHE'` from 2022 onward. For 2015–2021, CAHOOTS units are identified by the presence of `'J'` in the `primeunit` field (e.g., `_3J79`), consistent with the known CAHOOTS unit naming convention. Units matching EPD dispatch patterns are classified as `EPD`. All others are `UNKNOWN`.

**SPD (`classify_spd_unit()`):** Unit type is derived from the `prime_unit` identifier cross-referenced against the Designator Notes sheet in the SPD Excel file. Categories include: `CAHOOTS`, `PATROL`, `DETECTIVE`, `CSO_AC`, `COMMAND`, `NOT_SPD`, and `OTHER`.
