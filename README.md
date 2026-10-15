# Iowa Liquor Sales: Choosing a New Store Location

A regression analysis of Iowa's public liquor sales data to recommend where a liquor store owner should open a new location. This was Project 3 in the General Assembly Data Science Immersive.

More of my work: https://kylesantana.com

## Problem

A liquor store owner in Iowa wants to expand and asked for an analysis of the market data to find promising locations for a new storefront, along with the details of the best model I could fit.

## Dataset

Iowa liquor sales data published by the State of Iowa (Iowa Alcoholic Beverages Division, available on the Iowa Data portal at https://data.iowa.gov). Each row is a sale with store location (city, zip code, county), bottle retail price, bottles sold and sale amount in dollars.

The notebook reads a 10% sample, `Iowa_Liquor_sales_sample_10pct.csv`. The data file is not included in this repo because of its size. To re-run the notebook, download the data and save it under that name next to the notebook.

## Approach

1. Cleaned the data: dropped rows with missing values (about 10,000), checked for duplicates, standardized column names and converted price columns from text to numbers.
2. Explored sale dollars, bottles sold and bottle price with histograms and a correlation heatmap. Bottles sold and sale dollars are correlated.
3. Built one-hot (dummy) variables for county, city and zip code, dropping the most common category in each (Polk County, Des Moines and 50010).
4. Fit linear regression models of sale dollars on bottle retail price, bottles sold and location (one model each for county, city and zip code) with statsmodels and scikit-learn.
5. Evaluated the models with a 70/30 train/test split and 5-fold cross-validation, then plotted predicted vs. actual sales.

## Key findings

From the conclusion in the notebook:

- After the first round of models I dropped city and continued with county and zip code.
- The top five counties by sales-per-bottle relative to their size were Dallas, Carroll, Sioux, Iowa and Howard.
- Among the top zip codes, one was dropped because a single winery accounted for most of its sales. That left 50266, 50320 and 52154 as the top three.
- My first recommendation for a new store was zip code 50266.
- Narrowing the location further, down to a few blocks, would need demographic and population data that wasn't part of this dataset.

## Tools

Python, pandas, NumPy, matplotlib, seaborn, statsmodels, scikit-learn, Jupyter.

## How to view or run

- View: open `Iowa_Liquor.ipynb` on GitHub. The saved outputs and plots are included.
- Run:

```bash
pip install -r requirements.txt
jupyter notebook Iowa_Liquor.ipynb
```

The notebook was written for Python 3.6 and older pandas/scikit-learn versions, so some calls (for example `np.object`) may need small updates on current library versions.

## Files

| File | Description |
| --- | --- |
| `Iowa_Liquor.ipynb` | Full analysis: cleaning, exploration, regression models, cross-validation and conclusions |
| `requirements.txt` | Python libraries imported in the notebook |
