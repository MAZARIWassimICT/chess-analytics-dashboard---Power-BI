# Chess Games Dashboard (Lichess) - Power BI Project

An interactive Power BI report analyzing **20,000 real chess games played on Lichess.org**, exploring player behavior, openings strategy, and time management across rated and casual games.

**File:** `chess_games_dashboard_-_FinalVersion.pbix`
**Tool:** Microsoft Power BI Desktop

---

## Data Source

- **Dataset:** [Online Chess Games](https://mavenanalytics.io/data-playground/online-chess-games) - sourced from **Maven Analytics**
- **Volume:** ~20,000 individual chess games on Lichess
- **Original fields include:** game ID, rated (Y/N), start/end time, number of turns, victory status, winner, time_increment, white/black player IDs and ratings, move list, opening ECO code, opening name, and opening ply

---

## Process Overview

The project followed a complete BI workflow, from CSV raw data to a polished, interactive report:

`Cleaning , Transformation , Modeling , Visualization , Design`

### 1. Cleaning
- Removed/handled inconsistent, duplicate, and null records
- Standardized categorical text fields (e.g., winner, victory status, rating class)

### 2. Transformation
Key derived/calculated columns built with Power Query and DAX to enrich the raw dataset:
- **`who won?`** - the higher-rated or the lower-rated
- **`game_type (Lichess standards)`** - reclassifies games into Lichess's official speed categories (Blitz, Rapid, Classical) based on time control
- **`increment (s)`** and **`time_without_increment (min)`** - split from the raw Lichess increment code (e.g., `15+10`) into separate numeric fields for base time and increment
- **"opening_response" : Replaced value "Refused" to "Declined"
- **`turns (bins)`** - bucketed game length for distribution analysis
- **Gambit flags** - dedicated fields identifying Queen's Gambit, King's Gambit, and Elephant Gambit games
- **Created a hierarchy of: opening_shortname ___opening_variation
- **Replaced values in many columns

### 3. Modeling
A star-schema style data model with two core tables:
- **`chess_games`** - fact table (one row per game): ratings, turns, timing, opening, outcome
- **`player`** - dimension table tracking `player_id` with a hierarchy for **total games**, **games played as White**, and **games played as Black**

Custom DAX measures include:
- `Avg Rating`, `Max Rating`, `Min Rating`
- `Corr Time_Turns`, `Corr Increment_Turns`, `Corr Time_Increment` - correlation measures between time controls and game length
- `QG Games`, `QG Rate`, `QG Wins` - Queen's Gambit performance
- `KG Games`, `KG Rate`, `KG Wins` - King's Gambit performance
- `EG Games`, `EG Rate`, `EG Wins` - Elephant Gambit performance

### 4. Visualization
Charts and visuals built to answer key questions about game patterns and time control (see **Report Pages** below).

### 5. Design
- Custom color theme and background imagery (branded "Chess Analytics" theme)
- Icon/image assets for featured openings (Sicilian Defence, French Defence, Italian Game, Queen's Pawn Game)
- Interactive **navigation buttons** across all pages for a seamless, app-like user experience
- KPI cards, gauges, and slicers for guided filtering

---

## Report Pages

### 1. Overview
A high-level summary of the dataset:
- Win rate by color (White vs. Black)
- Win rate by rating group
- Game type breakdown (Bullet / Blitz / Rapid / Classical)
- Game category waterfall (rated vs. casual, decisive vs. draw, etc.)
- Top players by number of games played
- Overview for the rating included in the dataset

### 2. Openings
A deep dive into opening theory and its impact on results:
- Most played openings (by game count)
- Win rate of the most popular openings
- Gauge visuals and win-rate table tracking performance of the **Queen's Gambit**, **King's Gambit**, and **Elephant Gambit**
- Slicers to filter by game type and winner
- Visual gallery of featured openings (Sicilian Defence, French Defence, Italian Game, Queen's Pawn Game)

### 3. Time Management
Analysis of how time controls relate to gameplay:
- Average number of turns by victory status (checkmate, resignation, time-out, draw)
- Time control distribution and its relationship with game length (line/column combo charts)
- Correlation visuals between base time, increment, and number of turns
- KPI card and supporting breakdowns
---

## Key Insights the Dashboard Enables
- Does playing White or Black give a real advantage?
- Which openings have the highest play rates, are they usefull? , and are famous aggressive gambits (King's, Queen's, Elephant) actually worth it?
- How do time controls (Blitz vs Rapid vs Classical) affect how long games last by turns?
- Do higher-rated players behave differently in terms of openings and game length?
- Who are the most active players in the dataset?
--many more--
---

## How to Use
1. Open `chess_games_dashboard_-_FinalVersion.pbip` in **Power BI Desktop** (free download from Microsoft).
2. Use the on-report navigation buttons to move between the **Overview**, **Openings**, and **Time Management** pages.
3. Use slicers (game type, winner) to filter the visuals interactively.
4. Hover over charts and gauges for tooltips with exact figures.

---

## Credits
- **Data:** Maven Analytics - Online Chess Games (+20K games)
- **Report design & analysis:** Built end-to-end in Power BI (Power Query, DAX, and custom report design)
