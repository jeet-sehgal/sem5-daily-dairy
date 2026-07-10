# Daily Diary – Day 16
`Date : 10/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** Power BI – Introduction, Interface, Data Import, Power Query, Relationships, Visualizations, DAX Basics, Dashboard

---

## 1. What is Power BI? (Brief Theory)
**Power BI** is a **Business Intelligence (BI)** tool by Microsoft used to connect to data sources, transform data, create interactive visualizations, and share dashboards and reports. It turns raw data into meaningful insights without writing much code.

**Three versions:**
| Version | Use |
|---|---|
| Power BI Desktop | Free, installed on PC — for creating reports |
| Power BI Service | Cloud-based (browser) — for sharing reports |
| Power BI Mobile | Mobile app — for viewing reports |

**Where to download:** [https://powerbi.microsoft.com](https://powerbi.microsoft.com) → Download → Power BI Desktop (Free)

---

## 2. Power BI Interface – Key Areas

```
┌─────────────────────────────────────────────────────────┐
│  RIBBON (Home, Insert, Modeling, View, Help)            │
├───────────┬─────────────────────────────┬───────────────┤
│           │                             │               │
│  PAGES    │     CANVAS (Report View)    │  VISUALIZATIONS│
│  PANEL    │     (drag & drop charts     │  PANEL        │
│  (tabs)   │      and visuals here)      │  (chart types)│
│           │                             │               │
│           │                             │  FIELDS PANEL │
│           │                             │  (columns from│
│           │                             │   your tables)│
└───────────┴─────────────────────────────┴───────────────┘
```

**Three Views (Left panel icons):**
- **Report View** — Canvas where you design dashboards
- **Table View** — View raw data tables
- **Model View** — See and set relationships between tables

---

## 3. Connecting to Data Sources

**Home → Get Data → Choose Source**

Power BI can connect to:

| Source Type | Examples |
|---|---|
| Files | Excel (.xlsx), CSV, PDF, JSON |
| Databases | SQL Server, MySQL, PostgreSQL |
| Online Services | SharePoint, Google Analytics, Salesforce |
| Other | Web (URL), Python, R scripts |

```
Steps to import a CSV/Excel file:
1. Open Power BI Desktop
2. Click "Get Data" → "Text/CSV" or "Excel Workbook"
3. Browse and select your file
4. Preview appears → Click "Load" (direct) or "Transform Data" (to clean first)
```

---

## 4. Power Query Editor (Data Transformation)

**Theory:** Power Query is Power BI's built-in data cleaning and transformation tool. Click **"Transform Data"** to open it.

### Common Transformations

```
Home → Transform Data → Power Query Editor opens
```

| Operation | How To |
|---|---|
| Remove columns | Right-click column → Remove |
| Rename column | Double-click column header |
| Change data type | Click data type icon on column header |
| Remove duplicates | Home → Remove Rows → Remove Duplicates |
| Remove blank rows | Home → Remove Rows → Remove Blank Rows |
| Filter rows | Click dropdown arrow on column header |
| Split column | Transform → Split Column → By Delimiter |
| Add custom column | Add Column → Custom Column → write formula |
| Replace values | Transform → Replace Values |
| Trim whitespace | Transform → Format → Trim |

```
After all transformations:
Click "Close & Apply" (top left) to load cleaned data into Power BI
```

---

## 5. Data Types in Power BI

**Always check and fix data types first — wrong types cause wrong calculations!**

| Data Type | Examples | Icon |
|---|---|---|
| Whole Number | 1, 50, 100 | 123 |
| Decimal Number | 3.14, 99.99 | 1.2 |
| Text | "Bhawna", "Delhi" | ABC |
| Date | 01/01/2024 | 📅 |
| Date/Time | 01/01/2024 10:30 AM | 📅🕐 |
| Boolean | True / False | ✓ |

---

## 6. Relationships Between Tables (Data Model)

**Theory:** When you have more than one table, you link them using a **common column** (like a primary key). This is done in **Model View**.

```
Example:
  Table 1: Students (Student_ID, Name, Class)
  Table 2: Marks    (Student_ID, Subject, Score)

  Relationship: Students[Student_ID] → Marks[Student_ID]
  (One student → many marks = One-to-Many relationship)
```

**Steps to create a relationship:**
```
1. Go to Model View (left panel, third icon)
2. Drag Student_ID from Students table
3. Drop it on Student_ID in Marks table
4. A line appears connecting the two tables
5. Double-click line to edit (cardinality, direction)
```

**Cardinality types:**
| Type | Meaning |
|---|---|
| One-to-Many (1:*) | Most common — one ID → many rows |
| One-to-One (1:1) | Each ID unique in both tables |
| Many-to-Many (*:*) | Use carefully — needs bridge table |

---

## 7. Visualizations (Charts)

**Theory:** Drag and drop columns into the Visualizations panel to create charts on the canvas.

### Common Chart Types

| Visual | Use Case | Fields Needed |
|---|---|---|
| Bar Chart | Compare categories | Axis + Values |
| Column Chart | Compare over time | Axis + Values |
| Line Chart | Trends over time | Axis + Values |
| Pie/Donut Chart | Show proportions | Legend + Values |
| Card | Show single number | Fields (one value) |
| Table | Tabular view | Multiple columns |
| Matrix | Pivot-style table | Rows + Columns + Values |
| Map | Geographic data | Location + Size |
| Gauge | KPI progress | Value + Min/Max |
| Slicer | Interactive filter | Any column |

### Steps to create a Bar Chart
```
1. Click "Clustered Bar Chart" in Visualizations panel
2. A blank chart appears on canvas
3. Drag "Name" column → Axis field
4. Drag "Marks" column → Values field
5. Chart populates automatically
6. Use Format panel to change colors, font, title
```

---

## 8. Slicers (Interactive Filters)

**Theory:** A **Slicer** is a visual that acts as a filter for all other visuals on the same page. Click on a slicer item and all charts update instantly.

```
Steps to add a Slicer:
1. Click "Slicer" in Visualizations panel
2. Drag a column (e.g., "Class" or "Year") into the Field
3. The slicer appears — click any value to filter all visuals
```

---

## 9. DAX Basics (Data Analysis Expressions)

**Theory:** **DAX** is Power BI's formula language — similar to Excel formulas but for data models. Used to create **Calculated Columns** and **Measures**.

### Calculated Column vs Measure
| | Calculated Column | Measure |
|---|---|---|
| Stored in | Table (row by row) | Not stored, calculated on fly |
| Use for | Row-level calculation | Aggregations (sum, avg, count) |
| Example | `Grade = IF(Marks>=33,"Pass","Fail")` | `Total Sales = SUM(Sales[Amount])` |

### Common DAX Functions

```DAX
-- SUM
Total Marks = SUM(Students[Marks])

-- AVERAGE
Avg Marks = AVERAGE(Students[Marks])

-- COUNT
Student Count = COUNT(Students[Student_ID])

-- IF (Calculated Column)
Grade = IF(Students[Marks] >= 85, "A",
        IF(Students[Marks] >= 70, "B",
        IF(Students[Marks] >= 55, "C",
        IF(Students[Marks] >= 33, "D", "Fail"))))

-- CALCULATE (most powerful DAX function)
Pass Count = CALCULATE(COUNT(Students[Name]), Students[Marks] >= 33)

-- FILTER
Top Scorers = CALCULATE(SUM(Students[Marks]), FILTER(Students, Students[Marks] > 80))

-- RELATED (to use column from related table)
Student Class = RELATED(Classes[ClassName])
```

**Steps to add a Measure:**
```
1. Go to Table View
2. Right-click table name → New Measure
3. Write DAX formula in formula bar
4. Press Enter
5. Measure appears with calculator icon
6. Drag it into any visual
```

---

## 10. Formatting a Report

```
Click on any visual → Format Visual panel appears (paintbrush icon)

Key formatting options:
- Title:        Change text, font size, color
- Data Labels:  Show values on bars/slices
- Legend:       Show/hide legend
- Colors:       Change bar/line/slice colors
- Background:   Add background color to visual
- Border:       Add border around visual
- Canvas:       Home → View → Canvas Background (whole page color)
- Themes:       View → Themes → choose preset color theme
```

---

## 11. Publishing & Sharing

```
Steps to publish to Power BI Service (cloud):
1. Sign in with Microsoft account (free)
2. Home → Publish
3. Select "My Workspace"
4. Report uploads to powerbi.com
5. Share link with others or embed in website
```

---

## 12. Quick Reference – Power BI Workflow

```
RAW DATA
    ↓
Get Data (Connect source)
    ↓
Power Query (Clean & Transform)
    ↓
Data Model (Set Relationships)
    ↓
DAX (Create Measures & Columns)
    ↓
Visualizations (Build Charts)
    ↓
Format & Design (Make it look good)
    ↓
Publish & Share (Power BI Service)
```

---

## 13. Power BI vs Excel vs Python (Pandas)

| Feature | Power BI | Excel | Python (Pandas) |
|---|---|---|---|
| Best for | Dashboards & reports | Quick analysis | Large data / automation |
| Coding needed | No (DAX optional) | No (formulas) | Yes |
| Interactivity | High | Medium | Low (unless Streamlit) |
| Data size limit | Large (millions) | ~1 million rows | Unlimited |
| Sharing | Easy (cloud) | File sharing | Requires deployment |
| Real-time data | Yes | Limited | Yes |

---

## Summary of Day 16
Today I learned **Power BI** — Microsoft's Business Intelligence tool for building interactive dashboards. I covered the **3 views** (Report, Table, Model), how to **import data** from CSV/Excel, how to **clean and transform** data using **Power Query Editor** (remove duplicates, change data type, filter, replace values), how to create **relationships** between tables in Model View, how to build **visualizations** (bar, line, pie, card, slicer, matrix), and the basics of **DAX** — `SUM`, `AVERAGE`, `COUNT`, `IF`, `CALCULATE`, and `FILTER`. I also learned how to format reports and publish them to Power BI Service.

**Practice Tasks for Tomorrow:**
1. Import a CSV file into Power BI and clean it using Power Query (remove nulls, fix data types).
2. Create a bar chart showing total sales by category from a sales dataset.
3. Add a slicer by Year and observe how all charts filter dynamically.
4. Write a DAX measure to calculate total revenue and average order value.
5. Build a 1-page dashboard with at least 4 visuals — a card, bar chart, line chart, and slicer.