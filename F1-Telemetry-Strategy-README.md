# 🏎️ Formula 1 Performance & What-If Strategy Analytics Dashboard

An interactive, telemetry-inspired Power BI analytics dashboard designed to analyze Formula 1 historical race results, pit stop efficiency, driver/constructor standings, and simulate "What-If" strategy scenarios.

![F1 Dashboard Preview](screenshots/dashboard_preview.png) *(Upload your screenshot here)*

---

## 📌 Project Overview

Formula 1 is dictated by milliseconds, pit stop execution, and strategic adaptability. This project transforms multi-year F1 race telemetry data into an executive-ready BI control panel.

### Key Capabilities:
1. **Macro Season Scale Metrics**: Dynamic tracking of driver/constructor leaderboard dominance, win conversion rates, qualifying efficiency, and collision statistics.
2. **Pit Stop Efficiency Benchmarks**: Analytics on global grid pit stop durations across circuits.
3. **What-If Strategy Simulation**: Scenario modeling to quantify how pit stop optimizations alter championship points and standings.

---

## 🛠️ Tech Stack & Key Concepts

* **BI Platform**: Microsoft Power BI Desktop
* **Data Modeling**: Star Schema Architecture (Fact: `results`, `pit_stops` | Dim: `drivers`, `races`, `constructors`)
* **Analytics Engine**: Advanced DAX (Dynamic ranking, conditional branding, scenario parameters)
* **ETL**: Power Query (M Language) for duration formatting and schema transformation
* **UI/UX Design**: Custom Telemetry Dark Mode (`#0B131F`), Custom Slicers with red LED state indicators, and responsive team color formatting

---

## 📐 Key DAX Snippets

```dax
// Dynamic Leader Driver Identification
Overview_Leader_Driver = 
VAR TopDriverTable = 
    TOPN(1, VALUES('drivers'[code]), CALCULATE(SUM('results'[points])), DESC)
RETURN
    CONCATENATEX(TopDriverTable, 'drivers'[code], ", ")

// Leader Driver Total Wins Calculation
Overview_Leader_Wins = 
VAR TopDriver = 
    TOPN(1, VALUES('results'[driverId]), CALCULATE(SUM('results'[points])), DESC)
VAR LeaderWins = 
    CALCULATE(
        COUNTROWS('results'),
        'results'[positionOrder] = 1,
        TopDriver
    )
RETURN 
    IF(ISBLANK(LeaderWins), "0 Wins", LeaderWins & " Wins")
```

---

## 🚀 How to Explore

1. Clone the repository:
   ```bash
   git clone [https://github.com/YOUR_USERNAME/F1-Telemetry-Strategy-PowerBI.git](https://github.com/YOUR_USERNAME/F1-Telemetry-Strategy-PowerBI.git)
   ```
2. Open `F1_Race_Dashboard.pbix` in **Power BI Desktop**.
3. Use the **Year Slicer** on the left panel to dynamically explore seasons from 2018 to 2024.
