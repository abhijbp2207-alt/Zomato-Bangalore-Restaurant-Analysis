# Zomato Bangalore Restaurant Analysis

An end-to-end data analysis of Bangalore restaurants to find what drives ratings and where the market has room for a better restaurant.

## Problem
What drives restaurant ratings in Bangalore, and which areas offer room for a better restaurant?

## Dataset
- **Source:** Zomato Bangalore Restaurants (Kaggle)
- **Raw size:** about 51K records, 17 columns
- **After cleaning:** 41,392 rows, 15 columns
- **Key columns:** rating, cost for two, votes, cuisines, location, restaurant type, online order, table booking

## Approach
1. **Data cleaning:** converted ratings from text to numeric, cleaned cost values, handled nulls, standardized text and removed duplicates
2. **Exploratory analysis:** distributions, relationships, segments, hidden gems and area competition
3. **Predictive modeling:** Random Forest vs Gradient Boosting to predict ratings
4. **Visualization:** 5 charts summarizing the findings

## Data Cleaning Decisions
- Dropped unneeded columns (url, phone, menu_item)
- Converted rating from text ("4.1/5") to numeric; "NEW" and "-" became null
- Removed commas from cost and converted to numeric
- Dropped rows missing rating or cost, since they are core to the analysis
- Filled missing dish_liked with "Not available" to avoid losing about half the data
- Created a unique-restaurant view (one row per name and location), because the same restaurant appeared under several service types and inflated counts
- Kept cost outliers (up to ₹6,000), since they are genuine premium restaurants

## Key Findings
- Ratings are bell-shaped, peaking around 3.7 to 3.8. Most restaurants fall between 3.5 and 4.0.
- Cost for two is right-skewed, with most restaurants charging ₹300 to ₹500.
- Restaurants with **table booking** have clearly higher ratings (median about 4.2 vs 3.7).
- **Online ordering** has only a small effect on rating (median about 3.8 vs 3.7).
- Expensive restaurants (₹1,500+) rarely rate below 3.5, but high cost does not guarantee a high rating.
- **BTM** is the most crowded area with a below-average rating (3.57), which leaves room for a better restaurant.
- **Koramangala 5th Block** is crowded and highly rated (about 4.0), making it a tough market.
- **56 hidden gems** found (rating 4.2 or higher, under 100 votes), mostly affordable places (₹200 to ₹700).
- Top-rated cuisines (100+ restaurants): **EUROPEAN, ASIAN, BBQ**.

## Model Results
| Model | R2 | MAE |
|---|---|---|
| Random Forest | 0.37 | 0.25 |
| Gradient Boosting | 0.44 | 0.25 |

Gradient Boosting was selected as the final model. **Votes** and **cost for two** were the strongest predictors of rating.

## Recommendations
1. **Target crowded but low-rated areas** like BTM with a higher-quality offering.
2. **Offer table booking**, which is linked to higher ratings.
3. **Promote hidden gems:** high-rated restaurants with low visibility.
4. **Price in the ₹300 to ₹700 range**, where most demand and competition sit.

## Charts
![Rating distribution](images/1_rating_dist.png)
*Most restaurants are rated 3.5 to 4.0.*

![Table booking vs rating](images/2_booking.png)
*Restaurants with table booking rate higher.*

![Top cuisines](images/3_cuisines.png)
*Highest-rated cuisines with 100+ restaurants.*

![Area competition vs rating](images/4_areas.png)
*Crowded areas vary widely in average rating.*

![Rating drivers](images/5_drivers.png)
*Votes and cost for two are the strongest predictors.*

## Project Structure
```
zomato-bangalore-analysis/
├── data/
├── notebooks/
├── images/
└── README.md
```

## How to Run
1. Download `zomato.csv` from Kaggle (or use the cleaned file in `data/`)
2. Open the notebook in `notebooks/` in Jupyter or Google Colab
3. Run all cells from top to bottom

## Tools
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn

## Limitations
- Votes are partly a result of popularity, so they predict ratings but do not necessarily cause them
- No review text or time data, so trends over time and sentiment were not analyzed
- Taste and service quality are not in the data, which limits model accuracy (R2 0.44)