# Amazon vs eBay — Beauty Price Comparison Dashboard

A data pipeline and interactive Streamlit dashboard that scrapes Amazon.com and eBay side-by-side for the same beauty & personal care keywords, then compares prices at the brand and keyword level — including a **gray market risk analysis** for CPG brands concerned about MAP (Minimum Advertised Price) enforcement.

Built to answer a question that matters to CPG sales and brand teams: *are your products being sold cheaper on eBay than Amazon, and does that signal unauthorized reseller activity?*

---

## What It Does

- Scrapes the top 20 results from both **Amazon** and **eBay** for 12 beauty keywords using ScraperAPI
- Normalizes brand names from raw product titles using shared regex patterns
- Compares **average prices by brand and keyword** across both platforms
- Flags brands where eBay is significantly cheaper as **gray market risk**
- Visualizes everything in a 4-tab Streamlit dashboard with sidebar filters

---

## Dashboard Tabs

| Tab | What You See |
|---|---|
| **Brand Comparison** | Grouped bar chart (Amazon vs eBay avg price), price gap waterfall, summary table |
| **Keyword Breakdown** | Avg price by keyword across platforms, gap % bar chart |
| **Gray Market Risk** | Risk-flagged brands, color-coded by severity, with data table |
| **Raw Data** | Side-by-side Amazon and eBay listings with filters |

---

## Key Findings (Live Scraped Data)

**Amazon is cheaper than eBay across all 12 keywords** — the opposite of the common assumption. Amazon's brand stores, Prime fulfillment, and high volume drive mass-market prices down. eBay skews toward bundles, niche imports, and premium products.

| Keyword | Amazon Avg | eBay Avg |
|---|---|---|
| Hair mask | $14.05 | $44.97 |
| Deodorant | $11.56 | $34.46 |
| Conditioner | $12.40 | $30.94 |
| Moisturizer | $20.53 | $30.31 |

**Gray market risk brands** — where eBay is significantly *cheaper* than Amazon, signalling potential unauthorized reseller activity or lack of MAP enforcement:

| Brand | Amazon Avg | eBay Avg | Gap | Risk |
|---|---|---|---|---|
| Estée Lauder | $52.00 | $19.99 | 62% cheaper on eBay | 🔴 High |
| Clinique | $28.88 | $15.00 | 48% cheaper on eBay | 🔴 High |
| Tarte | $28.00 | $17.99 | 36% cheaper on eBay | 🔴 High |
| The Ordinary | $8.20 | $5.70 | 31% cheaper on eBay | 🔴 High |
| La Roche-Posay | $25.49 | $19.99 | 22% cheaper on eBay | 🟡 Medium |


---

## How Gray Market Risk Is Calculated

```
price_gap  = amazon_avg_price − ebay_avg_price
gap_pct    = price_gap / amazon_avg_price × 100

🔴 High risk   → eBay ≥ 30% cheaper than Amazon
🟡 Medium risk → eBay 15–30% cheaper than Amazon
```

A large positive gap suggests eBay listings may come from unauthorized third-party resellers, liquidation stock, or gray market imports — all of which undermine a brand's pricing integrity and MAP policy enforcement.

---

## eBay Scraper Filters

eBay results are filtered to ensure a fair comparison with Amazon:

- **Buy It Now only** (`LH_BIN=1`) — excludes auctions
- **New items only** (`LH_ItemCondition=1000`) — excludes used/refurbished

---

## Keywords Tracked

| Category | Keywords |
|---|---|
| Skincare | moisturizer, face serum, sunscreen, eye cream |
| Haircare | shampoo, conditioner, hair mask |
| Makeup | foundation, mascara, lip balm |
| Personal Care | deodorant, body lotion |


