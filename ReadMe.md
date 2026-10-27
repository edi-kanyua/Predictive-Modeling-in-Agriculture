# Predictive Modeling in Agriculture: an ELT Pipeline with DuckDB
An end-to-end data project that takes messy, realistic farm data through an ELT pipeline (Extract, Load, Transform) in DuckDB 
and finishes with a machine learning model that predicts crop yield per acre.

Everything between the raw files and the model is written in plain SQL, run from Python notebooks, so each step is easy to read, re-run and explain.

## Business Problem

A farmer wants to determine the most suitable crop to grow on a particular field based on soil conditions.

However, due to budget constraints, the farmer can only afford to measure four soil properties:

* Nitrogen (N)
* Phosphorous (P)
* Potassium (K)
* Soil pH

The objective is to determine **which of these soil measures provides the most useful information for predicting the appropriate crop**.

## Project Objective

Build a machine learning classification model to:

1. Predict crop yield per farm per season (a regression problem)

## Results at a glance:
The model learned agronomically sensible relationships: crop type matters most, followed by seasonal rainfall (a sweet spot, 
with too little and too much both hurting), fertilizer (with diminishing returns), certified seed, soil type and irrigation.

## Dataset
Farms are spread across eight counties and grow maize, beans, sorghum and wheat over twelve seasons (long and short rains, 2019 to 2024).
Yield depends on crop, soil, seasonal rainfall, dry spells, temperature, fertilizer, manure, pesticide, certified seed and irrigation, plus random noise.


### Design decisions
ELT rather than ETL: raw data is loaded first and cleaned inside the database, so the original is always preserved and every cleaning rule is visible as SQL.
Everything loaded as text: type conversion is a deliberate, documented step in staging rather than a silent guess at load time.
Fix what's certain in staging, decide the rest in marts: formats, spellings and units are fixed in staging. Judgement calls (outlier thresholds, 
imputation, which rows to use) are made in marts, where there is more context.
No silent row loss: every excluded row has a recorded reason, and row counts are asserted at each stage.
Time-based split and in-pipeline imputation: these prevent leakage and make the test score an honest estimate.
One database file: raw data, cleaned data, features and predictions all live in agri.duckdb and can be queried with SQL.

### Limitations
The data is synthetic. Real data would be noisier (pests, farmer skill, soil nutrients and other unmeasured factors), so expect lower accuracy.
The same farms appear in both training and test seasons. That suits a programme monitoring the same farms; predicting brand-new farms would need a split by farm.
The outlier thresholds (3 times the median input rate, 4 times the median yield) are simple rules of thumb, not agronomic limits.
Missing input records are treated as "nothing applied", which mirrors real data but adds noise.
> 


## Tech stack

* Python
* DuckDB (SQL)
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook / Google Colab

## Expected Outcome


The findings can help the farmer make **data-driven crop decisions while controlling soil-testing costs**.

## Project Structure

agri_elt/
├── data/
│   ├── source/              # synthetic CSVs
│   └── agri.duckdb          # the database
├── notebooks/
│   
│   ├── 01_extract_load.ipynb   # CSVs -> raw schema
│   ├── 02_transform_staging.ipynb  # raw -> staging (cleaning, in SQL)
│   ├── 03_transform_marts.ipynb    # staging -> marts (joins, features, in SQL)
│   └── 04_yield_model.ipynb        # modelling on the marts
├── requirements.txt
└── README.md

## Conclusion

This project demonstrates how machine learning and feature selection can be applied to a practical agricultural decision problem: 
**selecting the right crop using a limited number of affordable soil measurements.**
