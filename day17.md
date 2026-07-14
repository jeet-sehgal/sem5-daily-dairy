# Daily Diary – Day 17
`Date : 11/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** Power BI – Basic Charts (Bar, Column, Line, Area, Pie, Donut, Card, KPI, Table, Matrix, Scatter, Treemap, Slicer)

---

## 1. How to Add Any Chart (General Steps)

```
1. Open Power BI Desktop
2. Import your data (Get Data → CSV / Excel)
3. Go to Report View (canvas)
4. Click a chart type from the Visualizations panel
5. A blank visual appears on canvas
6. Drag columns from Fields panel into the chart's field wells
7. Resize and position the chart on canvas
8. Format using the Format Visual panel (paintbrush icon)
```

---

## 2. Bar Chart (Clustered & Stacked)

**When to use:** Compare values across **categories** (horizontal bars).

### Clustered Bar Chart
```
Fields to fill:
- Y-axis  → Category (e.g., Product Name, City, Department)
- X-axis  → Values   (e.g., Sales, Revenue, Count)
- Legend  → (optional) to split bars by another category

Example:
Y-axis  = City
X-axis  = Total Sales
→ Shows which city has highest sales as horizontal bars
```

### Stacked Bar Chart
```
Fields to fill:
- Y-axis  → Category  (e.g., Department)
- X-axis  → Values    (e.g., Total Salary)
- Legend  → Sub-category (e.g., Gender)

→ Each bar is divided into segments showing proportion of each sub-category
```

**Key Formatting Options:**
```
Format Visual → Visual tab:
- Bars → Colors → change each bar color
- Data Labels → On (shows values on each bar)
- Title → rename chart title
- X-axis / Y-axis → show/hide, change font size
```

---

## 3. Column Chart (Clustered & Stacked)

**When to use:** Same as Bar Chart but with **vertical bars** — best for **time-based comparisons**.

### Clustered Column Chart
```
Fields to fill:
- X-axis → Time / Category (e.g., Month, Quarter, Year)
- Y-axis → Values (e.g., Revenue, Units Sold)
- Legend → (optional) sub-category

Example:
X-axis = Month
Y-axis = Total Sales
→ Shows month-wise sales as vertical bars
```

### Stacked Column Chart
```
Fields to fill:
- X-axis → Category (e.g., Quarter)
- Y-axis → Values   (e.g., Sales)
- Legend → Sub-category (e.g., Region)

→ Each column stacked to show total, divided by region
```

### 100% Stacked Column
```
→ All bars the same height (100%)
→ Shows proportion/percentage of each sub-category
→ Useful for comparing shares rather than absolute values
```

---

## 4. Line Chart

**When to use:** Show **trends over time** — most useful with date/time on X-axis.

```
Fields to fill:
- X-axis   → Date / Time column (e.g., Date, Month, Year)
- Y-axis   → Numeric value (e.g., Sales, Temperature, Profit)
- Legend   → (optional) multiple lines for different categories
- Secondary Y-axis → (optional) second scale

Example:
X-axis = Order Date (Month level)
Y-axis = Total Revenue
→ Shows how revenue changes month by month as a line
```

**Key Formatting Options:**
```
- Lines → Stroke width (make line thicker)
- Markers → On (shows dots at each data point)
- Data Labels → On (shows values above each point)
- Trend Line → Analytics tab → add trend line
- Forecast → Analytics tab → predict future trend
```

---

## 5. Area Chart & Stacked Area Chart

**When to use:** Like a line chart but with the **area below the line filled** — shows volume over time.

```
Fields to fill:
- X-axis  → Date/Time
- Y-axis  → Numeric value
- Legend  → Category (for stacked area)

Example:
X-axis = Month
Y-axis = Revenue
Legend = Region (North, South, East, West)
→ Each region stacked as a filled area showing total volume
```

---

## 6. Pie Chart

**When to use:** Show **parts of a whole** (proportions/percentages) — best with **5 or fewer categories**.

```
Fields to fill:
- Legend → Category (e.g., Product Category, Region)
- Values → Numeric value (e.g., Sales, Count)

Example:
Legend = Category (Electronics, Clothing, Food)
Values = Total Sales
→ Each slice shows what % of total each category contributes
```

**Key Formatting Options:**
```
- Slices → Colors → change each slice color manually
- Detail Labels → Label contents → choose "Category, Percent"
- Inner Radius → 0 = Pie, >0 = Donut
- Legend → show/hide category names
```

---

## 7. Donut Chart

**When to use:** Same as Pie Chart but with a **hole in the middle** — cleaner look, can display a central metric.

```
Fields to fill:
- Legend → Category
- Values → Numeric value

Example:
Legend = Payment Method (Cash, Card, UPI)
Values = Transaction Count
→ Donut shows share of each payment method
```

---

## 8. Card Visual

**When to use:** Display a **single important number** (KPI) — like Total Sales, Total Customers, Average Revenue.

```
Fields to fill:
- Fields → one numeric column (e.g., Sales, Profit, Count)

Power BI automatically aggregates (SUM, COUNT, AVG)

Example:
Fields = Total Revenue (SUM)
→ Shows a big bold number like "₹ 45,23,000"
```

**Key Formatting Options:**
```
- Callout Value → font size, color, bold
- Category Label → rename the label below the number
- Background → add background color to card
```

### Multiple Cards Side by Side
```
Steps:
1. Create first Card → drag "Total Sales"
2. Duplicate (Ctrl+D) → change field to "Total Orders"
3. Duplicate again → change to "Average Order Value"
4. Arrange side by side on canvas

→ Creates a KPI row at the top of dashboard
```

---

## 9. KPI Visual

**When to use:** Shows progress toward a **target/goal** — value vs target + trend indicator.

```
Fields to fill:
- Value         → Actual value (e.g., This Month Sales)
- Target value  → Goal/Target (e.g., Sales Target)
- Trend axis    → Time (e.g., Month)

→ Shows green ▲ if above target, red ▼ if below target
```

---

## 10. Table Visual

**When to use:** Display **raw/detailed data** in rows and columns — like a spreadsheet inside the report.

```
Fields to fill:
- Columns → drag any columns you want to show
           (e.g., Name, Region, Sales, Profit, Date)

Example:
Columns = Order ID, Customer Name, Product, Sales, Profit, Order Date
→ Shows a scrollable table of all records
```

**Key Formatting Options:**
```
- Style presets → choose Bold Header, Minimal, etc.
- Column headers → font, background color, text color
- Values → alternate row color (makes it easier to read)
- Totals → show/hide total row at bottom
- Conditional Formatting → color cells based on value
  (Home → Format Visual → Cells → Conditional Formatting → Color Scale)
```

---

## 11. Matrix Visual

**When to use:** Like a **Pivot Table** — rows, columns, and values for cross-tabulation.

```
Fields to fill:
- Rows    → e.g., Product Category
- Columns → e.g., Region / Year
- Values  → e.g., Total Sales

Example:
Rows    = Product (Laptop, Mobile, TV)
Columns = Quarter (Q1, Q2, Q3, Q4)
Values  = Total Sales
→ Shows sales of each product per quarter in a grid

Can expand/collapse rows if hierarchy is added
```

---

## 12. Scatter Chart

**When to use:** Show **relationship/correlation** between two numeric variables — identifies patterns, clusters, outliers.

```
Fields to fill:
- X-axis   → First numeric column (e.g., Marketing Spend)
- Y-axis   → Second numeric column (e.g., Revenue)
- Values   → Category (e.g., Product) — each dot represents one category
- Size     → (optional) third numeric to set dot size

Example:
X-axis = Advertising Budget
Y-axis = Total Sales
Values = Store Name
→ Each dot = one store, shows if more advertising → more sales
```

---

## 13. Treemap

**When to use:** Show **hierarchical data** and part-to-whole relationships using nested rectangles. Size of rectangle = value.

```
Fields to fill:
- Category → Main group (e.g., Region)
- Details  → Sub-group (e.g., City)
- Values   → Numeric value (e.g., Sales)

Example:
Category = Category (Electronics, Clothing)
Details  = Sub-Category (Laptop, Mobile, T-Shirt)
Values   = Total Sales
→ Bigger rectangle = more sales
→ Color grouped by Category
```

---

## 14. Slicer (Interactive Filter)

**When to use:** Add **interactive filters** that users can click to filter all other visuals on the page.

```
Fields to fill:
- Field → any column you want to filter by
         (e.g., Year, Region, Category, Gender)

Slicer styles (Format → Visual → Slicer settings → Style):
- List    → checkboxes for each value
- Dropdown → compact dropdown menu
- Between  → range slider (for dates or numbers)
- Tile    → clickable button tiles
- Relative → "last 7 days", "this month" (for dates)

Example 1: Year Slicer
Field = Year → user clicks 2023 → all charts filter to 2023

Example 2: Region Slicer
Field = Region → user selects "North" → all charts show North data only

Multi-select: Hold Ctrl + Click to select multiple values
```

---

## 15. Chart Interactions

**Theory:** By default, clicking on one visual **filters** all other visuals on the same page. You can customize this.

```
Steps to change interactions:
1. Click on a visual (e.g., bar chart)
2. Go to Format tab in Ribbon
3. Click "Edit Interactions"
4. Small icons appear on all other visuals:
   - Filter icon (funnel)   → clicking filters that visual
   - Highlight icon (chart) → clicking highlights in that visual
   - None icon (circle/X)   → clicking has no effect on that visual
5. Click the icon you want for each visual
6. Click "Edit Interactions" again to turn off edit mode
```

---

## 16. Drill Down / Drill Through

**Theory:** If you add a **hierarchy** (e.g., Year → Quarter → Month), you can click into data at different levels.

```
Example hierarchy: Date → Year → Quarter → Month → Day

Enable drill down:
1. Add hierarchy to X-axis (Year, Quarter, Month)
2. Click the "Drill Down" arrow icon on the visual
3. Click a bar → zooms into next level
4. Click "Drill Up" to go back

Drill Through:
1. Create a new page
2. Add "Drill Through" field (e.g., Product Name)
3. On main page → right-click a bar → Drill Through → Page 2
4. Page 2 filters to that specific product automatically
```

---

## 17. Quick Reference – Charts at a Glance

| Chart | Best For | Key Fields |
|---|---|---|
| Bar Chart | Category comparison (horizontal) | Y-axis (Category), X-axis (Value) |
| Column Chart | Time-based comparison (vertical) | X-axis (Date), Y-axis (Value) |
| Line Chart | Trends over time | X-axis (Date), Y-axis (Value) |
| Area Chart | Volume over time | X-axis (Date), Y-axis (Value) |
| Pie Chart | Proportions (≤5 categories) | Legend (Category), Values |
| Donut Chart | Proportions (cleaner look) | Legend (Category), Values |
| Card | Single KPI number | Fields (one value) |
| KPI | Actual vs Target | Value, Target, Trend Axis |
| Table | Raw detail data | Any columns |
| Matrix | Pivot-style cross-tab | Rows, Columns, Values |
| Scatter | Correlation between 2 numbers | X-axis, Y-axis, Values |
| Treemap | Hierarchy + part-to-whole | Category, Details, Values |
| Slicer | Interactive filter | Any column |

---

## Summary of Day 17
Today I learned all **basic chart types in Power BI** and when to use each one. I practiced **Bar and Column charts** (clustered, stacked, 100%), **Line and Area charts** for trends, **Pie and Donut charts** for proportions, **Card and KPI visuals** for single metrics, **Table and Matrix** for detailed/pivot data, **Scatter charts** for correlations, **Treemaps** for hierarchical data, and **Slicers** for interactive filtering. I also learned how to customize **chart interactions**, use **drill down** through date hierarchies, and format each visual using the Format panel.

**Practice Tasks for Tomorrow:**
1. Load a sales dataset and create a clustered bar chart of sales by product category.
2. Plot a line chart showing monthly revenue trend with markers and a trend line enabled.
3. Create a KPI card showing total revenue with a target value.
4. Build a matrix showing product sales across different quarters and regions.
5. Add 3 slicers (Year, Region, Category) and observe how they filter all visuals together.