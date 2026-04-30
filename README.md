# dsci410_analyzing_cahoots_call_volumes

# Investigating Crisis Call Volumes: Eugene vs. Springfield (2015–2025)

## Overview
This project analyzes temporal patterns in emergency response call volumes 
across Eugene and Springfield, Oregon, using Computer-Aided Dispatch (CAD) 
and Springfield Police Department (SPD) responding unit data from 2015–2025. 
The central focus is on how demand shifted across agencies — particularly 
toward EPD — following the discontinuation of CAHOOTS alternative crisis 
response services in Eugene.

Currently, this notebook includes data preparation and cleaning steps. 

## Research Questions
- How do temporal call patterns differ between Eugene and Springfield, 
  particularly in terms of demand for alternative crisis response 
  services such as CAHOOTS?
- How do call volumes for different emergency response agencies vary 
  over time between Eugene and Springfield?
- How did call volume patterns in Eugene change after CAHOOTS stopped 
  services, and what does this suggest about shifts in demand across 
  agencies?

## Dependencies
The following Python packages are required to run the notebooks:

- pandas
- numpy
- openpyxl (required for reading the SPD Excel file)

Install all dependencies with:
    pip install pandas numpy openpyxl

## How to Run
1. Clone this repository
2. Place all raw data files in the data/ folder
3. Unzip the "2015-2025_SPD_Responding_Units.xslx" file
4. Run cad_cleaning.ipynb to produce cad_clean_2015_2025.csv
5. Run spd_cleaning.ipynb to produce spd_clean_2015_2025.csv

## Data Sources
- Eugene CAD data: City of Eugene public 911 Computer-Aided Dispatch system
- SPD Responding Units data: Springfield Police Department

## Author
Ilhan Haniff
DSCI 410 — Data Science in Action
University of Oregon
