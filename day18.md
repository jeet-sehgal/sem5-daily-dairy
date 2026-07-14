# Daily Diary – Day 18
`Date : 13/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** Power BI – Building a Complete Practice Dashboard (Sales Dashboard) from Scratch

---

## 1. What is a Dashboard? (Brief Theory)
A **Dashboard** is a single-page visual report that displays the most important KPIs and insights from your data at a glance. A good dashboard answers:
- **What happened?** (descriptive)
- **How much?** (metrics)
- **Where?** (geography)
- **Which category?** (breakdown)

**A good dashboard has:**
- KPI Cards at the top (summary numbers)
- Charts in the middle (trends, comparisons)
- Filters/Slicers on the side or top
- Clean layout, consistent colors, no clutter

---

## 2. Dataset Used – Sales Data

**Columns in the dataset:**
```
Order_ID | Customer_Name | Category | Sub_Category | Region |
State | Order_Date | Ship_Date | Sales | Profit | Quantity | Discount
```

**Import steps:**
```
1. Open Power BI Desktop
2. Home → Get Data → Text/CSV
3. Select your sales CSV file
4. Preview data → Click "Transform Data"
5. In Power Query:
   - Check all column data types
   - Order_Date → change to Date type
   - Sales, Profit → Decimal Number
   - Quantity → Whole Number
   - Click Close & Apply
```

---

## 3. Data Cleaning in Power Query

```
Open Power Query Editor → check each column:

Step 1: Remove blank/null rows
  Home → Remove Rows → Remove Blank Rows

Step 2: Fix data types
  Order_Date  → Date
  Ship_Date   → Date
  Sales       → Decimal Number
  Profit      → Decimal Number
  Quantity    → Whole Number
  Discount    → Decimal Number

Step 3: Add a new column "Profit Margin %"
  Add Column → Custom Column
  Name: Profit Margin %
  Formula: = [Profit] / [Sales] * 100

Step 4: Extract Month & Year from Order_Date
  Select Order_Date column
  Add Column → Date → Month → Month Name  (new column: Month Name)
  Add Column → Date → Year                (new column: Year)

Step 5: Close & Apply
```

---

## 4. DAX Measures Created

**Go to Table View → Right-click table → New Measure**

```DAX
-- 1. Total Sales
Total Sales = SUM('Sales'[Sales])

-- 2. Total Profit
Total Profit = SUM('Sales'[Profit])

-- 3. Total Orders
Total Orders = COUNT('Sales'[Order_ID])

-- 4. Total Quantity
Total Quantity = SUM('Sales'[Quantity])

-- 5. Profit Margin %
Profit Margin % = DIVIDE(SUM('Sales'[Profit]), SUM('Sales'[Sales])) * 100

-- 6. Average Order Value
Avg Order Value = DIVIDE(SUM('Sales'[Sales]), COUNT('Sales'[Order_ID]))

-- 7. Total Customers
Total Customers = DISTINCTCOUNT('Sales'[Customer_Name])

-- 8. Return on Sales
ROS = DIVIDE([Total Profit], [Total Sales])
```

---

## 5. Dashboard Layout Plan

```
┌──────────────────────────────────────────────────────────────────┐
│  TITLE: Sales Performance Dashboard                              │
├────────────┬────────────┬────────────┬────────────┬─────────────┤
│  CARD:     │  CARD:     │  CARD:     │  CARD:     │  CARD:      │
│  Total     │  Total     │  Total     │  Profit    │  Total      │
│  Sales     │  Profit    │  Orders    │  Margin %  │  Customers  │
├────────────┴────────────┼───────────────────────────────────────┤
│                         │                                        │
│  LINE CHART:            │  BAR CHART:                           │
│  Monthly Sales Trend    │  Sales by Category                    │
│                         │                                        │
├─────────────────────────┼───────────────────────────────────────┤
│                         │                                        │
│  DONUT CHART:           │  TABLE:                               │
│  Sales by Region        │  Top 10 Customers by Sales            │
│                         │                                        │
├─────────────────────────┴───────────────────────────────────────┤
│  SLICER: Year  │  SLICER: Region  │  SLICER: Category          │
└──────────────────────────────────────────────────────────────────┘
```

---

## 6. Step-by-Step Dashboard Building

### Step 1 – Page Setup
```
1. Right-click page tab (Page 1) → Rename → "Sales Dashboard"
2. View → Canvas Settings:
   - Type: Custom
   - Width: 1280, Height: 720
3. View → Themes → choose a theme
   (e.g., Innovation, Executive, Accessible Default)
4. Format → Canvas Background → set light grey (#F4F4F4)
```

---

### Step 2 – Add Title Text Box
```
1. Insert → Text Box
2. Type: "Sales Performance Dashboard"
3. Font size: 24, Bold, Dark color
4. Place at the very top of canvas
5. Format → Background → White with slight border
```

---

### Step 3 – KPI Cards Row (Top)
```
Create 5 Cards side by side:

Card 1: Total Sales
  - Click Card visual
  - Fields → drag [Total Sales] measure
  - Format → Callout Value → font 28, Bold, Dark Blue
  - Format → Category Label → rename "Total Sales"
  - Format → Background → White

Card 2: Total Profit
  - Same steps → drag [Total Profit]
  - Label → "Total Profit"

Card 3: Total Orders
  - Drag [Total Orders]
  - Label → "Total Orders"

Card 4: Profit Margin %
  - Drag [Profit Margin %]
  - Label → "Profit Margin %"

Card 5: Total Customers
  - Drag [Total Customers]
  - Label → "Total Customers"

Arrange all 5 in a row → select all → Format → Align → Top
```

---

### Step 4 – Line Chart (Monthly Sales Trend)
```
1. Click Line Chart visual
2. Fields:
   X-axis  → Month Name (from Order_Date)
   Y-axis  → [Total Sales] measure
3. Format:
   - Title → "Monthly Sales Trend"
   - Lines → Stroke Width → 3
   - Markers → On
   - Data Labels → On
   - X-axis → sort months correctly:
     (Right-click Month Name column → Sort by Column → Month Number)
```

---

### Step 5 – Bar Chart (Sales by Category)
```
1. Click Clustered Bar Chart
2. Fields:
   Y-axis → Category
   X-axis → [Total Sales]
3. Format:
   - Title → "Sales by Category"
   - Bars → Colors → different color per bar:
     Format Visual → Colors → "Show All" → toggle ON
   - Data Labels → On
   - Sort → Sort descending by Total Sales
     (Click "..." on visual → Sort by → Total Sales → Descending)
```

---

### Step 6 – Donut Chart (Sales by Region)
```
1. Click Donut Chart visual
2. Fields:
   Legend → Region
   Values → [Total Sales]
3. Format:
   - Title → "Sales by Region"
   - Detail Labels → Label contents → "Category, Percent"
   - Slices → change colors for each region
   - Legend → Position → Right
```

---

### Step 7 – Table (Top 10 Customers)
```
1. Click Table visual
2. Fields → drag:
   - Customer_Name
   - [Total Sales]
   - [Total Profit]
   - [Total Orders]
3. Filter to Top 10:
   - Go to Filters panel (right side)
   - Drag Customer_Name to "Filters on this visual"
   - Filter type → Top N
   - Show Top → 10
   - By value → [Total Sales]
   - Click Apply Filter
4. Format:
   - Title → "Top 10 Customers"
   - Style presets → Bold Header
   - Totals row → On
   - Conditional Formatting:
     Select Sales column → Format → Conditional Formatting
     → Data Bars → On (shows mini bar inside cell)
```

---

### Step 8 – Add Slicers (Filters)
```
Slicer 1: Year
  - Click Slicer visual
  - Field → Year
  - Format → Slicer Settings → Style → Tile
  - Place at bottom left

Slicer 2: Region
  - Click Slicer visual
  - Field → Region
  - Style → Tile
  - Place at bottom center

Slicer 3: Category
  - Click Slicer visual
  - Field → Category
  - Style → Dropdown
  - Place at bottom right

Test slicers:
  Click "2023" in Year slicer → all visuals update to 2023 data ✓
  Click "West" in Region slicer → all visuals filter to West ✓
```

---

### Step 9 – Final Formatting & Alignment
```
Consistency rules:
- All card backgrounds → White (#FFFFFF)
- All chart backgrounds → White with soft shadow
- All titles → same font, same size (14pt), same color (Dark Grey)
- Canvas background → Light grey (#F5F5F5)
- Same border style on all visuals

Alignment:
1. Select all cards → Format → Align → Distribute Horizontally
2. Select charts in row 2 → Align → Top + same height
3. Select all → Format → Align → Align Left / Center

Adding borders to visuals:
  Format Visual → General tab → Effects → Border → On
  Color → Light grey, Rounded corners → 5px
```

---

## 7. Adding a Second Page – Product Analysis

```
1. Click + at the bottom to add a new page
2. Rename → "Product Analysis"

Add on this page:
  Visual 1: Treemap → Category → Sub_Category → [Total Sales]
             Title: "Sales by Sub-Category"

  Visual 2: Scatter Chart
             X-axis → [Total Sales]
             Y-axis → [Total Profit]
             Values → Sub_Category
             Title: "Sales vs Profit by Sub-Category"

  Visual 3: Clustered Column Chart
             X-axis → Sub_Category
             Y-axis → [Total Quantity]
             Title: "Units Sold by Sub-Category"
             Sort descending

  Visual 4: Card → [Profit Margin %]
             Card → [Avg Order Value]

  Slicer → Category (filter whole page)
```

---

## 8. Drill Through Setup

```
Steps:
1. Create a 3rd page → rename "Customer Detail"
2. Add a Table with full customer info:
   Fields → Customer_Name, Region, State, Sales, Profit, Quantity, Order_Date

3. In Filters panel on this page:
   Drag Customer_Name to "Drill Through" field well

4. Go back to Page 1 (Sales Dashboard)
5. Right-click any customer name in the Top 10 Table
   → Drill Through → Customer Detail
6. Page 3 opens filtered to just that customer ✓
```

---

## 9. Final Dashboard Checklist

```
✅ Title clearly describes the dashboard
✅ KPI Cards row at the top with key numbers
✅ At least one trend chart (line chart with time)
✅ At least one comparison chart (bar/column)
✅ At least one proportion chart (pie/donut)
✅ Slicers for Year, Region, and Category
✅ All visuals have clear titles
✅ Data labels visible on charts
✅ Consistent color theme throughout
✅ No overlapping visuals
✅ All axes labeled correctly
✅ Slicer interactions tested (click and verify)
✅ Second page with deeper product analysis
✅ Drill through working on customer table
✅ Saved as .pbix file
```

---

## 10. Saving & Publishing

```
Save file:
  File → Save As → Sales_Dashboard.pbix

Publish to Power BI Service:
  Home → Publish → My Workspace → Select
  → Opens in browser at app.powerbi.com

Pin to Dashboard (in Service):
  Open report in browser
  Hover any visual → click Pin icon 📌
  → Create new dashboard or add to existing
```

---

## Summary of Day 18
Today I built a **complete Sales Dashboard in Power BI** from scratch. I started with importing and cleaning data in **Power Query** (fixing data types, adding custom columns, extracting Month/Year from date), created **8 DAX measures** (Total Sales, Profit, Orders, Customers, Profit Margin %, Avg Order Value), designed the **layout plan** before building, then added **5 KPI Cards**, a **Line Chart** for monthly trends, a **Bar Chart** for category comparison, a **Donut Chart** for region split, a **Top 10 Customers Table** with conditional formatting, and **3 Slicers** (Year, Region, Category). I also built a **second page** for product analysis with a Treemap, Scatter, and Column chart, set up **Drill Through** to a Customer Detail page, applied **consistent formatting**, tested all slicer interactions, and published the report.

**Practice Tasks for Tomorrow:**
1. Build a complete HR Dashboard showing headcount, avg salary, department breakdown, and attrition rate.
2. Add a Gauge visual showing actual profit vs target profit.
3. Create a map visual showing sales distribution by State/City.
4. Apply conditional formatting on a Matrix to highlight top-performing cells in green and bottom in red.
5. Set up a Drill Through from a product bar chart to a detailed product page.