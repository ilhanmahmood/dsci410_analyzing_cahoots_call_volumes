# dsci410_analyzing_cahoots_call_volumes

# Investigating Crisis Call Volumes: Eugene vs. Springfield (2015–2025)

## Overview
This project analyzes temporal patterns in emergency response call volumes 
across Eugene and Springfield, Oregon, using Computer-Aided Dispatch (CAD) 
and Springfield Police Department (SPD) responding unit data from 2015–2025. 
The central focus is on how demand shifted across agencies — particularly 
toward EPD — following the discontinuation of CAHOOTS alternative crisis 
response services in Eugene.

## Research Questions
- How do temporal call patterns differ between Eugene and Springfield, 
  particularly in terms of demand for alternative crisis response 
  services such as CAHOOTS?
- How do call volumes for different emergency response agencies (EPD, 
  CAHOOTS, SPD Patrol) vary over time and by hour of day between 
  Eugene and Springfield?
- How did call volumes change in Eugene after CAHOOTS discontinued 
  services on April 7, 2025, and does this suggest a shift in demand 
  toward EPD?

## Dependencies
The following Python packages are required to run the notebooks:

- pandas
- numpy
- matplotlib
- openpyxl (required for reading the SPD Excel file)

Install all dependencies with:
    pip install pandas numpy openpyxl matplotlib

## How to Run
1. Clone this repository
2. Makes sure all raw data files in the data/ folder
3. Unzip the "2015-2025_SPD_Responding_Units.xslx" file
4. Run cad_cleaning.ipynb to produce cad_clean_2015_2025.csv
5. Run spd_cleaning.ipynb to produce spd_clean_2015_2025.csv
6. Run analysis.ipnyb to produce summary tables and visualizations saved to the `figures/` folder

## Data Sources
- Eugene CAD data: City of Eugene public 911 Computer-Aided Dispatch system
- SPD Responding Units data: Springfield Police Department

## Output Figures
All visualizations are saved to the `figures/` folder:
- `eugene_yearly_call_volume.png` — Yearly call volume trends by agency (Eugene)
- `spd_yearly_call_volume.png` — Yearly call volume trends by unit type (Springfield)
- `hourly_call_volume_comparison.png` — Hourly patterns: Eugene vs. Springfield
- `agency_share_pre_post.png` — Agency share before vs. after CAHOOTS discontinuation
- `timeline_epd_cahoots.png` — Annotated monthly timeline with discontinuation marker

## Author
Ilhan Haniff
DSCI 410 — Data Science in Action
University of Oregon
