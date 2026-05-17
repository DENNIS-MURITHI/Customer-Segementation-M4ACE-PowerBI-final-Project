# 🛍️ Customer Segmentation Using RFM Analysis
### m4ACE PowerBI-Data Analytics Track | Final Project

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Project Overview

This project presents a comprehensive **customer segmentation analysis** for a retail business using the **RFM (Recency, Frequency, Monetary)** framework. The analysis was conducted on a marketing campaign dataset of **2,237 customers**, covering their demographic profiles, purchasing behaviour, product preferences, and responses to six marketing campaigns.

The goal was to move beyond generic, one-size-fits-all marketing by segmenting the customer base into **six distinct, actionable groups** — enabling the business to target the right customers with the right message at the right time.

---

## 🎯 Objectives

- Clean, validate, and prepare a real-world marketing dataset with multiple data quality issues
- Engineer meaningful features including Age, TotalSpend, Frequency, and Customer Tenure
- Build and apply an RFM scoring model to segment customers into six strategic groups
- Analyse spending behaviour, product preferences, and purchase channel usage
- Develop an interactive 3-page Power BI dashboard communicating findings clearly
- Deliver data-driven strategic recommendations to improve campaign ROI

---

## 📊 Dashboard Preview

> **3-Page Interactive Power BI Dashboard**

| Page | Title | Key Visuals |
|------|-------|-------------|
| 📋 Page 1 | Customer Overview | KPI Cards, Education & Marital Distribution, Income by Education, Age Group Analysis |
| 🔄 Page 2 | RFM Segmentation | Segment Distribution, Avg Spend by Segment, Campaign Acceptance Rates, RFM Score Table |
| 💰 Page 3 | Spending & Channel Behaviour | Spend by Age Group, Product Category Breakdown, Channel Preference, Campaign Response by Age |

---

## 🔑 Key Findings

### 💡 Revenue Concentration
> Champions and Loyal Customers represent only **36% of the customer base** yet generate **~78% of total revenue** — confirming the Pareto principle in customer analytics.

### 💡 Surprising Spending Pattern
> Customers **under 30 years old** spend an average of **$832 per head** — the highest of any age group, significantly above the dataset average of $606. A high-value younger segment often overlooked.

### 💡 Recoverable Revenue
> **434 At Risk customers** with an average historical spend of $205 each represent approximately **$89,000 in recoverable revenue** if a targeted win-back campaign is executed.

### 💡 Campaign Performance
> Campaign 2 had only **1.3% acceptance** — nearly 6x below average. The Latest Campaign achieved **14.9%**, the highest ever, suggesting improving campaign sophistication over time.

### 💡 Product Dominance
> **Wines alone account for 50% of all revenue** ($680K out of $1.36M total). Wines + Meat combined drive **77.5%** of all product spend.

---

## 📈 RFM Segment Results

| Segment | Customers | % of Base | Avg Spend | RFM Score | Action |
|---------|-----------|-----------|-----------|-----------|--------|
| 🏆 Champions | 334 | 14.9% | $1,333 | 13–15 | Reward & Retain |
| ⭐ Loyal Customers | 471 | 21.1% | $1,071 | 11–12 | Upsell |
| 🌱 Potential Loyalists | 464 | 20.7% | $616 | 9–10 | Nurture |
| ⚠️ At Risk | 434 | 19.4% | $205 | 7–8 | Win Back Urgently |
| 😴 Hibernating | 362 | 16.2% | $67 | 5–6 | Re-engage |
| ❌ Lost | 172 | 7.7% | $37 | 3–4 | Minimal Budget |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Microsoft Excel** | Data preprocessing, date standardisation, format cleaning |
| **Power Query (M Language)** | Data transformation pipeline, null imputation, type enforcement |
| **DAX (Data Analysis Expressions)** | Calculated columns, RFM scoring logic, segmentation |
| **Power BI Desktop** | Interactive dashboard development and data visualisation |

---

## 🧹 Data Cleaning Summary

| Issue | Records Affected | Resolution |
|-------|-----------------|------------|
| Income null values | 24 rows (1.1%) | Imputed with **median ($51,876)** — chosen over mean due to high skewness (6.76) from $666,666 outlier |
| Marital Status junk entries (YOLO, Absurd) | 4 rows | Removed — data entry errors with no reliable true value |
| Education typo ('2n Cycle') | 203 rows | Corrected to '2nd Cycle' |
| Mixed date formats (DD-MM-YYYY vs MM/DD/YYYY) | ~40% of rows | Standardised to DD/MM/YYYY in Excel, enforced as Date in Power BI using UK locale |
| Age outliers (born 1893 — age 131) | 3 rows | Removed rows where Year_Birth < 1924 |

**Final clean dataset: 2,237 customers | 29 original + 6 engineered columns = 35 total**

---

## ⚙️ Feature Engineering (DAX)

```dax
-- Age
Age = 2024 - marketing_campaign[Year_Birth]

-- Total Spend (Monetary RFM metric)
TotalSpend = 
    marketing_campaign[MntWines] + marketing_campaign[MntFruits] + 
    marketing_campaign[MntMeatProducts] + marketing_campaign[MntFishProducts] + 
    marketing_campaign[MntSweetProducts] + marketing_campaign[MntGoldProds]

-- Purchase Frequency (Frequency RFM metric)
Frequency = 
    marketing_campaign[NumWebPurchases] + 
    marketing_campaign[NumCatalogPurchases] + 
    marketing_campaign[NumStorePurchases]

-- Age Grouping
AgeGroup = 
    SWITCH(TRUE(),
        marketing_campaign[Age] < 30, "Under 30",
        marketing_campaign[Age] < 40, "30-40",
        marketing_campaign[Age] < 50, "40-50",
        marketing_campaign[Age] < 60, "50-60",
        "60+"
    )

-- RFM Segmentation
Segment = 
    SWITCH(TRUE(),
        marketing_campaign[RFM_Total] >= 13, "Champions",
        marketing_campaign[RFM_Total] >= 11, "Loyal Customers",
        marketing_campaign[RFM_Total] >= 9,  "Potential Loyalists",
        marketing_campaign[RFM_Total] >= 7,  "At Risk",
        marketing_campaign[RFM_Total] >= 5,  "Hibernating",
        "Lost"
    )
```

---

## 📁 Repository Structure

```
📦 customer-segmentation-rfm-analysis
 ┣ 📂 data
 ┃ ┣ 📄 marketing_campaign.csv          # Raw dataset
 ┃ ┗ 📄 marketing_campaign_clean.xlsx   # Cleaned dataset
 ┣ 📂 dashboard
 ┃ ┗ 📄 Dennis_Murithi_RFM_Dashboard.pbix   # Power BI dashboard file
 ┣ 📂 report
 ┃ ┗ 📄 Dennis_Murithi_RFM_Project_Report.docx  # Full project report
 ┣ 📄 README.md
```

---

## 🚀 How to Use

1. **Clone the repository**
```bash
git clone https://github.com/DENNIS-MURITHI/customer-segmentation-rfm-analysis.git
```

2. **Open the dashboard**
   - Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
   - Open `Dennis_Murithi_RFM_Dashboard.pbix`
   - Interact with slicers and navigation buttons across all 3 pages

3. **Review the data**
   - Open `marketing_campaign_clean.xlsx` to explore the cleaned dataset
   - All engineered columns are documented in the project report

---

## 📌 Strategic Recommendations Summary

| Segment | Immediate Action | Expected Impact |
|---------|-----------------|-----------------|
| Champions | Launch VIP loyalty programme, request referrals | Protect $445K revenue base |
| Loyal Customers | Upsell wines & meat, loyalty card | Increase avg spend by 15–20% |
| Potential Loyalists | Personalised email sequences, category trials | Convert 30% to Loyal Customers |
| At Risk | Win-back campaign with time-limited offer | Recover ~$44K in revenue |
| Hibernating | Low-cost reactivation email | 20–30% reactivation expected |
| Lost | One final email then suppress | Protect email sender reputation |

---

## 📚 Dataset

- **Source:** Marketing Campaign Dataset — HNG Internship Data Analytics Track
- **Records:** 2,240 raw / 2,237 after cleaning
- **Period:** Customer enrollment 2012–2014
- **Variables:** 29 original + 6 engineered = 35 total

---

## 👤 Author

**Dennis Murithi Muthuri**
- 🔗 [LinkedIn](https://linkedin.com/in/dennis-muthuri)
- 💻 [GitHub](https://github.com/DENNIS-MURITHI)
- 📧 denmurithi@gmail.com

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

> *"Without data you're just another person with an opinion." — W. Edwards Deming*

