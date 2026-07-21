# Daily Diary – Day 25
`Date : 21/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** Spotify Dashboard Project – Phase 2 (Advanced SQL Queries, Window Functions, KPI Calculations)

---

## 1. Phase 2 Goal
Use **advanced SQL** to extract meaningful KPIs and insights that will directly power the Power BI dashboard in Phase 3.

---

## 2. Window Functions

**Theory:** Window functions perform calculations across a set of rows **without collapsing them** into one row (unlike GROUP BY). Used for ranking, running totals, and comparisons.

```sql
-- RANK songs by popularity within each genre
SELECT track_name, track_artist, genre, track_popularity,
       RANK() OVER (PARTITION BY genre ORDER BY track_popularity DESC) AS genre_rank
FROM spotify;

-- Top 3 songs per genre
SELECT * FROM (
    SELECT track_name, track_artist, genre, track_popularity,
           RANK() OVER (PARTITION BY genre ORDER BY track_popularity DESC) AS rnk
    FROM spotify
) ranked
WHERE rnk <= 3;

-- ROW_NUMBER – unique rank even for ties
SELECT track_name, track_popularity,
       ROW_NUMBER() OVER (ORDER BY track_popularity DESC) AS row_num
FROM spotify;

-- DENSE_RANK – no gaps in rank on ties
SELECT track_name, track_popularity,
       DENSE_RANK() OVER (ORDER BY track_popularity DESC) AS dense_rnk
FROM spotify;
```

---

## 3. Running Total & Moving Average

```sql
-- Cumulative songs released over years
SELECT release_year,
       COUNT(*) AS songs_this_year,
       SUM(COUNT(*)) OVER (ORDER BY release_year) AS cumulative_songs
FROM spotify
GROUP BY release_year;

-- 3-year moving average of avg popularity
SELECT release_year,
       ROUND(AVG(track_popularity), 2) AS avg_pop,
       ROUND(AVG(AVG(track_popularity))
             OVER (ORDER BY release_year ROWS BETWEEN 2 PRECEDING AND CURRENT ROW), 2)
             AS moving_avg
FROM spotify
GROUP BY release_year;
```

---

## 4. KPI Queries for Dashboard

```sql
-- Total songs, artists, genres, avg popularity, avg BPM
SELECT
    COUNT(*)                          AS total_songs,
    COUNT(DISTINCT track_artist)      AS total_artists,
    COUNT(DISTINCT genre)             AS total_genres,
    ROUND(AVG(track_popularity), 1)   AS avg_popularity,
    ROUND(AVG(tempo), 1)              AS avg_bpm,
    SUM(CASE WHEN popularity_category = 'Viral' THEN 1 ELSE 0 END) AS viral_songs
FROM spotify;

-- Top artist by avg popularity (min 5 songs)
SELECT track_artist, ROUND(AVG(track_popularity), 2) AS avg_pop
FROM spotify
GROUP BY track_artist
HAVING COUNT(*) >= 5
ORDER BY avg_pop DESC LIMIT 1;

-- Most popular song overall
SELECT track_name, track_artist, track_popularity
FROM spotify
ORDER BY track_popularity DESC LIMIT 1;

-- Genre with highest avg danceability
SELECT genre, ROUND(AVG(danceability), 3) AS avg_dance
FROM spotify
GROUP BY genre
ORDER BY avg_dance DESC LIMIT 1;
```

---

## 5. Decade-wise Trend Analysis

```sql
-- Add decade column
ALTER TABLE spotify ADD decade VARCHAR(10);
UPDATE spotify
SET decade = CONCAT(FLOOR(release_year / 10) * 10, 's');

-- Avg energy & valence per decade (mood shift over time)
SELECT decade,
       COUNT(*)                       AS total_songs,
       ROUND(AVG(valence), 3)         AS avg_happiness,
       ROUND(AVG(energy), 3)          AS avg_energy,
       ROUND(AVG(danceability), 3)    AS avg_danceability,
       ROUND(AVG(track_popularity), 1) AS avg_popularity
FROM spotify
WHERE release_year >= 1960
GROUP BY decade
ORDER BY decade;
```

---

## 6. Genre vs Genre Comparison

```sql
-- Full audio feature profile per genre
SELECT genre,
       ROUND(AVG(danceability), 3) AS danceability,
       ROUND(AVG(energy), 3)       AS energy,
       ROUND(AVG(valence), 3)      AS valence,
       ROUND(AVG(speechiness), 3)  AS speechiness,
       ROUND(AVG(acousticness), 3) AS acousticness,
       ROUND(AVG(tempo), 1)        AS avg_bpm,
       COUNT(*)                    AS total_songs
FROM spotify
GROUP BY genre
ORDER BY total_songs DESC;
```

---

## 7. Subquery – Artists Above Average Popularity

```sql
-- Artists whose avg popularity beats overall avg
SELECT track_artist,
       ROUND(AVG(track_popularity), 2) AS avg_pop
FROM spotify
GROUP BY track_artist
HAVING AVG(track_popularity) > (SELECT AVG(track_popularity) FROM spotify)
ORDER BY avg_pop DESC
LIMIT 15;
```

---

## 8. Views – Save Queries for Power BI

**Theory:** A **VIEW** is a saved SQL query that acts like a virtual table. Power BI can connect directly to views.

```sql
-- View 1: Genre summary for Power BI
CREATE VIEW genre_summary AS
SELECT genre,
       COUNT(*)                        AS total_songs,
       ROUND(AVG(track_popularity), 2) AS avg_popularity,
       ROUND(AVG(danceability), 3)     AS avg_danceability,
       ROUND(AVG(energy), 3)           AS avg_energy,
       ROUND(AVG(valence), 3)          AS avg_valence
FROM spotify
GROUP BY genre;

-- View 2: Top artists
CREATE VIEW top_artists AS
SELECT track_artist,
       COUNT(*)                        AS total_songs,
       ROUND(AVG(track_popularity), 2) AS avg_popularity
FROM spotify
GROUP BY track_artist
HAVING COUNT(*) >= 5
ORDER BY avg_popularity DESC;

-- View 3: Decade trends
CREATE VIEW decade_trends AS
SELECT decade, release_year,
       COUNT(*)                        AS songs,
       ROUND(AVG(valence), 3)          AS avg_valence,
       ROUND(AVG(energy), 3)           AS avg_energy,
       ROUND(AVG(track_popularity), 2) AS avg_popularity
FROM spotify
GROUP BY decade, release_year;

-- Use a view
SELECT * FROM genre_summary;
SELECT * FROM top_artists LIMIT 10;
```

---

## 9. Phase 2 Key Findings

```
🏆 Top Artist      → Weekend / Bad Bunny (by avg popularity)
🎵 Most Viral Genre→ Pop (highest count of 80+ songs)
😊 Happiest Decade → 1960s–1980s (highest avg valence)
📉 Mood Drop       → Valence steadily falling since 1990s
⚡ Energy Rise     → EDM pushed avg energy up post-2010
🕺 Most Danceable  → Latin (consistent across all years)
📅 Peak Year       → 2019 (highest song releases)
```

---

## 10. Phase 2 Checklist

```
✅ Window functions → RANK, DENSE_RANK, ROW_NUMBER
✅ Cumulative & moving average queries
✅ All KPI queries ready for dashboard cards
✅ Decade column added and trend analysis done
✅ Genre vs genre full audio feature comparison
✅ Above-average artist subquery
✅ 3 Views created for Power BI connection
⬜ Phase 3 → Connect MySQL to Power BI → Build Dashboard
```

---

## Summary of Day 25
Today I completed **Phase 2 of the Spotify Project** — advanced SQL analysis. I used **window functions** (`RANK`, `DENSE_RANK`, `ROW_NUMBER`, running totals, moving averages) to rank songs per genre, calculated all **dashboard KPIs** (total songs, artists, viral count, top artist, top song), analyzed **decade-wise mood shifts** (valence declining post-1990s), compared **genre audio profiles**, found artists above average popularity using a **subquery**, and created **3 SQL Views** that Power BI will connect to directly in Phase 3.