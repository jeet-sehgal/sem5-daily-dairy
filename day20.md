# Daily Diary – Day 20
`Date : 15/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** Project Selection + Spotify Music Analytics Dashboard in Power BI

---

## 1. How to Choose a Project
A good project should have:
- Clear question to answer
- Rich dataset (500+ rows, mixed column types)
- Time-based data for trends
- A topic you understand

**Why Spotify?** → Rich dataset with 15+ columns (song name, artist, genre, popularity, audio features), relatable topic, perfect for all chart types.

---

## 2. Dataset Columns

```
Song Name | Artist | Genre | Popularity (0-100) | Release Date
danceability | energy | valence | tempo (BPM) | duration_ms
```

---

## 3. Power Query – Cleaning Steps

```
1. Fix data types → Popularity (Whole), Sales (Decimal), Date (Date)
2. Remove duplicates → by Song Name + Artist
3. Remove blank rows
4. Add custom column → Duration (Min) = [duration_ms] / 60000
5. Add custom column → Popularity Category:
   if Popularity >= 80 → "Viral"
   else if >= 60 → "Popular"
   else if >= 40 → "Moderate"
   else → "Low"
6. Extract Year from Release Date → Add Column → Date → Year
7. Close & Apply
```

---

## 4. DAX Measures

```DAX
Total Songs      = COUNT('spotify'[Song Name])
Total Artists    = DISTINCTCOUNT('spotify'[Artist])
Avg Popularity   = AVERAGE('spotify'[Popularity])
Avg BPM          = AVERAGE('spotify'[tempo])
Avg Danceability = AVERAGE('spotify'[danceability]) * 100
Avg Energy       = AVERAGE('spotify'[energy]) * 100
Avg Valence      = AVERAGE('spotify'[valence]) * 100
Viral Songs      = CALCULATE(COUNT('spotify'[Song Name]),
                             'spotify'[Popularity Category] = "Viral")
```

---

## 5. Dashboard – Page 1 (Overview)

**Theme:** Spotify Dark → Background `#191414`, Accent `#1DB954` (green)

```
ROW 1 → 6 KPI Cards:
  Total Songs | Total Artists | Total Genres | Avg Popularity | Avg BPM | Viral Songs

ROW 2 → Charts:
  Bar Chart   → Top 10 Artists by Avg Popularity
  Line Chart  → Songs Released Per Year (trend)
  Donut Chart → Songs by Genre (proportion)

ROW 3 → Charts:
  Scatter Chart → Energy vs Valence (Mood Map)
  Column Chart  → Avg Danceability by Genre
  Table         → Top 10 Most Popular Songs

BOTTOM → Slicers:
  Genre (Tile) | Decade (Tile) | Popularity Category (Dropdown)
```

---

## 6. Page 2 – Audio Features

```
Line Chart → Avg Energy over Years
Line Chart → Avg Valence (Happiness) over Years
Bar Chart  → BPM Distribution of Songs
Bar Chart  → Audio Feature Comparison by Genre
```

---

## 7. Page 3 – Artist Analysis

```
Bar Chart → Top 15 Artists by Total Songs
Bar Chart → Top 15 Artists by Avg Popularity
Table     → Artist | Songs | Avg Popularity | Top Genre
Drill Through → click artist on Page 1 → opens Page 3 filtered to that artist
```

---

## 8. Key Insights

```
🎵 Most Popular Genre    → Pop & Latin
🕺 Most Danceable Genre  → Latin
⚡ Most Energetic Genre  → EDM & Rock
😊 Happiest Genre        → Pop (highest valence)
📅 Peak Release Years    → 2016–2019
📉 Trend                 → Song happiness declined after 2010
🔥 Viral Songs (80+)     → ~15% of all songs
```

---

## Summary of Day 20
Today I finalized the **Spotify Music Analytics Dashboard** as my project. I cleaned the dataset in Power Query (removed duplicates, added custom columns), created 8 DAX measures, and built a 3-page dashboard with Spotify's dark theme. Page 1 has KPI cards, trend charts, mood map scatter, and slicers. Page 2 covers audio feature trends over decades. Page 3 shows artist rankings with drill through. **Project complete ✅**

```
File   : Spotify_Dashboard.pbix
Pages  : 3 (Overview | Audio Features | Artist Analysis)
Visuals: 15+ charts, cards, and slicers
Theme  : Spotify Dark (Black + Green #1DB954)
```