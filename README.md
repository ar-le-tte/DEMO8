# Dare Careers –  Power BI Dashboard for Tracking Student Progress and Performance.

## Overview
This project contains a Power BI dashboard built to help **Dare Careers** monitor learner engagement and performance across a **10-week** training program (Tracks: **Power BI** and **AWS Cloud**).

The dashboard focuses on:
- Attendance compliance (Zoom sessions)
- Daily participation
- Weekly quizzes and labs
- Graduation and certification outcomes

It is designed to support program managers and trainers in spotting engagement trends and identifying learners who may need additional support.

---

# Project Structure

```
DEMO8/
├── Dashboard/
│   └── Dare_Careers_Dashboard.pbix
├── data/
│   ├── Cloud Training/
│   │   ├── Labs & Quizzes/
│   │   ├── Participation/
│   │   ├── Status of Learners/
│   │   └── Zoom Attendance/
│   └── PowerBI Training/
│       ├── Labs & Quizzes/
│       ├── Participation/
│       ├── Status of Learners/
│       └── Zoom Attendance/
└── Page Screenshots/
    ├── Page-1-Performance-Overview.png
    └── Page-2-Learner-Insights.png
```

---

## Dashboard Pages

The report contains **two main pages**:

- **Overview** (program-level performance)
- **Learner Insights** (learner-level engagement and scores)

A consistent set of slicers at the top allows users to filter results across both pages.

### Global Filters (Top Slicers)
- **Graduation Status**
- **Learner Status**
- **Track** (Power BI / AWS Cloud)
- **Cohort**
- **Week**
- **Date Range** (Program timeline)

---

### Page 1 — Overview (Performance Overview)
![Performance Overview](Page%20Screenshots/Page-1-Performance-Overview.png)

This page provides a program-level summary of outcomes and engagement.

#### KPI Cards
- **Total Learners**
- **Total Certifications**
- **Certification Rate (%)**
- **Total Graduations**
- **Dropout Rate (%)**
- **Total Dropouts**

#### Visuals
- **Graduations by Cohorts** (bar)
- **Dropout Rate (%) by Cohort and Track** (clustered columns)
- **Average Attendance % by Cohort** (bar)
- **Certification Rates by Cohort** (bar)
- **Average Score by Assessment Type (Lab vs Quiz)** (bar)
- **Attendance vs Participation Rate** (comparison bar)

#### Summary Table
- **Performance Details** table showing, by Track:
  - Graduation Rate %
  - Certification Rate %
  - Average Assessment Score

---

### Page 2 — Learner Insights (Key Learner Insights)
![Learner Insights](Page%20Screenshots/Page-2-Learner-Insights.png)
This page focuses on learner-level engagement, weekly trends, and detailed performance.

#### KPI Cards
- **Total Labs**
- **Learner Avg Labs Completed**
- **Total Class Hours**
- **Average Attendance (%)**
- **Average Assessment Score**
- **Average Participation (%)**

#### Visuals
- **Attendance Trend by Week** (line chart)
- **Weekly Average Assessment Score (/100)** (horizontal bar chart)

#### Learner Search + Filters
- A **search box** (“Enter Name”) to quickly locate a learner
- **Assessment Type** slicer (Lab / Quiz)

#### Detailed Table (Learners Performance Details)
A detailed learner table including:
- Name
- Track
- Cohort
- Total Hours in Class
- Average Participation %
- Average Attendance %
- Average Score


