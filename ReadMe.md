THIS IS AN ONGOING PROJECT!

# Predictive Modeling for Agriculture: Crop Recommendation

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

## Dataset



### Features

                        |

### Target



## Methodology

The analysis will follow a machine learning workflow:



## Key Question

> 


## Tools & Technologies

* Python
* DuckDB
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

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

This project demonstrates how machine learning and feature selection can be applied to a practical agricultural decision problem: **selecting the right crop using a limited number of affordable soil measurements.**
