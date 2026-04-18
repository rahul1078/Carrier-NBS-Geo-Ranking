# Carrier-NBS-Geo-Ranking
# Top 3 Carrier Ranking Dashboard (Florida)

## Problem

Identify the **top 3 insurance carriers** in Florida based on **Full Term Premium**, segmented by:

* County (20+ counties)
* Coverage band (Coverage A)
* Property age (Year Built bands)

This enables stakeholders to understand **carrier dominance and variation across regions and risk segments**.

---

## Dataset & Source

* Data extracted using SQL (see `/sql` folder)
* Key fields:

  * Carrier
  * Full Term Premium
  * County, State (FL)
  * Coverage A (banded)
  * Year Built (banded)

---

## Data Model

* Fact Table: `Policies`
* Dimension Tables:

  * `Coverage A`
  * `Year Form Type` (Year Built bands)
  * `Account Zip`
  * `Zip SQL` (County mapping)

Model follows a **light star schema** with relationships on keys like AccountId and Zip.

(Refer to `/images` for model screenshot)

---

## Key Logic

* **Metric:** Full Term Premium (aggregated)

* **Ranking:** Top 3 carriers per:

  * County
  * Coverage band OR Year Built band

* Ranking implemented using **DAX (RANKX)** within each segment.

---

## Dashboard Pages

1. **Coverage View**

   * Top 3 carriers by Coverage A bands
2. **Year Built View**

   * Top 3 carriers by property age bands

Filters:

* State (FL)
* County
* Year
* Month

---

## Data Refresh

* Data is refreshed **daily** via scheduled refresh in Power BI Service
* Data latency: up to 24 hours
* Depends on upstream SQL source availability

---

## Key Insights

* Certain carriers consistently dominate across multiple counties
* Rankings vary significantly across coverage bands and property age
* Smaller counties show higher volatility in top carriers

---

## Tools Used

* Power BI (data modeling, DAX, visualization)
* SQL (data extraction and preparation)

---

## Project Structure

* `/pbix` → Power BI file
* `/sql` → SQL query used
* `/images` → Dashboard & data model screenshots

---

## Notes / Assumptions

* Includes **Home and Dwelling Fire lines of business only**
* Ranking based on **issued policy premium (NBS)**

---

## How to Use

1. Open `.pbix` file in Power BI Desktop
2. Use filters to explore counties, coverage bands, and time
3. Review ranking tables for top carriers

---

## Limitations

* Data latency (up to 24 hours)
* Performance not optimized for very large datasets
* Assumes clean and consistent upstream data

---
Dashboard Screenshot: https://github.com/rahul1078/Carrier-NBS-Geo-Ranking/blob/main/Coverage%20Tab%20View.webp
Semantic Model Screenshot: https://github.com/rahul1078/Carrier-NBS-Geo-Ranking/blob/main/Semantic%20Model.png
