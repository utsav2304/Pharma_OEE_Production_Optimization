# Production Process & OEE Optimization (Excel + Power BI)

Analysis of production-line effectiveness for a pharmaceutical solid-dosage plant (tablets, capsules, blister packing) using **Overall Equipment Effectiveness (OEE)**, downtime Pareto, bottleneck identification, quality-loss analysis and an improvement what-if scenario.

> **Data disclosure:** all data in this repository is **simulated** for portfolio and learning purposes. It is not from any real plant or company. Realistic ranges and failure patterns were built into the simulation so the analysis has something meaningful to find.

## Problem statement

Analyze production-line performance using OEE, downtime, quality and capacity metrics to identify bottlenecks and recommend process improvements.

## Scope

| Item | Detail |
|---|---|
| Period | Jan - Jun 2026 |
| Lines | 4 (2 compression & coating, 1 capsule filling, 1 blister packing) |
| Products | 12 |
| Production runs | 1,663 (shift-level) |
| Downtime events | 9,706 |
| Defect records | 10,121 |

## Method

- **Availability** = Operating Time / Planned Production Time
- **Performance** = Ideal Time / Operating Time (Ideal Time = Total units / ideal rate)
- **Quality** = Fully Productive Time / Ideal Time (good units, time-weighted)
- **OEE** = Availability x Performance x Quality

OEE is aggregated **time-based**, so tablets, capsules and strips can be combined into one plant-level figure without mixing units.

## Workbook structure (`Pharma_OEE_Production_Analytics.xlsx`)

| Sheet | Purpose |
|---|---|
| Summary | Headline KPIs, auto-generated findings, charts |
| OEE_Analysis | OEE by line, line x shift, shift, month |
| Downtime_Analysis | Pareto of reasons, reason x line, machine ranking |
| Quality_Analysis | Defect Pareto, rejection by line and product |
| Scenario | What-if levers (breakdown, changeover, material shortage, rejects) |
| Assumptions | All parameters (blue = input) |
| Production_Log, Downtime_Log, Quality_Log | Fact tables (Power BI sources) |
| Line_Master, Machine_Master, Rate_Master | Dimension tables |

All analysis sheets are live formulas (SUMIFS, INDEX-MATCH, LARGE-based dynamic Pareto).

## Key findings

- Plant OEE is **71.2%** (Availability 84.8%, Performance 85.9%, Quality 97.8%) vs an 85% world-class benchmark.
- **Line 2** is the weakest line at 64.1% OEE; Line 3 is the strongest at 80.8%.
- **Breakdowns and minor stoppages cause 65%** of unplanned downtime (Pareto).
- **Tablet Press 2** is the bottleneck machine: 493 h of downtime, 26% of plant total, with a failure spike in April.
- **Shift C** is the weakest shift (65.9% OEE vs 73.9% for Shift A).
- Material shortage is the third-largest downtime cause; Line 4 shortage downtime more than doubles in May.
- Scenario (breakdowns -30%, changeovers -25%, material shortages -20%, rejects -20%) lifts plant OEE to about **73.6%**. This is a potential estimate, not a realised result.

## Power BI dashboard

Build steps, data model, relationships and DAX measures are in [`docs/PowerBI_Build_Guide_OEE_Project.md`](docs/PowerBI_Build_Guide_OEE_Project.md).

Planned pages: Plant Overview, OEE Analysis, Downtime & Bottleneck, Quality & Improvement.

<!-- Add screenshots to /images and uncomment these lines once the dashboard is built:
![Plant Overview](images/page1_plant_overview.png)
![Downtime & Bottleneck](images/page3_downtime_bottleneck.png)
-->

## How to use

1. Open `Pharma_OEE_Production_Analytics.xlsx` and start at the **Summary** sheet.
2. Change inputs (blue cells) in **Assumptions**, or levers (yellow cells) in **Scenario**; everything recalculates.
3. In Power BI Desktop: Get Data > Excel > load the six data sheets, then follow the build guide.

## Tools

Excel (formulas, Pareto, scenario analysis), Power BI (DAX, interactive dashboard), Python (used only to generate the simulated dataset).

## Author

Utsav Kumar Jaiswal - B.Tech, Production & Industrial Engineering, NIT Jamshedpur
