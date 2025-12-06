## Expected Loss (EL) Modeling Project

This repository contains analysis and modeling for Expected Loss (EL) calculation using the Lending Club dataset. The project follows the Basel regulatory framework, decomposing Expected Loss into its three components: Probability of Default (PD), Loss Given Default (LGD), and Exposure at Default (EAD).

### Project Structure

- **data-preparation-notebook.ipynb** - Data cleaning and preprocessing
- **PD-modeling-notebook.ipynb** - Probability of Default modeling and analysis
- **LGD-modeling-notebook.ipynb** - Loss Given Default (Recovery Rate) modeling
- **EAD-modeling-notebook.ipynb** - Exposure At Default (Credit Conversion Factor) modeling

### Setup Instructions

Download the [Lending Club dataset](https://www.kaggle.com/datasets/janiobachmann/lending-club-first-dataset/data)

Put the raw dataset file in the raw-data/ folder

Run the notebooks in sequence:

First: Run **data-preparation-notebook.ipynb**
- Cleans and preprocesses raw data
- Performs feature engineering
- Saves processed data to processed-data/ folder

Second: Run the modeling notebooks:
- **PD_modeling.ipynb**
- **LGD_modeling.ipynb**
- **EAD_modeling.ipynb**

### Modeling Approach

#### 1. Probability of Default (PD)
Models the likelihood that a borrower will default on their loan obligations.

#### 2. Loss Given Default (LGD)
- Primary target: Recovery Rate (RR) - the percentage of exposure recovered after default
- LGD calculation: LGD = 1 - Recovery Rate
- Models the proportion of exposure that is lost when default occurs

#### 3. Exposure at Default (EAD)
- Primary target: Credit Conversion Factor (CCF) - the portion of the undrawn commitment that is likely to be drawn at default
- EAD calculation: Based on CCF applied to the original loan amount
- Models the expected exposure at the time of default

### Expected Loss Calculation

The final Expected Loss is calculated as:
` ` `
EL = PD × LGD × EAD
` ` `

Where:
- PD: Probability of Default (0-1 scale)
- LGD: Loss Given Default (0-1 scale, calculated as 1 - Recovery Rate)
- EAD: Exposure at Default (monetary amount, calculated using CCF)

### Current Development

- FastAPI Web Service - Currently building a FastAPI application that integrates all three models
- API Endpoint - Creating an endpoint that accepts loan application data and returns:
- - Individual PD, LGD, EAD estimates
- - Final Expected Loss calculation
- - Risk grade classification
- Model Integration - Combining the three trained models into a unified prediction pipeline

### Notes

The data_preparation.ipynb notebook creates a consistent, cleaned dataset that all three modeling notebooks use as their input. Each modeling notebook then applies component-specific preprocessing and target variable definitions for PD, LGD, and EAD respectively.