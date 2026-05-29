# Indian Startup Funding Trends (2015–2020)

End-to-end data analytics project analyzing a decade of Indian startup funding data — from raw CSV to a relational database to an interactive Power BI dashboard.

---

## Tech Stack

| Layer | Tools |
|---|---|
| Data Cleaning | Python, Pandas |
| Database | SQLite, SQL |
| Analytics | SQL (CTEs, Window Functions) |
| Visualization | Power BI |

---

## Project Structure

```
├── Startup_Funding.ipynb   # Full ETL + SQL analysis notebook
├── dim_startups.csv        # Dimension table — one row per startup
├── fact_funding.csv        # Fact table — one row per funding round
```

---

## What I Built

### 1. ETL Pipeline
- Cleaned ~2,300 raw funding records using custom Pandas functions
- Resolved malformed numeric strings (Indian comma formatting), URL-contaminated startup names, and inconsistent city/date formats
- Loaded clean data into a normalized SQLite database with a star schema (`startups` + `funding_rounds` tables)

### 2. SQL Analytics
- **Aggregations** — total funding and deal count by city
- **CTE** — identified the highest-funded startup per city without losing row-level detail
- **Window Function** — `RANK() OVER (PARTITION BY city_location)` to rank every startup within its city by deal size
- **Investor analysis** — traced Tiger Global's portfolio (BYJU'S $200M, Zenoti, Grey Orange)

### 3. Power BI Dashboard
- KPI cards: **$38B total funding**, **2,349 funding rounds**
- Top 10 cities bar chart — Bangalore leads at **$16.4B**, Mumbai at **$5B**
- Funding stage donut chart with Top N filter to handle long-tail noise
- Connected directly to SQLite data mart via dimensional CSV exports

---

## Key Findings

- **Bangalore** received 4x more funding than Mumbai ($16.4B vs $5B) and led in deal volume (850 rounds)
- **Tiger Global** was the most active large-ticket investor — BYJU'S alone received $200M
- **Private Equity and Series B/C** rounds dominated total dollar value despite Seed rounds being higher in volume
- Several startup names in the raw data were stored as full URLs — cleaned during ETL

---

## How to Run

1. Clone the repo
2. Open `Startup_Funding.ipynb` in Jupyter or Google Colab
3. Upload `startup_funding.csv` (source data)
4. Run all cells — the SQLite DB and CSV exports are generated automatically
