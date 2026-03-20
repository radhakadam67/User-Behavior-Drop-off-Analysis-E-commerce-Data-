# eCommerce User Behaviour & Drop-off Analysis

A end-to-end data analytics project built on the Kaggle **eCommerce Behavior Data from Multi Category Store** dataset. The project covers data loading, exploratory analysis, SQL querying, and an interactive dashboard — structured as a portfolio piece for a Data Analyst role.

---

## Dataset

**Source:** [Kaggle — eCommerce behavior data from multi category store](https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store)

| File | Size (approx) | Period |
|---|---|---|
| `2019-Oct.csv` | ~5 GB | October 2019 |
| `2019-Nov.csv` | ~9 GB | November 2019 |

**Key columns:**

| Column | Description |
|---|---|
| `event_time` | Timestamp of the event |
| `event_type` | `view`, `cart`, or `purchase` |
| `product_id` | Unique product identifier |
| `category_code` | Full category path (e.g. `electronics.smartphone`) |
| `brand` | Product brand |
| `price` | Product price in USD |
| `user_id` | Unique user identifier |
| `user_session` | Session identifier |

---

## Tech Stack

| Layer | Tools |
|---|---|
| Data processing | Python, Pandas, NumPy |
| Visualisation | Matplotlib, Seaborn |
| SQL analysis | SQLite (in-memory via `sqlite3`) |
| Interactive dashboard | Plotly (exported as standalone HTML) |
| Environment | Kaggle Notebook |

---

## Project Structure

```
ecommerce-analysis/
│
├── Cell 1  — Data Loading (sampled 500k rows per file)
├── Cell 2  — Cleaning & Feature Engineering
├── Cell 3  — Sanity Check
│
├── Cell 4  — Analysis 1 : Funnel Analysis
├── Cell 5  — Analysis 2 : Category-Level Analysis
├── Cell 6  — Analysis 3 : Price Sensitivity Analysis
├── Cell 7  — Analysis 4 : Time-Based Analysis
├── Cell 8  — Analysis 5 : User Segmentation
│
├── Cell 9  — SQL Analysis (9 queries via SQLite)
└── Cell 10 — Interactive Dashboard (Plotly HTML)
```

---

## Feature Engineering

Features added during preprocessing:

| Feature | Description |
|---|---|
| `hour` | Hour of event (0–23) |
| `day_of_week` | Day name (Monday–Sunday) |
| `date` | Calendar date |
| `month` | Month number |
| `main_category` | Top-level category extracted from `category_code` |
| `price_range` | Price bucket: `<$20`, `$20-50`, `$50-100`, `$100-200`, `$200-500`, `$500+` |

---

## Analyses

### Analysis 1 — Funnel Analysis
Builds a user-level View → Cart → Purchase funnel.

- Unique users at each stage
- View → Cart conversion rate
- Cart → Purchase conversion rate
- Overall conversion rate
- Drop-off rate at each stage
- User breakdown: viewed only / carted but not purchased / purchased

**Output:** `analysis1_funnel.png`

---

### Analysis 2 — Category-Level Analysis
Compares funnel performance across product categories.

- View → Purchase conversion rate per category
- Cart → Purchase rate per category
- High-interest / low-conversion category identification (high traffic, conversion < 2%)
- Event volume by category
- Heatmap of funnel stage rates across categories

**Output:** `analysis2_category.png`

---

### Analysis 3 — Price Sensitivity Analysis
Examines how product pricing affects purchase behaviour.

- Conversion rate by price range bucket
- Cart rate vs purchase rate comparison
- Average and median price per event type (view / cart / purchase)
- Price uplift: difference between avg viewed price and avg purchased price
- Price distribution: views vs purchases (histogram + box plot)

**Output:** `analysis3_price.png`

---

### Analysis 4 — Time-Based Analysis
Identifies peak activity windows and conversion timing patterns.

- Hourly user activity (views, carts, purchases)
- Hourly conversion rate with peak hour highlighted
- Day-of-week activity and conversion comparison
- Best and worst converting days identified

**Output:** `analysis4_time.png`

---

### Analysis 5 — User Segmentation
Segments users by purchase behaviour and profiles each group.

| Segment | Definition |
|---|---|
| Browser | 0 purchases |
| One-Time Buyer | Exactly 1 purchase |
| Repeat Buyer | 2–3 purchases |
| High-Value Customer | 4+ purchases |

Metrics per segment: user count, avg spend, total revenue, revenue share %, avg events, avg sessions, avg active days, spend distribution.

**Output:** `analysis5_segmentation.png`

---

## SQL Analysis (Cell 9)

All analyses are replicated in SQL using an in-memory SQLite database. Nine queries are run covering:

| Query | Topic |
|---|---|
| SQL-1 | Funnel conversion and drop-off rates |
| SQL-2 | Category conversion rates (top 12) |
| SQL-3 | High-interest / low-conversion categories |
| SQL-4 | Average price by event type |
| SQL-5 | Conversion rate by price range |
| SQL-6 | Hourly conversion ranked |
| SQL-7 | Day-of-week conversion |
| SQL-8 | User segment summary |
| SQL-9 | Top 10 highest-value users |

Key SQL techniques used: `CTEs`, `CASE WHEN` aggregations, `NULLIF` for safe division, `RANK() OVER`, `HAVING` filters, and subqueries.

---

## Interactive Dashboard (Cell 10)

A single-file interactive Plotly dashboard covering all 5 analysis areas.

**Output:** `ecommerce_dashboard.html` — open in any browser, no server needed.

| Panel | Content |
|---|---|
| 1A | Funnel users per stage (bar) |
| 1B | Funnel drop-off rates (horizontal bar) |
| 2A | Category conversion rate (bar) |
| 2B | Views vs purchases bubble chart |
| 3A | Conversion rate by price range (grouped bar) |
| 3B | Price distribution: views vs purchases (histogram) |
| 4A | Hourly user activity (multi-line) |
| 4B | Hourly conversion rate (filled area) |
| 5A | User segment distribution (donut) |
| 5B | Average spend by segment (bar) |

---

## How to Run (Kaggle)

1. Open a new Kaggle Notebook
2. Add the dataset: **eCommerce behavior data from multi category store**
3. Run cells **1 → 2 → 3** to load and prepare data
4. Run cells **4 → 8** for all 5 analyses
5. Run cell **9** for SQL output
6. Run cell **10** for the interactive dashboard

> Each cell is fully self-contained. No `.py` files or imports between cells are needed.

---

## Key Findings (Sample — will vary by sample)

- The largest drop-off occurs at the **View → Cart** stage, indicating a browse-heavy user base
- **Electronics** and **computers** drive the highest traffic but show below-average conversion
- Products priced **$20–$100** show the strongest conversion rates
- Peak user activity occurs in the **evening hours (18:00–21:00)**
- **Browsers** make up the majority of users but contribute zero revenue; **High-Value Customers** are a small segment that drives a disproportionate share of revenue

---

## Skills Demonstrated

- Data cleaning and feature engineering with Pandas
- Exploratory data analysis with Matplotlib and Seaborn
- Funnel analysis and conversion rate calculation
- Customer segmentation
- SQL aggregations, window functions, and CTEs
- Interactive dashboard creation with Plotly
- Working with large datasets efficiently (sampling strategy)
- Kaggle notebook workflow

---

## Author

Built as a portfolio project to demonstrate end-to-end data analytics skills across Python, SQL, and data visualisation.
