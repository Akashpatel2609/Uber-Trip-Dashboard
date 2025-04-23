## 🚖 Uber Trip Analysis Dashboards

**Objective:**  
Analyze Uber trip data in Power BI to surface booking trends, revenue metrics, trip efficiency and location insights—enabling stakeholders to make data-driven decisions.

---

### 📊 Dashboard 1: Overview Analysis

**Key Questions & KPIs**  
| KPI                         | Definition                                                         |
|-----------------------------|--------------------------------------------------------------------|
| **Total Bookings**          | Number of trips booked over a selected period                      |
| **Total Booking Value**     | Sum of revenue from all bookings                                   |
| **Average Booking Value**   | Total Booking Value ÷ Total Bookings                               |
| **Total Trip Distance**     | Sum of distances covered by all trips                              |
| **Average Trip Distance**   | Total Trip Distance ÷ Total Bookings                                |
| **Average Trip Time**       | Mean duration of all trips                                         |

**Expected Outcomes**  
- Identify ride-booking and revenue trends  
- Assess trip efficiency (distance vs. duration)  
- Compare metrics across time windows  
- Inform pricing optimizations and customer-experience improvements  

**Visuals & Interactivity**  
1. **Measure Selector**  
   - Disconnected table values: `Total Bookings` | `Total Booking Value` | `Total Trip Distance`  
   - Dynamic measures drive all visuals and chart titles.  
2. **Breakdowns**  
   - By Payment Type (Card, Cash, Wallet)  
   - By Trip Type (Day vs. Night)  
3. **Vehicle-Type Grid**  
   - Matrix shows KPIs by vehicle category  
   - Conditional formatting highlights extremes  
4. **Daily Booking Trends**  
   - Line/area chart of bookings per day  
   - Annotate peaks (holidays, events)  
5. **Location Analysis**  
   - Top 5 pickup & drop-off points  
   - Most-preferred vehicle by pickup location  
   - “Farthest trip” identification  

**UX Enhancements**  
- **Dynamic Title**: Reflects selected measure  
- **Slicers**: Date, City, Payment Type, Trip Type  
- **Tooltips**: Show secondary KPIs  
- **Bookmarks**:  
  - _Data Details_ (metric definitions, data sources)  
  - _Clear Filters_ button (resets slicers)  
- **Download Raw Data** button via Power Automate

---

### ⏱️ Dashboard 2: Time Analysis

**Purpose:** Reveal intraday and weekday/weekend demand patterns.  

| Visualization                     | Description                                                       |
|-----------------------------------|-------------------------------------------------------------------|
| **Area Chart** by 10-min interval | Bookings grouped in 10-minute slices                               |
| **Line Chart** by Day Name        | Trends Mon – Sun                                                  |
| **Heatmap (Matrix)**              | Hours (0–23) × Days (Mon–Sun), colored by dynamic measure         |

**Global Dynamic Measure**  
– Same selector as Dashboard 1 drives all three visuals.

---

### 🔍 Dashboard 3: Details Tab

**Purpose:** Enable drill-through to raw trip records for granular analysis.

- **Grid Table**:  
  Displays fields such as Trip ID, Date, Time, Pickup/Drop-off, Distance, Duration, Fare, Payment Type, Vehicle Type  
- **Drill-Through**:  
  Right-click any data point in Charts/Heatmap → “Drill through” → Details Tab  
- **Bookmarks**:  
  - _View Full Data_ toggles between filtered and unfiltered record sets  

---

## 🛠️ Power BI Implementation Highlights

1. **Data Model**  
   - Fact table: Trips (with measures for distance, fare, time)  
   - Dimensions: Date, Time, Vehicle, Location, Payment Type  
   - Inactive relationship between Pickup and Drop-off locations (activated via DAX when needed)  
2. **DAX Measures**  
   - Dynamic‐measure SWITCH based on selector  
   - Time‐binning for 10-minute intervals:  
     ```DAX
     Interval10Min = 
       FLOOR(
         HOUR([TripTime])*60 + MINUTE([TripTime]),
         10
       ) & "–" & FLOOR(
         HOUR([TripTime])*60 + MINUTE([TripTime]),
         10
       ) + 9
     ```
3. **Interaction & UX**  
   - Sync slicers across pages  
   - Clear Filters button with Action = “Reset to Default”  
   - Export button leveraging Power Automate flow  

---

