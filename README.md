# Stockholm Airbnb Market Analysis

An end-to-end data analysis of Stockholm's short-term rental market, examining the drivers of nightly price and the structure of the host landscape.

**Author:** Faith Kangogo
**Tools:** Python · SQL (SQLite) · pandas · matplotlib · seaborn · scipy

---

## Objective

This project investigates what drives nightly price across Stockholm's Airbnb listings and characterises the host market. The goal is to surface patterns useful to a host setting a competitive price, or to a platform team monitoring market health.

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

- **Prices are right-skewed.** The median nightly price is **1,196 SEK**, with most listings between 500–1,500 SEK and a long tail of premium listings up to ~6,750 SEK.
- **Room type is a strong price driver.** Entire homes/apartments dominate the market (**79.6%** of listings) and command roughly **2.1× the price** of private rooms (1,684 SEK vs 808 SEK).
- **Clear centre-to-periphery price gradient.** Central, affluent districts (Södermalm, Norrmalm, Östermalm) average ~1,700+ SEK, while outer districts average roughly half that.
- **Superhost status showed no significant price premium** (Welch's t-test, p = 0.13). Superhosts charged marginally *less* on average — suggesting the badge functions as a trust/competitiveness signal rather than a pricing lever.
- **The market is mostly casual hosts** (62% run a single listing), yet casual hosts charge *more* than professional operators — likely because they tend to list larger, whole-home properties.

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

