# Customer Lifetime Value (CLV) Prediction

Probabilistic modeling of customer purchasing behavior to estimate future revenue contribution per customer, using the BG/NBD and Gamma-Gamma frameworks on transactional retail data.

## Overview

This project builds an end-to-end pipeline that transforms raw invoice-level transactions into forward-looking Customer Lifetime Value estimates. Rather than relying on naive historical averages, the pipeline explicitly models each customer's probability of remaining active and their expected future purchase frequency and monetary value.

## Key Features

- Data cleaning and outlier handling on raw transactional records
- Exploratory data analysis of revenue trends, order distribution, and geographic breakdown
- RFM (Recency, Frequency, Monetary) feature engineering with rule-based customer segmentation
- Monthly cohort retention analysis
- BG/NBD model for predicting purchase frequency and churn probability
- Gamma-Gamma model for estimating expected average transaction value
- 6-month and 12-month discounted CLV projections
- CLV-based customer segmentation (Low, Medium, High, Premium)
- Model validation via calibration/holdout split
- Exportable scored customer base for downstream marketing and CRM use

## Project Structure

```
.
├── data/
│   └── transactions.xlsx
├── Customer_Lifetime_Value.ipynb
├── customer_clv_scored.csv
└── README.md
```

## Requirements

```
pandas
numpy
matplotlib
seaborn
squarify
lifetimes
openpyxl
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Usage

1. Place your transactional data file under `data/transactions.xlsx`, containing invoice-level records with columns for invoice number, product code, quantity, unit price, invoice date, customer ID, and country.
2. Open `Customer_Lifetime_Value.ipynb` in Jupyter.
3. Run all cells sequentially. The notebook will output cleaned data summaries, visualizations, fitted model diagnostics, and a final scored customer file.

## Methodology

The pipeline follows a two-stage probabilistic modeling approach:

1. **BG/NBD (Beta Geometric / Negative Binomial Distribution):** models the number of transactions a customer will make in a future period and the probability that the customer is still active, based on their historical frequency and recency.
2. **Gamma-Gamma:** models the expected average monetary value per transaction, conditioned on purchase frequency, assuming no strong correlation between purchase frequency and spend per transaction.

Combining both models yields a discounted CLV estimate over a chosen time horizon, which is then used to segment customers by projected value.

## Output

The notebook exports `customer_clv_scored.csv`, containing per-customer:

- RFM metrics and rule-based segment
- BG/NBD frequency, recency, and customer age (T)
- Predicted purchase count over the forecast horizon
- Probability of being an active customer
- Predicted average transaction value
- 6-month and 12-month projected CLV
- CLV-based segment label

## License

This project is released under the MIT License.
