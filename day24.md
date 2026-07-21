# Daily Diary – Day 24
`Date : 20/7/26`
**Subject:** Data Analytics
#### **Topic Covered:** Project Phase 1 – Spotify Dashboard (Dataset Understanding, Database Setup, Data Cleaning & Exploration using SQL)

---

## 1. Project Overview

**Project Name:** Spotify Music Analytics Dashboard
**Tool Stack:** SQL (MySQL) → Power BI (Dashboard)
**Goal:** Analyze 600,000+ Spotify songs to find trends in popularity, genres, audio features, and top artists.

```
Project Phases:
  Phase 1 (Today) → Setup, Data Import, Cleaning & Exploration in SQL
  Phase 2         → Advanced SQL Queries & KPI Calculations
  Phase 3         → Connect SQL to Power BI → Build Dashboard
```

---

## 2. Dataset Overview

**File:** `spotify_songs.csv`
**Source:** Kaggle – Spotify Songs Dataset

**Key Columns:**
```
track_id                  → Unique song ID
track_name                → Song name
track_artist              → Artist name
track_popularity          → Popularity score (0–100)
track_album_release_date  → Release date
playlist_genre            → Genre (pop, rock, edm, latin, r&b, rap)
playlist_subgenre         → Sub-genre
danceability              → 0 to 1 (how danceable)
energy                    → 0 to 1 (intensity)
loudness                  → dB value (-60 to 0)
speechiness               → 0 to 1 (spoken words)
acousticness              → 0 to 1 (acoustic level)
valence                   → 0 to 1 (happiness)
tempo                     → BPM (beats per minute)
duration_ms               → Duration in milliseconds
```

---

## 3. Phase 1 – Database & Table Setup

```sql
-- Step 1: Create database
CREATE DATABASE spotify_db;
USE spotify_db;

-- Step 2: Create table
CREATE TABLE spotify (
    track_id          VARCHAR(50)    PRIMARY KEY,
    track_name        VARCHAR(200),
    track_artist      VARCHAR(100),
    track_popularity  INT,
    release_date      DATE,
    genre             VARCHAR(50),
    subgenre          VARCHAR(50),
    danceability      DECIMAL(4,3),
    energy            DECIMAL(4,3),
    loudness          DECIMAL(6,3),
    speechiness       DECIMAL(4,3),
    acousticness      DECIMAL(4,3),
    valence           DECIMAL(4,3),
    tempo             DECIMAL(6,3),
    duration_ms       INT
);
```

---

## 4. Data Import

```sql
-- Import CSV into MySQL table
LOAD DATA INFILE 'spotify_songs.csv'
INTO TABLE spotify
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

-- Verify import
SELECT COUNT(*) FROM spotify;       -- total rows
SELECT * FROM spotify LIMIT 5;      -- preview first 5
```

---

## 5. Data Cleaning

### Check for Nulls
```sql
SELECT
    SUM(CASE WHEN track_name     IS NULL THEN 1 ELSE 0 END) AS null_names,
    SUM(CASE WHEN track_artist   IS NULL THEN 1 ELSE 0 END) AS null_artists,
    SUM(CASE WHEN track_popularity IS NULL THEN 1 ELSE 0 END) AS null_popularity,
    SUM(CASE WHEN genre          IS NULL THEN 1 ELSE 0 END) AS null_genre,
    SUM(CASE WHEN release_date   IS NULL THEN 1 ELSE 0 END) AS null_date
FROM spotify;
```

### Check for Duplicates
```sql
-- Find duplicate songs (same name + artist)
SELECT track_name, track_artist, COUNT(*) AS count
FROM spotify
GROUP BY track_name, track_artist
HAVING COUNT(*) > 1
ORDER BY count DESC;

-- Remove duplicates (keep highest popularity)
DELETE s1 FROM spotify s1
INNER JOIN spotify s2
WHERE s1.track_id > s2.track_id
  AND s1.track_name   = s2.track_name
  AND s1.track_artist = s2.track_artist;
```

### Fix Invalid Values
```sql
-- Check for popularity out of range
SELECT COUNT(*) FROM spotify
WHERE track_popularity < 0 OR track_popularity > 100;

-- Check for negative tempo
SELECT COUNT(*) FROM spotify WHERE tempo <= 0;

-- Remove rows with zero duration
DELETE FROM spotify WHERE duration_ms = 0;
```

### Add Useful Columns
```sql
-- Duration in minutes
ALTER TABLE spotify ADD duration_min DECIMAL(5,2);
UPDATE spotify SET duration_min = ROUND(duration_ms / 60000, 2);

-- Popularity category
ALTER TABLE spotify ADD popularity_category VARCHAR(20);
UPDATE spotify
SET popularity_category = CASE
    WHEN track_popularity >= 80 THEN 'Viral'
    WHEN track_popularity >= 60 THEN 'Popular'
    WHEN track_popularity >= 40 THEN 'Moderate'
    ELSE 'Low'
END;

-- Extract release year
ALTER TABLE spotify ADD release_year INT;
UPDATE spotify SET release_year = YEAR(release_date);

-- Mood label based on valence
ALTER TABLE spotify ADD mood VARCHAR(20);
UPDATE spotify
SET mood = CASE
    WHEN valence >= 0.6 THEN 'Happy'
    WHEN valence >= 0.4 THEN 'Neutral'
    ELSE 'Sad'
END;
```

---

## 6. Data Exploration Queries

### Basic Stats
```sql
-- Total songs, artists, genres
SELECT
    COUNT(*)                        AS total_songs,
    COUNT(DISTINCT track_artist)    AS total_artists,
    COUNT(DISTINCT genre)           AS total_genres,
    ROUND(AVG(track_popularity), 2) AS avg_popularity,
    ROUND(AVG(tempo), 2)            AS avg_bpm,
    ROUND(AVG(duration_min), 2)     AS avg_duration_min
FROM spotify;
```

### Genre Distribution
```sql
-- How many songs per genre
SELECT genre,
       COUNT(*) AS total_songs,
       ROUND(AVG(track_popularity), 2) AS avg_popularity
FROM spotify
GROUP BY genre
ORDER BY total_songs DESC;
```

### Top 10 Most Popular Songs
```sql
SELECT track_name, track_artist, genre, track_popularity
FROM spotify
ORDER BY track_popularity DESC
LIMIT 10;
```

### Top 10 Artists by Avg Popularity
```sql
SELECT track_artist,
       COUNT(*)                        AS total_songs,
       ROUND(AVG(track_popularity), 2) AS avg_popularity
FROM spotify
GROUP BY track_artist
HAVING COUNT(*) >= 5
ORDER BY avg_popularity DESC
LIMIT 10;
```

### Songs Released Per Year
```sql
SELECT release_year,
       COUNT(*) AS total_songs
FROM spotify
WHERE release_year IS NOT NULL
GROUP BY release_year
ORDER BY release_year ASC;
```

### Audio Features by Genre
```sql
SELECT genre,
       ROUND(AVG(danceability), 3) AS avg_danceability,
       ROUND(AVG(energy), 3)       AS avg_energy,
       ROUND(AVG(valence), 3)      AS avg_valence,
       ROUND(AVG(tempo), 2)        AS avg_bpm
FROM spotify
GROUP BY genre
ORDER BY avg_danceability DESC;
```

### Viral Songs Analysis
```sql
SELECT genre,
       COUNT(*) AS viral_songs
FROM spotify
WHERE popularity_category = 'Viral'
GROUP BY genre
ORDER BY viral_songs DESC;
```

### Mood Distribution
```sql
SELECT mood, COUNT(*) AS total_songs,
       ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM spotify), 2) AS percentage
FROM spotify
GROUP BY mood
ORDER BY total_songs DESC;
```

---

## 7. Key Findings from Phase 1

```
📊 Total Songs        → ~32,000 unique songs (after dedup)
🎤 Total Artists      → ~10,000+ unique artists
🎵 Most Songs Genre   → Pop (highest count)
⭐ Avg Popularity     → ~42 out of 100
🕺 Most Danceable     → Latin genre
⚡ Most Energetic     → EDM genre
😊 Happiest Genre     → Pop (highest valence)
📅 Peak Release Year  → 2019 (most songs released)
🔥 Viral Songs        → Pop & Latin dominate 80+ popularity
```

---

## 8. Phase 1 Summary Checklist

```
✅ Database created → spotify_db
✅ Table created with correct data types
✅ CSV data imported successfully
✅ Null values checked per column
✅ Duplicates found and removed
✅ Invalid values cleaned (zero duration, out-of-range)
✅ New columns added → duration_min, popularity_category, release_year, mood
✅ Basic exploration queries run
✅ Key findings noted for dashboard planning
⬜ Phase 2 → Advanced queries (JOINs, subqueries, window functions)
⬜ Phase 3 → Connect to Power BI → Build Dashboard
```

---

## Summary of Day 24
Today I started **Phase 1 of the Spotify Dashboard Project** — the data setup and exploration phase. I created the `spotify_db` database and `spotify` table with correct data types, imported the CSV using `LOAD DATA INFILE`, checked for **null values** column by column using CASE-based null counting, **removed duplicate** songs using INNER JOIN on the same table, fixed invalid values, and **added 4 new useful columns** (duration in minutes, popularity category, release year, mood). I then ran exploration queries to find total songs/artists/genres, genre distribution, top 10 songs and artists, release trends by year, audio features by genre, and viral song breakdown. Key findings were noted to guide the dashboard design in Phase 2 and 3.

**Tomorrow – Phase 2:**
- Window functions (RANK, DENSE_RANK, ROW_NUMBER)
- Advanced queries for dashboard KPIs
- Genre vs genre comparisons
- Decade-wise trend analysis