# 🛍️ Consumer Behaviour Analysis

A complete end-to-end data analytics project that explores retail customer shopping behaviour — from raw data through preprocessing and EDA, to an interactive Power BI dashboard — to help a company make smarter marketing, product, and logistics decisions.

---

## 📁 Project Structure

```
Consumer-Behaviour-Analysis/
│
├── Customer_Behaviour_dataset.csv      # Raw dataset (3,900 customers, 18 columns)
├── Data Preprocessing.ipynb            # Python notebook: cleaning, EDA & feature engineering
├── cleaned_customer_data.csv           # Cleaned & enriched output (21 columns)
└── Consumer-Behavior-Analysis.pbix     # Power BI interactive dashboard
```

---

## 🎯 Problem Statement

> *"How can the company leverage consumer shopping data to identify trends, improve customer engagement and optimise marketing and product strategies?"*

A leading retail company wants to better understand its customers' shopping behaviour in order to improve sales, customer satisfaction, and long-term loyalty. Management has noticed shifting purchasing patterns across demographics, product categories, and sales channels (online vs. offline) and needs data-driven answers.

---

## 📊 Dataset Overview

**Source file:** `Customer_Behaviour_dataset.csv`  
**Records:** 3,900 customers  
**Original columns:** 18

| Column | Type | Description |
|--------|------|-------------|
| Customer ID | int | Unique customer identifier |
| Age | int | Customer age (18–70) |
| Gender | str | Male / Female |
| Item Purchased | str | 25 distinct product types |
| Category | str | Clothing, Accessories, Footwear, Outerwear |
| Purchase Amount (USD) | int | Transaction value ($20–$100) |
| Location | str | US state |
| Size | str | S, M, L, XL |
| Color | str | Product colour |
| Season | str | Spring, Summer, Fall, Winter |
| Review Rating | float | 2.5–5.0 (37 missing values) |
| Subscription Status | str | Yes / No |
| Shipping Type | str | 6 shipping methods |
| Discount Applied | str | Yes / No |
| Promo Code Used | str | Yes / No |
| Previous Purchases | int | Number of prior orders (1–50) |
| Payment Method | str | 6 payment options |
| Frequency of Purchases | str | Weekly → Annually |

---

## 🔧 Data Preprocessing (`Data Preprocessing.ipynb`)

### Libraries Used
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### Steps Performed

#### 1. Initial Inspection
- Loaded dataset and verified shape: **(3900, 18)**
- Checked column types, missing values, and duplicates
- Found **37 missing values** only in `Review Rating`
- **0 duplicate rows**

#### 2. Outlier Check — Review Rating
Applied the **IQR method** to check for outliers:
```
Q1: 3.1 | Q3: 4.4 | IQR: 1.3
Lower bound: 1.15 | Upper bound: 6.35
Outliers found: 0
```
No outliers — safe to fill missing values with the mean.

#### 3. Missing Value Imputation
```python
df['Review Rating'] = df['Review Rating'].fillna(df['Review Rating'].mean())
# Filled with mean ≈ 3.75
```

#### 4. Feature Engineering — 3 New Columns

| New Column | Method | Values |
|------------|--------|--------|
| `Age Group` | `pd.cut()` on Age | 18-25 · 26-35 · 36-45 · 46-55 · 56-70 |
| `Shopping Channel` | Inferred from Shipping Type | Online · Offline |
| `Frequency Score` | Mapped from Frequency of Purchases | 1 (Annually) → 7 (Weekly) |

**Cleaned output:** `cleaned_customer_data.csv` — 3,900 rows × **21 columns**

---

## 🔍 Key Questions Answered (EDA)

### Q1 — Which age group shops the most?
**56–70** is the largest segment (1,105 customers), followed by 46–55 (753).

### Q2 — Which demographic engages least in online shopping?
Surprisingly, **neither gender nor age group** significantly differs. Online shopping is uniformly preferred across all segments at ~82–85%. Gender has minimal impact — Male offline: 17%, Female offline: 15%. The company's online platform has **broad, universal appeal**.

### Q3 — Which product sells most across demographics?
No single "hero product" dominates overall (top items: Blouse, Pants, Jewelry — all tied at ~171 each).  
However, **age is a stronger predictor of product preference than gender**:

| Age Group | Top Products |
|-----------|-------------|
| 18–25 | Sweater, Coat, Dress |
| 26–35 | Shirt, Backpack, Jewelry |
| 36–45 | Scarf, Pants, Jacket |
| 46–55 | Shoes, Boots, Sandals |
| 56–70 | Jewelry, Handbag, Dress |

**Recommendation:** Adopt age-segmented product & marketing strategies rather than one-size-fits-all campaigns.

### Q4 — Which product category receives the worst ratings?
All categories are rated nearly identically — ratings range from **3.72 to 3.79**. Clothing scores lowest (3.72); Footwear scores highest (3.79). No category stands out as a serious satisfaction concern.

### Q5 — Which season drives the highest sales?
Spring leads slightly in transaction volume (≈1,020), with all four seasons remaining fairly close. Average spend is slightly higher in Winter (~$62).

### Q6 — Do discounts drive repeat purchases?
Customers who received discounts have marginally higher previous purchase counts, suggesting discounts contribute to retention but are not the sole driver.

### Q7 — Do higher-rated customers shop more frequently?
A positive correlation exists — customers who rate products higher tend to purchase more frequently, reinforcing that satisfaction drives loyalty.

### Q8 — Online vs. offline product sales
74% of all purchases are made online, 26% offline. Product preferences are consistent across channels.

### Q9 — Payment method usage
Payment methods are well-distributed across 6 options. Credit Card leads (~22%), with PayPal, Cash, Venmo, Debit Card, and Bank Transfer all closely following. No dominant single method.

### Q10 — Which customers shop least frequently?
Customers marked "Annually" represent the largest single frequency group (Frequency Score = 1), indicating a significant one-time or rare-buyer segment worth targeting with re-engagement campaigns.

---

## 📈 Power BI Dashboard (`Consumer-Behavior-Analysis.pbix`)

An interactive **2-page** executive dashboard built in Power BI Desktop.

### Pages

| Page | Title | Focus |
|------|-------|-------|
| 1 | **Customer Behaviour Dashboard** | KPI cards, age group distribution, seasonal sales, top products by gender, online vs offline by gender |
| 2 | **Loyalty & Retention Analysis** | Discount impact, rating by frequency, payment method usage, annual shopper profile |

---

### Page 1 — Customer Behaviour Dashboard

#### KPI Cards (4 cards across the top)
| Metric | Value |
|--------|-------|
| Total Revenue ($) | **233K** |
| Total Customers | **3.9K** |
| Avg. Review Rating | **3.75** |
| Avg. Previous Purchases | **25.35** |

#### Visuals
| Chart | Type | Key Finding |
|-------|------|-------------|
| **Customers by Age Group** | Horizontal bar chart | 56–70 is the largest group (1.1K), 18–25 is smallest (0.6K) |
| **Total Sales by Season** | Clustered column chart | Fall leads ($60K), all seasons are close ($56K–$60K) |
| **Top 6 Products by Gender** | Grouped horizontal bar chart | Males dominate all top products; Sweater is the overall leader |
| **Online vs Offline Shopping by Gender** | Clustered column chart | Males: 2.2K online / 0.5K offline · Females: 1.1K online / 0.2K offline |

---

### Page 2 — Loyalty & Retention Analysis

#### Visuals
| Chart | Type | Key Finding |
|-------|------|-------------|
| **Discount Applied vs Avg Previous Purchases** | Horizontal bar chart | Discounted buyers avg 25.74 prior purchases vs 25.06 without discount — marginal but positive effect |
| **Avg. Review Rating by Purchase Frequency** | Column chart | Ratings are nearly identical across all frequency groups (3.71–3.78); frequency doesn't heavily influence satisfaction |
| **Payment Method Usage** | Line/area chart | Credit Card leads (169), Bank Transfer is lowest (145); distribution is fairly even across all 6 methods |
| **Annual Shoppers by Age Group** | Column chart | 56–70 has the most annual shoppers (187); 26–35 has the fewest (87) |
| **Annual Shoppers by Gender** | Donut chart | Male: 387 (67.66%) · Female: 185 (32.34%) |
| **Annual Shoppers by Category** | Bar chart | Clothing dominates (258), Outerwear is lowest (43) |

---

## 💡 Business Insights Summary

| # | Insight | Recommendation |
|---|---------|----------------|
| 1 | 56–70 is the largest and highest-spending segment | Prioritise loyalty programs and premium product lines for this group |
| 2 | Online shopping is preferred by all demographics equally | Invest in mobile UX and personalised e-commerce across all segments |
| 3 | Age predicts product preference better than gender | Run age-segmented marketing campaigns, not gender-based |
| 4 | No hero product — uniform distribution across 25 items | Diversify inventory equally; avoid over-stocking any single item |
| 5 | Credit Card leads payments, but distribution is diverse | Support all 6 payment methods; no need to push a single option |
| 6 | 17% of shoppers buy offline | Maintain store presence but prioritise digital investment |
| 7 | ~18% of customers rate below 3.0 | Deploy follow-up surveys and NPS outreach to low-raters |
| 8 | Discount and promo code use is ~41–43% | Headroom to grow promo adoption among non-subscribers |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Python 3.x | Data analysis & preprocessing |
| Pandas | Data manipulation & feature engineering |
| Matplotlib / Seaborn | EDA visualisations |
| Jupyter Notebook | Interactive analysis environment |
| Power BI Desktop | Interactive dashboard |

---

## 🚀 How to Run

### Python Notebook
1. Clone this repository
2. Install dependencies:
   ```bash
   pip install pandas matplotlib seaborn jupyter
   ```
3. Open `Data Preprocessing.ipynb` in Jupyter:
   ```bash
   jupyter notebook "Data Preprocessing.ipynb"
   ```
4. Run all cells — `cleaned_customer_data.csv` will be regenerated

### Power BI Dashboard
1. Open **Power BI Desktop**
2. File → Open → select `Consumer-Behavior-Analysis.pbix`
3. If prompted, update the data source path to point to your local `cleaned_customer_data.csv`

---

## 📚 Acknowledgements

This project was built as a learning exercise following the **Data Analyst Complete Guide**, practising every stage of a real analytics workflow:

1. Problem definition
2. Data collection & loading
3. Data quality checks
4. Cleaning & preprocessing
5. Exploratory data analysis
6. Feature engineering
7. Business insight generation
8. Dashboard visualisation

---

## 👤 Author

**Kaif Ansari**  
Aspiring Data Analyst | Python · SQL · Power BI

---

*⭐ If you found this project helpful, feel free to star the repository!*
