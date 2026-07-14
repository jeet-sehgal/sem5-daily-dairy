# Daily Diary – Day 19
`Date : 14/07/26`
**Subject:** Data Analytics
#### **Topic Covered:** Power BI – Slicers (All Types & Settings) and Data Transformation (Power Query Editor – In Depth)

---

## PART A – SLICERS

---

## 1. What is a Slicer? (Brief Theory)
A **Slicer** is a visual filter placed directly on the report canvas. When a user clicks a value in a slicer, **all other visuals on the same page filter automatically** based on that selection. Slicers make dashboards interactive without any coding.

```
Without Slicer → Static report, user can't filter
With Slicer    → Interactive report, user controls the view
```

---

## 2. How to Add a Slicer

```
Steps:
1. Go to Visualizations panel
2. Click the Slicer icon (funnel shape)
3. A blank slicer appears on canvas
4. In Fields panel → drag a column into "Field" well
   (e.g., Region, Year, Category, Gender)
5. Slicer populates with values from that column
6. Click any value → all visuals filter ✓
```

---

## 3. Slicer Styles (Types)

**Format Visual → Visual tab → Slicer settings → Options → Style**

### Style 1 – List (Default)
```
Appearance: Checkbox list of all values
  ☑ North
  ☑ South
  ☐ East
  ☐ West

Best for: Text/category columns with few values
Multi-select: Click multiple checkboxes
Single select: Format → Selection → Single Select → ON
```

### Style 2 – Dropdown
```
Appearance: Compact dropdown — shows one value at a time
  [  Region  ▼  ]

Best for: When slicer space is limited on canvas
Click dropdown → select from list
Multi-select: Hold Ctrl + Click
```

### Style 3 – Tile (Button style)
```
Appearance: Each value shown as a clickable button tile
  [ North ]  [ South ]  [ East ]  [ West ]

Best for: Small number of distinct values (2–6)
Looks: Clean, modern, easy to click
Orientation: Horizontal or Vertical
```

### Style 4 – Between (Range Slider)
```
Appearance: Two handles on a slider
  |----[====]---|
  Min          Max

Best for: Numeric columns (Sales, Age, Quantity)
          Date columns (pick a date range)
User drags handles to set min and max range
```

### Style 5 – Before / After / Relative (Date Slicers)
```
Best for: Date columns

- Before  → show data before a selected date
- After   → show data after a selected date
- Relative → dynamic:
    "Last 7 days", "This Month", "This Year"
    "Last 3 Months", "Last 1 Quarter"
    → updates automatically as time passes
```

---

## 4. Slicer Formatting Options

```
Format Visual → Visual tab:

Slicer Settings:
  - Style         → List / Dropdown / Tile / Between / Relative
  - Orientation   → Horizontal / Vertical (for List & Tile)

Selection:
  - Show "Select All" option → ON/OFF
    (adds a "Select All" checkbox at the top)
  - Single Select  → ON (only one value at a time)
  - Multi-Select with Ctrl → ON/OFF

Search:
  - Search box    → ON (adds a search bar inside slicer)
    Best for: columns with many values (50+ items)

Values:
  - Font size, font color, background color per item

Slicer Header:
  - Show/hide the slicer header (column name at top)
  - Rename the header text
  - Font size, color, bold

Background:
  - Set background color for whole slicer visual
```

---

## 5. Slicer Interactions

### Default Behaviour
```
By default → Slicer filters ALL visuals on the same page
```

### Change Interaction for Specific Visuals
```
Steps:
1. Click on the Slicer visual
2. Format tab (ribbon) → Edit Interactions
3. Small icons appear on each other visual:
   🔽 Filter icon   → slicer WILL filter this visual
   📊 Highlight     → slicer highlights but doesn't filter
   ⊘  None          → slicer has NO effect on this visual
4. Click the icon you want on each visual
5. Click Edit Interactions again to exit
```

### Sync Slicers Across Multiple Pages
```
Steps:
1. Click the Slicer
2. View tab (ribbon) → Sync Slicers
3. A panel opens showing all pages
4. Toggle:
   👁 Visible  → slicer appears on that page
   🔄 Sync     → slicer filters that page even if not visible

Example:
Page 1 → Year Slicer (visible + synced)
Page 2 → Year Slicer (synced but not visible → still filters Page 2)
Page 3 → Year Slicer (synced + visible)
→ Selecting 2023 on Page 1 filters Page 2 and Page 3 too ✓
```

---

## 6. Date Slicer – Relative Filtering (Practical)

```
Steps:
1. Add Slicer → Field → Order_Date (date column)
2. Format → Slicer settings → Style → Relative

3. Set relative period:
   Show items in the last → 1 → Years
   Show items in the last → 3 → Months
   Show items in the last → 7 → Days

4. Anchor date (optional):
   Toggle → Use Anchor Date → ON
   Set date → all calculations relative to that date

Real-world use:
  Sales report always shows "last 30 days" automatically
  No need to update date filter manually every month ✓
```

---

## 7. Slicer – Practical Examples

### Example 1 – Year Slicer (Tile Style)
```
Field   → Year (extracted from Order_Date)
Style   → Tile
Layout  → Horizontal
Select All → OFF

Tiles: [ 2021 ]  [ 2022 ]  [ 2023 ]  [ 2024 ]
Click 2023 → all charts show only 2023 data
```

### Example 2 – Region Slicer (List Style)
```
Field   → Region
Style   → List
Show "Select All" → ON
Multi-select → ON (Ctrl + Click for multiple)

☑ Select All
☑ East
☑ North
☐ South
☐ West
```

### Example 3 – Sales Range Slicer (Between Style)
```
Field   → Sales
Style   → Between
Slider: |----[1000====50000]---|
→ Shows only orders where Sales is between 1000 and 50000
```

### Example 4 – Search Slicer (Many Values)
```
Field   → Customer_Name  (500+ customers)
Style   → Dropdown
Search  → ON

[  Search customers...  ]
Type "Bh" → shows only Bhawna, Bharat, Bhanu...
Click name → all visuals filter to that customer ✓
```

---

---

## PART B – DATA TRANSFORMATION (POWER QUERY EDITOR)

---

## 8. What is Power Query? (Brief Theory)
**Power Query Editor** is Power BI's built-in data cleaning and transformation engine. Every step you perform is recorded as a step in "Applied Steps" — making it fully repeatable and editable.

```
Open Power Query:
  Home → Transform Data → Power Query Editor opens
```

**Power Query Window Layout:**
```
┌──────────────────────────────────────────────────────────┐
│  RIBBON (Home, Transform, Add Column, View)              │
├─────────────┬──────────────────────────┬─────────────────┤
│             │                          │                 │
│  QUERIES    │  DATA PREVIEW            │  APPLIED STEPS  │
│  PANEL      │  (shows rows & columns   │  (every action  │
│  (tables)   │   of selected table)     │   recorded here)│
│             │                          │                 │
└─────────────┴──────────────────────────┴─────────────────┘
│  FORMULA BAR (M Language formula for selected step)      │
└──────────────────────────────────────────────────────────┘
```

---

## 9. Changing Data Types

```
Why important:
  If a Sales column is stored as Text → SUM won't work
  If Date is stored as Text → date slicers won't work

Steps:
1. Click the data type icon on column header (left of column name)
   ABC = Text
   123 = Whole Number
   1.2 = Decimal Number
   📅  = Date
   ✓   = Boolean (True/False)

2. Select correct data type from dropdown

3. A dialog asks "Replace current conversion?" → Replace

OR:
  Select column → Transform tab → Data Type → choose type

Common fixes:
  Sales, Profit, Discount → Decimal Number
  Quantity, Order_ID      → Whole Number
  Order_Date, Ship_Date   → Date
  Customer_Name, Region   → Text
```

---

## 10. Removing Columns

```
Method 1 – Remove specific column:
  Right-click column header → Remove

Method 2 – Remove multiple columns:
  Ctrl + Click multiple column headers → Right-click → Remove Columns

Method 3 – Keep only selected columns (remove all others):
  Select columns you WANT to keep
  Right-click → Remove Other Columns

Method 4 – Home tab:
  Home → Remove Columns → Remove Columns / Remove Other Columns
```

---

## 11. Renaming Columns

```
Method 1: Double-click column header → type new name → Enter

Method 2: Right-click column header → Rename → type new name

Example renames:
  "Cust_NM"    → "Customer Name"
  "Ord_Dt"     → "Order Date"
  "Tot_Sls"    → "Total Sales"
  "Prft_Mrgn"  → "Profit Margin"
```

---

## 12. Filtering Rows

```
Click the dropdown arrow (▼) on any column header

Options:
  ✅ Text Filters:
     Equals / Does Not Equal
     Contains / Does Not Contain
     Begins With / Ends With

  ✅ Number Filters:
     Equals / Greater Than / Less Than / Between

  ✅ Date Filters:
     Before / After / Between
     Is In Previous N Days/Months/Years

Example 1: Keep only rows where Region = "North"
  Click ▼ on Region → uncheck all → check "North" only → OK

Example 2: Keep only rows where Sales > 100
  Click ▼ on Sales → Number Filters → Greater Than → 100

Example 3: Remove cancelled orders
  Click ▼ on Status → uncheck "Cancelled" → OK
```

---

## 13. Removing Duplicates & Blank Rows

```
Remove Duplicate Rows (keep first occurrence):
  Select key column (e.g., Order_ID)
  Home → Remove Rows → Remove Duplicates

Remove Blank Rows:
  Home → Remove Rows → Remove Blank Rows

Remove Rows with Errors:
  Home → Remove Rows → Remove Errors

Remove Top/Bottom N Rows:
  Home → Remove Rows → Remove Top Rows → enter number
  Home → Remove Rows → Remove Bottom Rows → enter number
```

---

## 14. Splitting Columns

```
Use case: "Full Name" column has "Bhawna Sharma" → split into First & Last

Method 1 – By Delimiter:
  Select column → Transform → Split Column → By Delimiter
  Delimiter: Space (or comma, semicolon)
  Split at: Each occurrence / Left-most / Right-most
  → Creates two new columns

Method 2 – By Number of Characters:
  Select column → Transform → Split Column → By Number of Characters
  Enter: 5 characters → splits after 5th character

Method 3 – By Position:
  Custom positions to split the string
```

---

## 15. Merging Columns

```
Opposite of Split — combine two columns into one

Steps:
1. Hold Ctrl + Click both columns (e.g., First_Name, Last_Name)
2. Transform → Merge Columns
3. Separator → Space (or comma, dash)
4. New column name → "Full Name"
→ Creates one column: "Bhawna Sharma"
```

---

## 16. Replace Values

```
Steps:
1. Select the column
2. Transform → Replace Values
3. Value to Find → type old value (e.g., "N/A", "null", "0")
4. Replace With → type new value (e.g., "Unknown", "0", "Not Available")
5. Click OK

Examples:
  Replace "M" with "Male" in Gender column
  Replace "F" with "Female" in Gender column
  Replace 0 with null in Sales column
  Replace "N/A" with "Unknown" in Country column
```

---

## 17. Adding Custom Columns

```
Add Column tab → Custom Column

Examples:

1. Profit Margin %
   Column Name: Profit Margin %
   Formula: = [Profit] / [Sales] * 100

2. Full Name
   Column Name: Full Name
   Formula: = [First_Name] & " " & [Last_Name]

3. Shipping Days
   Column Name: Shipping Days
   Formula: = Duration.Days([Ship_Date] - [Order_Date])

4. Sales Category
   Column Name: Sales Category
   Formula: = if [Sales] > 1000 then "High"
               else if [Sales] > 500 then "Medium"
               else "Low"
```

---

## 18. Extracting Date Parts

```
Select a Date column → Add Column tab → Date →

  Year        → extracts year (2023)
  Month       → extracts month number (1–12)
  Month Name  → extracts month name (January, February...)
  Quarter     → extracts quarter (1–4)
  Day         → extracts day number
  Week Number → extracts week of year
  Day of Week → extracts day name (Monday, Tuesday...)

These columns are used:
  Month Name → X-axis of line chart (sorted by Month Number)
  Year       → Slicer filter
  Quarter    → Matrix columns
```

---

## 19. Grouping Rows (Group By)

```
Use: Summarize/aggregate data — like GROUP BY in SQL

Steps:
  Home → Group By

Example 1: Total Sales per Region
  Group by: Region
  New column: Total Sales
  Operation: Sum
  Column: Sales
  → Creates a summary table with one row per region

Example 2: Count of orders per Customer
  Group by: Customer_Name
  New column: Order Count
  Operation: Count Rows
  → Each row = one customer with their order count
```

---

## 20. Pivot & Unpivot Columns

### Pivot Column (Rows → Columns)
```
Use: Turn row values into column headers

Example:
  Before:
  Month  | Sales
  Jan    | 5000
  Feb    | 7000
  Mar    | 6000

  Select Month column → Transform → Pivot Column
  Values column → Sales
  Aggregate → Sum

  After:
  Jan   | Feb   | Mar
  5000  | 7000  | 6000
```

### Unpivot Columns (Columns → Rows)
```
Use: Turn column headers into row values (reverse of pivot)

Example:
  Before:
  Name   | Jan  | Feb  | Mar
  Bhawna | 85   | 90   | 88

  Select Jan, Feb, Mar columns → Transform → Unpivot Columns

  After:
  Name   | Attribute | Value
  Bhawna | Jan       | 85
  Bhawna | Feb       | 90
  Bhawna | Mar       | 88
```

---

## 21. Append Queries (Stack Tables)

```
Use: Stack two tables with same columns on top of each other (like UNION in SQL)

Steps:
  Home → Append Queries → Append Queries as New
  Table 1: Sales_2023
  Table 2: Sales_2024
  → Creates a new combined table with all rows from both

Conditions:
  Both tables must have same column names
  Mismatched columns → filled with null
```

---

## 22. Merge Queries (Join Tables)

```
Use: Join two tables on a common column (like JOIN in SQL)

Steps:
  Home → Merge Queries → Merge Queries as New
  Table 1: Orders (Order_ID, Customer_ID, Sales)
  Table 2: Customers (Customer_ID, Name, City)
  Join column: Customer_ID (both tables)
  Join kind:
    Inner Join    → only matching rows
    Left Outer   → all rows from Table 1, match from Table 2
    Right Outer  → all rows from Table 2, match from Table 1
    Full Outer   → all rows from both tables

→ Expand the merged column to show columns from Table 2
```

---

## 23. Applied Steps Panel – Key Feature

```
Every transformation is recorded as a step:
  ✅ Step 1: Source
  ✅ Step 2: Promoted Headers
  ✅ Step 3: Changed Type
  ✅ Step 4: Removed Columns
  ✅ Step 5: Added Custom Column
  ✅ Step 6: Filtered Rows

Actions on steps:
  Click any step → preview data at that point in time
  Rename step    → right-click → Rename
  Delete step    → click X next to step (careful — removes that transformation)
  Reorder steps  → drag up/down
  Edit step      → click gear ⚙ icon next to step → edit settings

This makes Power Query:
  ✅ Fully auditable (see every change)
  ✅ Repeatable (refresh = all steps run again on new data)
  ✅ Editable (go back and change any step)
```

---

## 24. Close & Apply

```
After all transformations are done:
  Home → Close & Apply

What happens:
  1. Power Query closes
  2. All transformations applied to data
  3. Clean data loaded into Power BI data model
  4. Fields panel updates with new columns

If you make mistakes after closing:
  Home → Transform Data → Power Query reopens
  Edit any step and Close & Apply again
```

---

## 25. Quick Reference – Power Query Transformations

| Task | Where |
|---|---|
| Change data type | Click type icon on column header |
| Rename column | Double-click column header |
| Remove column | Right-click → Remove |
| Filter rows | Column dropdown ▼ |
| Remove duplicates | Home → Remove Rows → Remove Duplicates |
| Remove blank rows | Home → Remove Rows → Remove Blank Rows |
| Split column | Transform → Split Column |
| Merge columns | Transform → Merge Columns |
| Replace values | Transform → Replace Values |
| Add custom column | Add Column → Custom Column |
| Extract date parts | Add Column → Date |
| Group by | Home → Group By |
| Pivot | Transform → Pivot Column |
| Unpivot | Transform → Unpivot Columns |
| Append (stack) | Home → Append Queries |
| Merge (join) | Home → Merge Queries |

---

## Summary of Day 19
Today I learned **Slicers** in full depth — all 5 styles (List, Dropdown, Tile, Between, Relative), formatting options (Select All, Single Select, Search), changing slicer interactions, and syncing slicers across multiple pages. In the second half I went deep into **Power Query Editor** — the complete data transformation toolkit. I covered changing data types, removing/renaming columns, filtering rows, removing duplicates and blanks, splitting and merging columns, replacing values, adding custom columns with formulas, extracting date parts (Year, Month, Quarter), grouping rows, pivoting and unpivoting, appending (stacking) and merging (joining) tables, and the **Applied Steps** panel which records every transformation.

**Practice Tasks for Tomorrow:**
1. Add a relative date slicer showing "Last 3 Months" data dynamically.
2. Sync a Year slicer across 3 pages of a report.
3. In Power Query — split a "Full Name" column into First Name and Last Name.
4. Create a custom column "Shipping Days" = Ship Date – Order Date.
5. Append two years of sales data (Sales_2023 and Sales_2024) into one table using Append Queries.