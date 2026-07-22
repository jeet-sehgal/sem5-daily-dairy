# Daily Diary – Day 26
`Date  : 22/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** Spotify Dashboard Project – Phase 3 (Connecting MySQL to Power BI, Building Final Dashboard)

---

## 1. Phase 3 Goal
Connect the cleaned **MySQL database** to **Power BI**, import the views created in Phase 2, and build the complete **Spotify Analytics Dashboard**.

---

## 2. Connect MySQL to Power BI

```
Steps:
1. Open Power BI Desktop
2. Home → Get Data → MySQL Database
3. Server   → localhost (or your server IP)
4. Database → spotify_db
5. Click OK → Enter MySQL username & password
6. Navigator opens → select tables/views to import:
   ✅ spotify           (main table)
   ✅ genre_summary     (view)
   ✅ top_artists       (view)
   ✅ decade_trends     (view)
7. Click Load → data loads into Power BI
```

---

## 3. Data Verification in Power BI

```
After loading → go to Table View:

Check spotify table:
  ✅ track_popularity  → Whole Number
  ✅ danceability      → Decimal Number
  ✅ release_date      → Date
  ✅ genre             → Text
  ✅ duration_min      → Decimal Number
  ✅ mood              → Text
  ✅ decade            → Text

Check views loaded correctly:
  SELECT * FROM genre_summary   → 6 rows (one per genre)
  SELECT * FROM top_artists     → top artists list
  SELECT * FROM decade_trends   → year-wise data
```

---

## 4. DAX Measures

```DAX
Total Songs      = COUNT(spotify[track_id])
Total Artists    = DISTINCTCOUNT(spotify[track_artist])
Avg Popularity   = ROUND(AVERAGE(spotify[track_popularity]), 1)
Avg BPM          = ROUND(AVERAGE(spotify[tempo]), 1)
Avg Danceability = ROUND(AVERAGE(spotify[danceability]) * 100, 1)
Viral Songs      = CALCULATE(COUNT(spotify[track_id]),
                             spotify[popularity_category] = "Viral")
Avg Valence      = ROUND(AVERAGE(spotify[valence]) * 100, 1)
Avg Energy       = ROUND(AVERAGE(spotify[energy]) * 100, 1)
```

---

## 5. Dashboard Layout – Page 1 (Overview)

```
┌──────────────────────────────────────────────────────────┐
│  🎵 Spotify Music Analytics Dashboard                    │
├───────┬───────┬───────┬───────┬───────┬─────────────────┤
│ CARD  │ CARD  │ CARD  │ CARD  │ CARD  │ CARD            │
│Total  │Total  │ Avg   │ Avg   │Viral  │ Avg             │
│Songs  │Artists│ Pop.  │ BPM   │Songs  │ Danceability    │
├───────┴───────┼───────────────┼─────────────────────────┤
│ BAR CHART     │ LINE CHART    │ DONUT CHART             │
│ Top 10 Artists│ Songs Per Year│ Songs by Genre          │
│ by Popularity │ (Trend)       │ (Proportion)            │
├───────────────┼───────────────┼─────────────────────────┤
│ SCATTER CHART │ COLUMN CHART  │ TABLE                   │
│ Energy vs     │ Danceability  │ Top 10 Songs            │
│ Valence       │ by Genre      │ (Name, Artist, Pop.)    │
├───────────────┴───────────────┴─────────────────────────┤
│ SLICER: Genre │ SLICER: Decade │ SLICER: Mood           │
└──────────────────────────────────────────────────────────┘
```

---

## 6. Building Each Visual

### KPI Cards (Row 1)
```
6 Cards in a row:
  Total Songs | Total Artists | Avg Popularity | Avg BPM | Viral Songs | Avg Danceability
  Background → #282828 (dark grey)
  Value color → #1DB954 (Spotify green)
  Font size   → 28, Bold
```

### Bar Chart – Top 10 Artists
```
Visual    → Clustered Bar Chart
Source    → top_artists view
Y-axis    → track_artist
X-axis    → avg_popularity
Filter    → Top N → 10 by avg_popularity
Color     → #1DB954
Sort      → Descending
Title     → "Top 10 Artists by Popularity"
```

### Line Chart – Songs Per Year
```
Visual    → Line Chart
Source    → decade_trends view
X-axis    → release_year
Y-axis    → songs (count)
Line color→ #1DB954
Markers   → ON
Title     → "Songs Released Per Year"
```

### Donut Chart – Songs by Genre
```
Visual    → Donut Chart
Source    → genre_summary view
Legend    → genre
Values    → total_songs
Labels    → Category + Percent
Title     → "Songs by Genre"
Colors    → Pop(green) Rock(red) EDM(blue) Latin(pink) R&B(orange) Rap(yellow)
```

### Scatter Chart – Energy vs Valence (Mood Map)
```
Visual    → Scatter Chart
Source    → genre_summary view
X-axis    → avg_energy
Y-axis    → avg_valence
Values    → genre
Size      → total_songs
Title     → "Genre Mood Map (Energy vs Happiness)"
```

### Column Chart – Danceability by Genre
```
Visual    → Clustered Column Chart
Source    → genre_summary view
X-axis    → genre
Y-axis    → avg_danceability
Color     → gradient green
Data Labels → ON
Title     → "Avg Danceability by Genre"
```

### Top 10 Songs Table
```
Visual    → Table
Source    → spotify table
Columns   → track_name, track_artist, genre, track_popularity, duration_min
Filter    → Top 10 by track_popularity
Header BG → #1DB954
Conditional Formatting → Popularity column → green color scale
Title     → "Top 10 Most Popular Songs"
```

### Slicers (Bottom Row)
```
Slicer 1 → genre        → Style: Tile
Slicer 2 → decade       → Style: Tile
Slicer 3 → mood         → Style: Dropdown
All slicers: Dark bg (#282828), Green selected (#1DB954)
```

---

## 7. Page 2 – Audio Features Trend

```
Visual 1 → Line Chart
  X-axis → decade, Y-axis → avg_valence
  Title  → "Happiness of Music Over Decades"

Visual 2 → Line Chart
  X-axis → decade, Y-axis → avg_energy
  Title  → "Energy of Music Over Decades"

Visual 3 → Clustered Bar Chart
  X-axis → genre
  Y-axis → avg_danceability, avg_energy, avg_valence (3 measures)
  Title  → "Full Audio Profile by Genre"

Visual 4 → Card → Avg Valence | Card → Avg Energy

Slicer → genre, decade
```

---

## 8. Page 3 – Artist Deep Dive

```
Visual 1 → Bar Chart  → Top 15 Artists by Total Songs
Visual 2 → Bar Chart  → Top 15 Artists by Avg Popularity
Visual 3 → Table      → Artist | Songs | Avg Pop | Avg Dance | Top Genre
Visual 4 → Scatter    → Total Songs vs Avg Popularity (by artist)

Drill Through:
  Add track_artist to Drill Through field
  Right-click any artist on Page 1 bar chart
  → Drill Through → Artist Deep Dive page ✓
```

---

## 9. Final Theme & Formatting

```
Canvas Background   → #191414 (Spotify black)
Accent Color        → #1DB954 (Spotify green)
All text            → #FFFFFF (white)
Card backgrounds    → #282828
Chart backgrounds   → #282828
All titles          → White, 14pt, Bold
Gridlines           → Dark grey (#3A3A3A)

Apply globally:
  View → Themes → Customize:
  Primary color     → #1DB954
  Background        → #191414
  Foreground        → #282828
  Text              → #FFFFFF
```

---

## 10. Final Dashboard Checklist

```
✅ MySQL connected to Power BI successfully
✅ All 4 tables/views loaded and verified
✅ 8 DAX measures created
✅ Page 1 – Overview (6 cards + 5 charts + 3 slicers)
✅ Page 2 – Audio Feature Trends (decade & genre)
✅ Page 3 – Artist Deep Dive (with drill through)
✅ Spotify dark theme applied throughout
✅ All slicers tested (genre, decade, mood)
✅ Drill through working artist → detail page
✅ Data labels on all bar/column charts
✅ Top 10 filters on table and bar chart
✅ Saved as Spotify_Final_Dashboard.pbix
✅ Published to Power BI Service
```

---

## Project Complete – Final Insights

```
🎵 Most Songs Genre    → Pop
🏆 Top Artist          → Bad Bunny / The Weeknd
🔥 Most Viral Genre    → Pop & Latin
😊 Happiest Decade     → 1960s–1970s (high valence)
📉 Music Mood Drop     → Valence declining since 1990
⚡ Energy Peak         → 2010s (EDM era)
🕺 Most Danceable      → Latin
📅 Peak Release Year   → 2019
🎧 Avg Song Duration   → ~3.5 minutes
```

---

## Summary of Day 26
Today I completed **Phase 3 — the final phase of the Spotify Dashboard Project**. I connected **MySQL to Power BI** using the MySQL connector and imported the main `spotify` table and all 3 views (`genre_summary`, `top_artists`, `decade_trends`). I created **8 DAX measures**, built a **3-page dashboard** — Overview (6 KPI cards, 5 charts, 3 slicers), Audio Features (decade and genre trends), and Artist Deep Dive (with drill through) — all styled with the **Spotify dark theme** (`#191414` background, `#1DB954` green). Slicers and interactions tested. Dashboard published. **Project fully complete ✅**

```
Project : Spotify Music Analytics Dashboard
Phases  : 3 (SQL Setup → Advanced SQL → Power BI)
Pages   : 3
Visuals : 18+
File    : Spotify_Final_Dashboard.pbix
Status  : COMPLETE ✅
```