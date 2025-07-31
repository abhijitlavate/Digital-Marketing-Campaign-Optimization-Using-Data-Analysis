# Digital-Marketing-Campaign-Optimization-Using-Data-Analysis
# 📈 Project: Digital Marketing Campaign Optimization Using Data Analysis

## 🧠 Problem Statement

As a **Data Analyst** at a **Digital Marketing Agency**, the objective was to **maximize return on investment (ROI)** from advertising campaigns across platforms. Using diverse datasets containing ad formats, impressions, clicks, conversions, costs, and sales, the project aimed to:

- Evaluate campaign performance
- Optimize ad budgets
- Improve targeting and platform strategies

---

## 🧩 Key Features

- **Temporal Features**: `Date`, `Month`, `Year` – Trend and seasonality analysis
- **Ad Campaign**: Campaign identifiers for segmentation
- **Ad Formats**: `Display Ads`, `Overlay Ads`, `Skippable Ads`, `Non-skippable Ads`, `Bumper Ads`
- **Platforms**: e.g., Google Ads, Facebook Ads, Twitter Ads
- **User Engagement**: `Avg Pages Visited`, `AVG Time on Site (mins)`
- **Performance Metrics**: `Impressions`, `Clicks`, `Conversions`, `Quantity Sold`
- **Financials**: 
  - Cost Metrics: `CPM`, `CPC`, `Unit Cost Price`, `Final Cost Price`
  - Revenue Metrics: `Unit Sale Price`, `Final Sale Price`, `Sales Target`, `Ad Budget`

---

## 🎯 Analysis Objectives

1. **📊 Campaign Performance Analysis** – Analyze impressions, clicks, conversions, ROI
2. **🔄 Platform Comparison** – Find high-performing platforms and reduce budget waste
3. **📺 Ad Format Optimization** – Evaluate and improve user engagement by format
4. **💰 Budget Allocation Optimization** – Maximize ROI within constraints
5. **📅 Temporal Analysis** – Understand trends and seasonality
6. **🧭 User Engagement Analysis** – Use behavioral metrics to improve traffic quality
7. **💸 Cost Efficiency Analysis** – Identify ways to lower CPM and CPC

---

## 🧮 DAX Measures

```DAX
-- Conversion vs CPC
Conv vs CPC = 
VAR Conv_CPC = DIVIDE([Total Clicks], [Total Impresion])
RETURN 1 - Conv_CPC

-- Conversion / CPC
Conv/CPC = DIVIDE([Total Conversions], [Total Clicks])

-- CPC vs CPM
CPC vs CPM = 
VAR CPC_CPM = DIVIDE([Total Clicks],[Total Impresion])
RETURN 1 - CPC_CPM

-- CPC / CPM
CPC/CPM = DIVIDE([Total Clicks], [Total Impresion])

-- Total Ad Budget CY
Total Ad Budget CY = SUMX('Ad Budget', 'Ad Budget'[Ad Budget])

-- Total Ads Cost CY
Total Ads Cost CY = [Total CPC Cy] + [Total CPM CY]

-- Total Clicks
Total Clicks = SUMX(Data, Data[Clicks])

-- Total Conversions
Total Conversions = SUMX(Data, Data[Conversions])

-- Total Conversion LY
Total Conv LY = CALCULATE([Total Conversions], SAMEPERIODLASTYEAR('Calender'[Date]))

-- Total Cost CY
Total Cost CY = SUMX(Data, Data[Final Cost Price])

-- Total CPC CY
Total CPC Cy = 
VAR TotalCost = SUMX('Click Cost', 'Click Cost'[Cost Per Click (CPC)])
RETURN TotalCost * [Total Clicks]

-- Total CPC LY
Total CPC Last_Year = CALCULATE([Total CPC Cy], SAMEPERIODLASTYEAR('Calender'[Date]))

-- Total CPM CY
Total CPM CY = 
VAR By1000Impresions = DIVIDE([Total Impresion], 1000)
VAR CostPer1000Impresion = SUMX('Impression Cost', 'Impression Cost'[Cost Per 1000 Impression (CPM)])
RETURN By1000Impresions * CostPer1000Impresion

-- Total CPM LY
Total CPM LY = CALCULATE([Total CPM CY], SAMEPERIODLASTYEAR('Calender'[Date]))

-- Total Impressions
Total Impresion = SUMX(Data, Data[Impressions])

-- Total Profit %
Total Profit % CY = DIVIDE([Total Profit CY], [Total Cost CY])

-- Total Profit
Total Profit CY = [Total Sales Cy] - [Total Cost CY] - [Total Ads Cost CY]

-- Quantity Sold CY
Total Quantites Sold CY = SUMX(Data, Data[Quantity Sold])

-- Total Sales CY
Total Sales Cy = SUMX(Data, Data[Final Sale Price])

-- Total Sales LY
Total Sales LY = CALCULATE([Total Sales Cy], SAMEPERIODLASTYEAR('Calender'[Date]))

-- Total Sales YoY%
Total Sales YoY% = 
VAR CYminusLY = ([Total Sales Cy] - [Total Sales LY])
RETURN DIVIDE(CYminusLY, [Total Sales LY])

-- Sales Target CY
Total target Sales CY = SUMX('Sales Target', 'Sales Target'[Sales Target])
