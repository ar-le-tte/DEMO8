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

---
## Data Rules & Preparation

### Attendance Rule
A learner is marked as **Attended = 1** if:
- **Minutes in Zoom session > 30**

This rule is applied before computing attendance rates and summaries.

### Data Shaping (recommended)
Data is loaded from the `data/` directory and cleaned into analysis-ready tables:
- Standardize learner identifier (use **email** consistently)
- Ensure dates are proper `Date` type
- Create a single assessment table by stacking labs + quizzes:
  - `email, cohort, track, week, assessment type, score`

---

## Data Model
The report is modeled using a star-schema approach:

**Dimensions**
- `Learners` (email, learner name, cohort, track)
- `Calendar Table` (Date, Month, Week, etc.)

**Facts**
- `Zoom Attendance`
- `Participation`
- `Assessments` (Labs + Quizzes combined)
- `Status` (Graduation + Certification)

**Relationships**
- `Learners[email]` → each fact table `[email]`
- `Calendar Table[Date]` → attendance/participation `[Date]`
- `Calendar Table[Week]` → assessments `[Week]` 
---

## Key DAX Calculations

### Total Learners

```DAX
Total Learners = DISTINCTCOUNT(Learners[email])
```


### Total Graduate

```DAX
Total Graduations = 
CALCULATE(
    COUNTROWS('Status of Participant'),
    'Status of Participant'[Graduation Status] = "Graduate"
)
```

### Graduation Rate

```DAX
Graduation Rate % = COALESCE(
DIVIDE(
    [Total Graduations],
    [Total Learners],
    0
), 0)
```

### Total Certified

```DAX
Total Certifications = 
CALCULATE(
    COUNTROWS('Status of Participant'),
    'Status of Participant'[Certification Status] = "Certified"
)
```

### Certification Rate

```DAX
Certification Rate % = COALESCE(
DIVIDE(
    [Total Certifications],
    [Total Learners],
    0
), 0) 
```
### Dropout Rate
```DAX
Total Dropouts = 
COALESCE(CALCULATE(
    COUNTROWS('Status of Participant'),
    'Status of Participant'[Graduation Status] = "Non Graduate"
), 0)
```
```DAX
Dropout Rate % = 
DIVIDE(
    [Total Dropouts],
    [Total Learners],
    0
) 
```

### Attendance Rate
```DAX
Learner Attendance % = 
VAR SessionsHeld =
    CALCULATE(
        DISTINCTCOUNT('Zoom Attendance'[Date]),
        REMOVEFILTERS('Zoom Attendance'[Email])
    )
VAR SessionsAttended =
    CALCULATE(
        DISTINCTCOUNT('Zoom Attendance'[Date]),
        'Zoom Attendance'[Attended] = 1
    )
RETURN
    DIVIDE(SessionsAttended, SessionsHeld)
```DAX
```DAX
Average Attendance % = COALESCE(
AVERAGEX(
    VALUES(Learners[email]),
    [Learner Attendance %]
), 0)
```


---
## How to Use

1. Open the `.pbix` inside Dashboard/
2. If data paths are broken, update them to point to your local data/ folder
3. Refresh the model
4. Use slicers to filter by cohort/track/week and explore:
    - engagement patterns
    - assessment performance
    - graduation/certification outcomes


## Tools Used

* Power BI Desktop
* Power Query
* Custom JSON Theme
