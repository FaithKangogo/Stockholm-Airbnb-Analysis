# Stockholm Airbnb Market Analysis

An end-to-end data analysis of Stockholm's short-term rental market, examining the drivers of nightly price and the structure of the host landscape.

**Author:** Faith Kangogo &nbsp;&nbsp; **Tools:** Python · SQL (SQLite) · pandas · matplotlib · seaborn · scipy

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

**Source:** [Inside Airbnb](http://insideairbnb.com/get-the-data/), Stockholm, 30 June 2026 snapshot.

One row per active listing, covering price, location, room type, host attributes, and review activity. To reproduce this analysis, download the detailed `listings.csv.gz` file for Stockholm from the link above and place it in the project folder.

After cleaning (converting price to numeric, removing listings with no recorded price, and excluding the top 1% of prices as outliers), the working dataset contains **3,231 actively bookable listings** out of 4,806 scraped.

## Approach

1. **Data cleaning:** converted price from text to numeric, mapped Superhost flags, handled missing values, and removed outliers.
2. **SQL extraction:** loaded the cleaned data into an in-memory SQLite database and used SQL (`GROUP BY`, aggregation, `HAVING`, `CASE`) for analysis.
3. **Statistical testing:** applied a Welch's two-sample t-test to assess whether Superhost status is associated with price.
4. **Visualisation & interpretation:** produced charts and written business insights for each finding.

---

## Key Findings

### 1. Stockholm Airbnb prices are highly right-skewed

![Price and room type distribution](stockholm_price_roomtype_distribution.png)

The median nightly price is **1,918 SEK**, with half of all listings between roughly 1,100 and 3,000 SEK and a long tail of premium listings up to about 9,100 SEK.

### 2. Room type is a strong price driver

![Price by room type](price_by_room_type.png)

Entire homes/apartments dominate the market (**81% of listings**) and average roughly **2.6× the price** of private rooms (2,570 SEK vs 1,002 SEK), making room type one of the clearest pricing factors observed.

### 3. Location matters, but it is a tendency rather than a rule

![Price by neighbourhood](price_by_neighbourhood.png)

Södermalm tops the market at about 2,672 SEK on average, with the premium central districts (Östermalm, Norrmalm) close behind, while the cheapest outer districts (Skärholmen at 1,178 SEK, Rinkeby-Tensta at 1,226 SEK) average less than half of Södermalm's rate. Interestingly, some districts outside the centre (Bromma, Farsta) also rank near the top, so the centre-to-periphery gradient holds broadly but with exceptions worth investigating.

### 4. Hosting is overwhelmingly casual, with a small professional tail

![Host types](host_types.png)

About **9 in 10 hosts** operate a single listing, and these single-listing hosts supply roughly **two-thirds (65%) of all listings**. At the other end, a handful of professional operators run large portfolios, with the biggest managing over 50 listings.

### 5. Superhosts don't charge significantly more

![Superhost test](superhost_test.png)

Superhosts average slightly higher prices than regular hosts (2,344 vs 2,237 SEK, about 5% more), but a Welch's t-test finds the difference is not statistically significant at the 5% level (p = 0.09). Superhost status appears to be associated more with guest trust and competitiveness than with a clear pricing premium. Further analysis of occupancy and booking performance would be needed to test this interpretation.

## Repository Contents

| File | Description |
| --- | --- |
| `airbnb_market_analysis.ipynb` | The full analysis notebook |
| `stockholm_price_roomtype_distribution.png` | Price distribution and room-type overview |
| `price_by_neighbourhood.png` | Average price by neighbourhood |
| `price_by_room_type.png` | Price distribution by room type |
| `superhost_test.png` | Superhost vs regular host price comparison |
| `host_types.png` | Market share by host type |

## How to Run

1. Download Stockholm's `listings.csv.gz` from [Inside Airbnb](http://insideairbnb.com/get-the-data/) and place it in this folder.
2. Install dependencies: `pip install pandas numpy matplotlib seaborn scipy notebook`
3. Open `airbnb_market_analysis.ipynb` and run all cells top to bottom.

## Possible Extensions

- Test whether Superhost status drives higher **occupancy** rather than price, using booking/availability data.
- Investigate why some non-central districts (Bromma, Farsta) command high prices.
- Model price as a function of multiple features (size, location, room type) using regression.

---

*Prices are in Swedish kronor (SEK). This is a portfolio project for learning and demonstration purposes.*
