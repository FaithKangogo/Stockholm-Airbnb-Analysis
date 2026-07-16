# Stockholm Airbnb Market Analysis

An end-to-end data analysis of Stockholm's short-term rental market, examining the drivers of nightly price and the structure of the host landscape.

**Author:** Faith Kangogo
**Tools:** Python · SQL (SQLite) · pandas · matplotlib · seaborn · scipy

## Skills Demonstrated

- Exploratory Data Analysis (EDA)
- SQL querying (SQLite)
- Statistical hypothesis testing
- Data visualisation
- Business insight generation
- Data cleaning & preprocessing

---

## Business Question

This project investigates what drives nightly prices across Stockholm's Airbnb listings and characterises the host market. The goal is to surface patterns useful to a host setting a competitive price, or to a platform team monitoring market health.

## Data

**Source:** [Inside Airbnb](http://insideairbnb.com/get-the-data/) — Stockholm, May 2026 snapshot.

One row per active listing, covering price, location, room type, host attributes, and review activity. To reproduce this analysis, download the detailed `listings.csv.gz` file for Stockholm from the link above and place it in the project folder.

After cleaning (converting price to numeric, removing listings with no recorded price, and excluding the top 1% of prices as outliers), the working dataset contains **3,158 actively bookable listings**.

## Approach

1. **Data cleaning** — converted price from text to numeric, mapped Superhost flags, handled missing values, and removed outliers.
2. **SQL extraction** — loaded the cleaned data into an in-memory SQLite database and used SQL (`GROUP BY`, aggregation, `HAVING`, `CASE`) for analysis.
3. **Statistical testing** — applied a Welch's two-sample t-test to assess whether Superhost status is associated with price.
4. **Visualisation & interpretation** — produced charts and written business insights for each finding.

---

## Key Findings

The analysis identified five key insights that explain pricing behaviour and the structure of Stockholm's Airbnb market.

### 1. Stockholm Airbnb prices are highly right-skewed

  <img width="1923" height="722" alt="stockholm_price_and roomtype_distribution" src="https://github.com/user-attachments/assets/cf84c537-3870-4111-acd3-87d5fec76246" />
  
The median nightly price is **1,196 SEK**, with most listings between 500–1,500 SEK and a long tail of premium listings up to ~6,750 SEK.
  
 ### 2. Room type is a strong price driver. 
 
 <img width="1923" height="722" alt="stockholm_price_and roomtype_distribution" src="https://github.com/user-attachments/assets/26a1f19b-dbfc-4a16-b0d7-261725ff4cda" />
 
<img width="1473" height="869" alt="price_by_room_type" src="https://github.com/user-attachments/assets/ceed952c-8584-4e6a-a467-27b0de8c050f" />

Entire homes/apartments dominate the market (**79.6%** of listings) and command roughly **2.1× the price** of private rooms (1,684 SEK vs 808 SEK), making room type one of the clearest pricing factors observed.

### 3. Location matters. Clear centre-to-periphery price gradient.

<img width="1475" height="870" alt="price_by_neighbourhood" src="https://github.com/user-attachments/assets/879e8742-caee-4fb4-98df-13e91ac195c6" />

Central, affluent districts (Södermalm, Norrmalm, Östermalm) average ~1,700+ SEK, while outer districts average roughly half that.

 ### 4. Most hosts are casual. 
 
 <img width="1093" height="870" alt="host_types" src="https://github.com/user-attachments/assets/f2028396-be10-4de4-aefc-827810f7eb5e" />

Nearly two-thirds of hosts operate only one listing, indicating that Stockholm's Airbnb supply remains predominantly distributed among individual hosts rather than concentrated among multi-listing operators.
 
 ### 5. Superhosts don't charge significantly more. 
 
 <img width="1923" height="763" alt="superhost_test" src="https://github.com/user-attachments/assets/c19d7c8f-4b1d-448f-acdb-a2c128a2c849" />
 
Welch's t-test found no statistically significant price difference between Superhosts and regular hosts (p = 0.13). Superhosts charged marginally less on average, suggesting that Superhost status may be associated more with competitiveness or guest trust than with a direct pricing premium. 
Further analysis of occupancy and booking performance would be needed to test this interpretation.

## Repository Contents

| File | Description |
|------|-------------|
| `airbnb_market_analysis.ipynb` | The full analysis notebook |
| `price_roomtype_distribution.png` | Price distribution and room-type overview |
| `price_by_neighbourhood.png` | Average price by neighbourhood |
| `price_by_room_type.png` | Price distribution by room type |
| `superhost_price_test.png` | Superhost vs regular host price comparison |
| `host_segmentation.png` | Market share by host type |

## How to Run

1. Download Stockholm's `listings.csv.gz` from [Inside Airbnb](http://insideairbnb.com/get-the-data/) and place it in this folder.
2. Install dependencies: `pip install pandas numpy matplotlib seaborn scipy notebook`
3. Open `airbnb_market_analysis.ipynb` and run all cells top to bottom.

## Possible Extensions

- Test whether Superhost status drives higher **occupancy** rather than price, using booking/availability data.
- Build a geographic **price heat map** from the latitude/longitude columns.
- Model price as a function of multiple features (size, location, room type) using regression.

---

*Prices are in Swedish kronor (SEK). This is a portfolio project for learning and demonstration purposes.*

