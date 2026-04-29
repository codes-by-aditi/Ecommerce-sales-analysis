# 🛒 Amazon India E-Commerce Sales Analysis
## End-to-End Exploratory Data Analysis | Portfolio Project
 
<p align="left">
  <img src="https://img.shields.io/badge/Python-3.10-blue?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?style=flat-square&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C9A8A?style=flat-square"/>
  <img src="https://img.shields.io/badge/Matplotlib-Plotting-11557C?style=flat-square"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=flat-square&logo=kaggle&logoColor=white"/>
  <img src="https://img.shields.io/badge/Domain-E--Commerce-FF6F00?style=flat-square"/>
</p>
> Analysed **128,975 Amazon India orders** across product categories, geographies, and fulfilment methods
> to uncover what actually drives revenue — and what's silently costing it.
 
---
 
## 🎯 Business Problem
 
> **"What drives revenue and fulfilment efficiency on Amazon India — and which product categories, geographies, and fulfilment strategies should a seller prioritise to maximise profitability?"**
 
This is not an academic exercise. This is the exact question an e-commerce analyst at a D2C brand, Amazon seller, or marketplace analytics team faces on Day 1.
 
---
 
## 📊 Dataset
 
| Attribute | Detail |
|---|---|
| **Source** | [Unlock Profits with E-Commerce Sales Data — Kaggle](https://www.kaggle.com/datasets/thedevastator/unlock-profits-with-e-commerce-sales-data) |
| **File** | `Amazon Sale Report.csv` |
| **Rows** | 128,975 |
| **Columns** | 24 |
| **Time Period** | March – June 2022 |
| **Geography** | India (all states & cities) |
 
**Key columns:** `Order ID`, `Date`, `Status`, `Fulfilment`, `Sales Channel`, `Category`, `Size`, `Qty`, `Amount`, `Ship-State`, `Ship-City`, `B2B`, `Courier Status`, `Promotion-IDs`
 
> **Note:** Dataset not included due to size. Download from Kaggle and place as `Amazon Sale Report.csv` in the root directory before running.
 
---
 
## 🛠️ Tech Stack
 
| Tool | Purpose |
|---|---|
| **Python 3.10** | Core language |
| **Pandas** | Data cleaning, GroupBy aggregations, feature engineering |
| **NumPy** | Numerical operations, outlier detection |
| **Seaborn** | Statistical visualisations |
| **Matplotlib** | Custom dual-axis plots, annotations, layout control |
| **Jupyter Notebook** | Interactive, documented analysis environment |
 
---
 
## 🧹 Data Cleaning — What Was Done & Why
 
Real-world e-commerce exports are messy. Here's exactly how each issue was handled:
 
| Issue | Strategy | Reason |
|---|---|---|
| Null `Amount` values | **Dropped rows** | Revenue analysis is impossible without a valid order value |
| Null `ship_city` / `ship_state` | **Filled → 'Unknown'** | Retain rows for non-geographic analysis |
| Null `promotion_ids` | **Filled → 'No Promotion'** | Enables promotion flag feature engineering |
| Null `fulfilled_by` | **Filled → 'Unknown'** | Preserve FBA vs merchant comparison integrity |
| Unnamed Excel artifact columns | **Dropped** | Zero analytical value |
| Mixed-case / spaced column names | **Standardised** to `lower_snake_case` | Consistency across all code |
| String columns with casing issues | **`.str.title()`** applied | Prevents groupby splitting same value into two groups |
| `Amount` / `Qty` stored as strings | **Coerced to numeric** | Required for all aggregations |
| `Date` column as object | **Parsed to datetime** | Enables time-series and month/day extraction |
| Duplicate rows | **Removed** | Prevents double-counting in aggregations |
| Outliers in `Amount` | **Flagged, retained** | High-value B2B bulk orders are legitimate — not errors |
 
---
 
## 🔧 Feature Engineering
 
11 new features created from existing columns:
 
| Feature | Source | Business Use |
|---|---|---|
| `month`, `month_name` | `date` | Monthly revenue trend analysis |
| `week` | `date` | Weekly seasonality |
| `day_of_week`, `is_weekend` | `date` | Ad scheduling — when do customers order? |
| `revenue_per_unit` | `amount ÷ qty` | Unit economics by category/size |
| `order_size` | `qty` bins | Classify orders: Single / Small / Medium / Bulk |
| `has_promotion` | `promotion_ids` | Measure promotion impact on volume & AOV |
| `is_amazon_fulfilled` | `fulfilment` | FBA vs merchant-fulfilled comparison |
| `is_cancelled` | `status` | Cancellation rate calculation |
| `is_shipped` | `status` | Filter to confirmed revenue only |
 
---
 
## 📈 Key Insights (11 Insights, 11 Visualisations)
 
### 1️⃣ Order Status & Cancellation Rate
- Mapped the full funnel: Shipped → Delivered → Cancelled → Returned
- **Cancellation rate quantified** — every 1% improvement at 100K orders = 1,000 recovered orders
- 📊 *Bar chart + Pie chart*
---
 
### 2️⃣ Revenue by Product Category
- Top 3 categories account for the majority of total revenue
- Separate comparison of **revenue volume vs average order value** per category
- High-AOV categories ≠ high-volume categories — requires different strategies
- 📊 *Dual bar chart (revenue + AOV)*
---
 
### 3️⃣ Monthly Revenue Trend
- Month-over-Month revenue growth calculated
- Visualised relationship between order volume and revenue — divergence signals AOV change
- 📊 *Dual-axis bar + line chart*
---
 
### 4️⃣ Geographic Analysis — Top States & Cities
- Maharashtra, Karnataka, and Delhi dominate by order volume
- **High-AOV states ≠ high-volume states** — critical for ad targeting decisions
- 📊 *Horizontal bar charts (revenue + AOV by state)*
---
 
### 5️⃣ Amazon FBA vs Merchant-Fulfilled
- Compared on: total orders, average order value, and **cancellation rate**
- FBA shows measurably lower cancellation rates — **quantifies the ROI of paying FBA fees**
- 📊 *3-panel bar chart comparison*
---
 
### 6️⃣ B2B vs B2C Order Analysis
- B2B orders carry **2–3× higher AOV** than B2C
- B2B shows lower cancellation rate — higher purchase intent from business buyers
- **Business case for activating Amazon Business channel**
- 📊 *Side-by-side bar: AOV + cancellation rate*
---
 
### 7️⃣ Day-of-Week Sales Pattern
- Identifies peak ordering days (weekday vs weekend split)
- Directly actionable: shift Sponsored Ads budget peaks to high-order days
- 📊 *Colour-coded bar chart (weekday vs weekend)*
---
 
### 8️⃣ Size-wise Sales Distribution
- Top 3–4 sizes account for the majority of order volume
- Restocking ratios derived from actual demand — reduces stockouts and dead inventory
- 📊 *Dual bar: orders + revenue by size*
---
 
### 9️⃣ Promotion Impact Analysis
- Orders with promotions vs without: compared on orders, AOV, and avg quantity
- Reveals whether promotions increase basket size or just discount margin
- 📊 *3-panel promotion comparison*
---
 
### 🔟 Correlation Heatmap
- Numeric + boolean features encoded and correlated
- Key signals: `b2b` ↔ `qty`, `is_amazon_fulfilled` ↔ `is_cancelled`, `has_promotion` ↔ `amount`
- 📊 *Masked lower-triangle heatmap*
---
 
### 1️⃣1️⃣ Category × Fulfilment Grouped Heatmap
- Cancellation rate broken down by every category + fulfilment method combination
- Pinpoints the exact SKU groups where switching to FBA has the highest impact
- 📊 *Pivot heatmap*
---
 
## 💡 Business Recommendations
 
| Recommendation | Expected Impact |
|---|---|
| Migrate high-cancellation SKUs to Amazon FBA | Recover ₹5L+ per 1% cancellation reduction at scale |
| Concentrate ad spend on top 3 revenue categories | Higher ROAS by focusing budget on proven performers |
| Activate Amazon Business (B2B) channel | 2–3× AOV uplift from business buyers |
| Rebalance inventory restocking by actual size demand | Reduce stockouts on best-sellers, reduce dead stock on slow sizes |
| Measure promotion ROI (net revenue, not just volume) | Stop running promotions that only discount margin without increasing basket size |
| Shift Sponsored Ads budget peaks to high-order days | Lower CPC on peak days by scheduling budget correctly |
 
---
 
## 📂 Project Structure
 
```
Amazon-Ecommerce-EDA/
│
├── Amazon Sale Report.csv          ← Dataset (download from Kaggle — not included)
├── Amazon_Ecommerce_EDA.ipynb      ← Main notebook (11 insights, 11 visualisations)
├── README.md                       ← Project documentation
│
└── visualizations/                 ← (Optional) Exported chart PNGs
    ├── order_status.png
    ├── category_revenue.png
    ├── monthly_trend.png
    ├── state_revenue.png
    ├── fba_vs_merchant.png
    ├── b2b_vs_b2c.png
    ├── day_of_week.png
    ├── size_distribution.png
    ├── promotion_impact.png
    ├── correlation_heatmap.png
    └── category_fulfil_heatmap.png
```
 
---
 
## 🚀 How to Run
 
```bash
# 1. Clone the repository
git clone https://github.com/codes-by-aditi/Amazon-Ecommerce-EDA.git
cd Amazon-Ecommerce-EDA
 
# 2. Install dependencies
pip install pandas numpy seaborn matplotlib jupyter
 
# 3. Add the dataset
# Download "Amazon Sale Report.csv" from Kaggle (link above)
# Place it in the root directory
 
# 4. Launch the notebook
jupyter notebook Amazon_Ecommerce_EDA.ipynb
 
# 5. Run all cells
# Kernel → Restart & Run All
```
 
---
 
## 💼 Skills Demonstrated
 
| Skill | How It Was Applied |
|---|---|
| **Data Cleaning** | 10-step cleaning pipeline with documented reasoning per decision |
| **Feature Engineering** | 11 new features from date, text, boolean, and numeric columns |
| **Exploratory Data Analysis** | Univariate, bivariate, grouped, and correlation analysis |
| **Business Thinking** | Every chart paired with a business-impact interpretation |
| **Pandas** | GroupBy, pivot, cut, pct_change, merge, apply, fillna, isnull |
| **Seaborn + Matplotlib** | Bar, pie, dual-axis, stacked, annotated, heatmap charts |
| **Statistical Thinking** | IQR outlier detection, MoM growth rate, rate calculations |
| **Communication** | Markdown-structured notebook with insight captions on every chart |
| **Code Quality** | Clean, commented, reproducible — section-by-section structure |
 
---
 
## 🔮 Future Improvements
 
- [ ] Add interactive **Power BI / Tableau dashboard** for live filtering by state, category, and month
- [ ] Build a **cancellation predictor** (logistic regression or XGBoost) using order features
- [ ] Perform **RFM segmentation** if customer ID data becomes available
- [ ] Add **cohort analysis** to track repeat purchase behaviour over time
- [ ] **Hypothesis testing** — is the FBA cancellation rate difference statistically significant?
---
 
## 👩‍💻 Author
 
**Aditi Chaudhary**  
Aspiring Data Scientist | Python · SQL · Machine Learning | VTU '28
 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/aditi-chaudhary-bb3324250)
[![GitHub](https://img.shields.io/badge/GitHub-codes--by--aditi-181717?style=flat-square&logo=github)](https://github.com/codes-by-aditi)
[![Kaggle](https://img.shields.io/badge/Kaggle-Profile-20BEFF?style=flat-square&logo=kaggle)](https://www.kaggle.com/)
 
---
 
> ⭐ If this project was useful or interesting, consider starring the repo — it helps others find it!
