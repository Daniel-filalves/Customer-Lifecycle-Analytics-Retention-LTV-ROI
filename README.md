# 📊 Customer Lifecycle & Marketing Efficiency Analysis — Y.Afisha (CAC, LTV, ROI/ROMI)

## 📌 Overview
This project analyses **product usage**, **sales performance**, and **marketing efficiency** for Y.Afisha using event logs, purchase data, and marketing costs.  
The goal is to understand the **customer lifecycle** (acquisition → retention → monetisation) and provide **budget allocation recommendations** based on performance metrics such as **DAU/WAU/MAU, retention cohorts, AOV, LTV, CAC, ROI/ROMI**.

---

## 🎯 Business Goal
Evaluate the efficiency of marketing investments and recommend:
- **where to invest (best-performing channels)**
- **how to reallocate budget (reduce waste and scale winners)**

---

## 🧾 Data Sources
This analysis uses three datasets:

- `visits_log_us.csv` — sessions and acquisition attributes  
- `orders_log_us.csv` — purchases and revenue  
- `costs_us.csv` — marketing spend by source/channel  

---

## 🔧 Data Preparation
Key preprocessing steps:
- Renamed columns to consistent `snake_case`
- Converted types (`datetime`, numeric fields)
- Created:
  - `date` (daily granularity)
  - `session_duration_min`
  - purchase month periods (`Period[M]`) for cohort modelling
- Built **user registration table** (`users_reg`) containing:
  - first visit timestamp
  - first device
  - first acquisition source (`first_source_id`)

---

## 📈 Part 1 — Product Usage Metrics

### KPIs computed
- **DAU / WAU / MAU**  
  - calendar-based and rolling (7 / 30 days)
- **Sessions per day**
- **Session duration (minutes)**
- **Retention cohorts (monthly)** with heatmap

### Output examples
- Daily metrics consolidated for easy plotting
- Monthly retention heatmap by cohort (`first_month`) vs `lifetime`

---

## 💰 Part 2 — Sales & Customer Value

### KPIs computed
- Orders per day/week/month
- Orders per user (1 order vs repeat buyers)
- **AOV (Average Order Value)**:
  - global
  - by month
  - by first device

### LTV Cohorts
- Cohorts based on **first purchase month**
- LTV computed as:
  - Revenue per cohort / number of buyers
  - **Cumulative LTV** over monthly lifetime (`period_number`)
- LTV heatmap produced to visualise cohort monetisation over time

---

## 📣 Part 3 — Marketing Efficiency (CAC, ROI/ROMI)

### Spend Analysis
- Total marketing spend
- Spend by channel (`source_id`)
- Spend by month and by channel-month

### CAC (Customer Acquisition Cost)
CAC computed:
- total CAC per source
- CAC per source and acquisition month (based on first purchase month)

### ROI / ROMI
Two perspectives:
1. **Cohort ROMI**
   - `ROMI = LTV / CAC`
   - Cohort-based ROMI heatmap (cohort month × lifetime)
2. **ROI by Source**
   - monthly ROI trend for channels where revenue and spend overlap
   - `ROI = revenue / costs - 1`

---

## ✅ Executive Summary (Key Findings)
- ROI is positive on average, but **highly unequal by source**
- **Best-performing sources:** `source_id 3`, `source_id 5`, `source_id 7`  
  - consistent ROI roughly between **+45% and +70%**
- **CAC median ≈ $19**
  - sources **3, 5, 7** have CAC below median and positive ROI → **recommended**
- **LTV at 6 months ≈ $52**
  - cohorts from sources **3 and 7** reach **$65–70**
- **AOV ≈ $11** (stable)
  - desktop users spend ~**+15%** more than mobile
- Retention:
  - **~37% return within ≤7 days**
  - median time between sessions ~**5 days**

---

## 🎯 Recommendations
### A) Scale winners (controlled growth)
- Increase budget **+20%** for: `source_id 3`, `5`, `7`
- Re-evaluate after **4 weeks** using CAC, ROI, and cohort LTV trends

### B) Maintain / optimise
- `source_id 6` shows weak positive ROI but instability → maintain and optimise creatives/targeting

### C) Reduce / pause
- Reduce **-40%** or pause: `source_id 1`, `2`
  - negative ROI and high CAC
  - keep only if required for awareness/brand goals

---

## 🛠️ Tech Stack
- Python
- pandas, numpy
- matplotlib, seaborn
- cohort analysis with `Period[M]`
- defensive type handling + robust joins

---

## 📁 Suggested Repository Structure
