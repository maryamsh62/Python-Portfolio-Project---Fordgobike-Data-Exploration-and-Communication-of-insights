# Ford GoBike Data Exploration & Insight Visualization

This repository documents a two-part exploration of the **2017 Ford GoBike (now Bay Wheels)** bike-sharing trip data. The work was completed as a capstone-style project to demonstrate how **systematic data wrangling** and **effective visualization** can reveal usage patterns, user behavior, and operational insights in a real urban mobility system.

---

## 1. Project Structure

This project has **two main parts**:

1. **Exploratory Data Analysis (EDA)**  
   In this phase, the original trip data (`2017-fordgobike-tripdata.csv`) was cleaned, enriched with time features, and explored from univariate to multivariate levels using Python visualization libraries.

2. **Communicating the Findings**  
   In the second phase, the most compelling patterns were turned into presentation-ready visualizations and organized into an HTML slide deck (reveal.js) to tell a clear story about rider behavior.

---

## 2. Dataset Overview

**Context.**  
Ford GoBike (now **Bay Wheels**) is the first large-scale bike-sharing system on the U.S. West Coast. As of January 2018, it operated ~2,600 bikes across more than 260 stations in the San Francisco Bay Area (San Francisco, East Bay, and San Jose). The system was launched as Ford GoBike on **June 28, 2017** and later rebranded to **Bay Wheels** after Lyft’s acquisition of Motivate in 2019.

**Data source.**  
The original data file used in this project:

- **`2017-fordgobike-tripdata.csv`**  
- Covers trips from **June 28, 2017 to December 31, 2017**  
- Publicly available from Bay Wheels system data:  
  https://www.lyft.com/bikes/bay-wheels/system-data

**Data contents.**  
The dataset contains **~519,700 anonymized trips**, each with:

- Start/end times  
- Start/end station locations  
- Trip duration  
- Rider type (`Subscriber` vs `Customer`)  
- Basic demographics (in original raw data)

This volume and structure make it ideal for temporal, behavioral, and operational analysis.

---

## 3. Data Cleaning & Feature Engineering (`fordgobike-tridata_clean.csv`)

To make the dataset suitable for bi- and multivariate analysis, several cleaning steps were applied:

1. **Outlier handling**  
   - Trip duration was filtered using a Z-score rule of **|z| > 5**.  
   - This effectively removed extreme trips, resulting in an upper bound of **~44 minutes** for `duration_min`.  
   - Rationale: the bulk of bike-share usage is short and urban; keeping extreme values would distort distributions and visualizations.

2. **Time-based feature creation**  
   From the trip start time, the following engineered features were added to enable temporal usage analysis:
   - `start_hour_of_day` (0–23)
   - `start_day_of_week` (Monday–Sunday)
   - `start_month`

3. **Data type fixes**  
   Some columns were converted to appropriate types (e.g. datetime) to support grouping and plotting.

**Key variables used throughout the analysis:**

- `user_type` — `"Subscriber"` or `"Customer"`
- `duration_min` — trip duration in minutes
- `start_date`
- `start_hour_of_day`
- `start_day_of_week`
- `start_month`

The cleaned dataset was saved as:

- **`fordgobike-tridata_clean.csv`**

---

## 4. Exploratory Findings (Part 1)

The EDA focused on understanding **who uses the system, when they use it, and how long they ride**. The core insight that emerged is that **Subscribers and Customers exhibit clearly different behavior patterns**.

### 4.1 User-Type Behavior

- **Subscribers**  
  - Ride mostly on **weekdays**  
  - Show clear **commute peaks** (8–9 AM and 5–6 PM)  
  - Have **shorter trips** on average (≈ **10 minutes**)
  - Likely using the service for **work/school commuting**

- **Customers** (casual users / non-members)  
  - Ride more on **weekends**  
  - Have **longer trips** (≈ **18 minutes**, about **2×** Subscribers)  
  - Weekend trips (Sat/Sun) are about **10% longer** than weekday trips  
  - Likely using the service for **recreational / tourist** purposes  
  - Highest activity window: **12 PM–5 PM on weekends**

### 4.2 Temporal Patterns

- Usage across the week shows a **strong 7×24 structure**:
  - Weekdays: strong AM and PM commute peaks (especially for Subscribers)
  - Weekends: flatter but higher mid-day usage (especially for Customers)

- This pattern becomes most visible in **heatmaps** of:
  - `start_day_of_week` × `start_hour_of_day`
  - Segmented by `user_type`

### 4.3 Location Effects

- Certain **destination stations** show **significantly higher trip durations**, especially:
  - **“The Embarcadero at Sansome St”**  
  - Likely due to being in a **touristic/recreational** area  
  - This supports the hypothesis that **trip purpose** and **end-location** influence trip duration

---

## 5. Key Insights for Presentation (Part 2)

The second part of the project focuses on **communicating** the analysis results. The selected visualizations tell a progressive story:

1. **User type distribution**  
   - Bar chart comparing total trips by `user_type`
   - Shows the system is **dominated by Subscribers**, but Customers are an important segment with different behavior

2. **Trip duration by user type**  
   - Side-by-side histograms or boxplots  
   - Makes the **“Customers ride longer”** insight immediately visible

3. **Weekly usage heatmaps**  
   - 7 (days) × 24 (hours) heatmaps for **each** user type  
   - Reveals:
     - Commute pattern for Subscribers
     - Leisure/tourist pattern for Customers

4. **Trip duration by day and destination**  
   - Clustered bar chart of **average trip duration** by **start day of week** for **top 10 end stations**  
   - Shows that **where** a trip ends can be as important as **when** it starts

**Presentation file:**  
- `2_slide_deck_GoBikes_by_DirkKadijk1.0.slides.html`  
- Built from a Jupyter Notebook using **reveal.js**  
- Navigation: use arrow keys (← → ↑ ↓), press **ESC** for overview

---

## 6. Files in This Project

- 2017-fordgobike-tripdata.csv                # Original raw dataset (source: Bay Wheels)

- fordgobike-tridata_clean.csv                # Cleaned and feature-enriched dataset

- exploration_GoBikes_by_DirkKadijk1.0.ipynb  # Notebook with full EDA (part 1)

- 2_slide_deck_GoBikes_by_DirkKadijk1.0.slides.html  # Presentation (part 2)

- README.md
