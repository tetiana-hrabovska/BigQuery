# BigQuery SQL Practice: Google Analytics Sample Dataset #

SQL analysis of e-commerce web analytics data in Google BigQuery. The project contains 8 queries of increasing complexity, from simple counts to working with nested and repeated fields.

📄 **Full write-up with queries and result screenshots:** [BigQuery_GA_Sample_Homework.pdf](BigQuery_GA_Sample_Homework.pdf)

## Dataset

`bigquery-public-data.google_analytics_sample.ga_sessions_*`

Obfuscated Google Analytics 360 data from the [Google Merchandise Store](https://shop.googlemerchandisestore.com/), an online store selling Google-branded products. The data covers **1 August 2016 - 1 August 2017** and is stored as one table per day (`ga_sessions_YYYYMMDD`).

- **Grain:** one row = one session
- **Nested fields:** `totals`, `trafficSource`, `device`, `geoNetwork`
- **Repeated field:** `hits` (pageviews, events and transactions inside a session)

Column descriptions: [BigQuery Export schema (Google Analytics Help)](https://support.google.com/analytics/answer/3437719?hl=en)

## Tasks and key results

| # | Task | Result |
|---|------|--------|
| 1 | Total number of sessions | 903,653 |
| 2 | Sessions on 31 July 2017 | 2,620 |
| 3 | Sessions by device category | desktop 664,479 / mobile 208,725 / tablet 30,449 |
| 4 | Top 5 traffic sources | (direct), google, youtube.com, Partners, analytics.google.com |
| 5 | Top 10 pages by pageviews | `/home` leads with 981,285 pageviews |
| 6 | Average session duration | 131.33 seconds |
| 7 | Top 5 countries by sessions | United States (364,744), India, United Kingdom, ... |
| 8 | Transactions and revenue | 12,115 transactions, $1,780,149.23 revenue |

## SQL concepts demonstrated

- Table wildcards (`ga_sessions_*`) and `_TABLE_SUFFIX` filtering to reduce scanned data
- Aggregation: `COUNT`, `SUM`, `AVG`, `GROUP BY`, `ORDER BY`, `LIMIT`
- Nested records accessed with dot notation (`device.deviceCategory`)
- Flattening repeated fields with `UNNEST(hits)`
- Handling `NULL` values (`IFNULL`)
- Reading the schema documentation to interpret units: `totalTransactionRevenue` is stored multiplied by 10^6, so it is divided by 1,000,000 to match Google Analytics

## Tools

Google BigQuery (Standard SQL, sandbox)
