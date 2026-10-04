# kansas-medicaid-analytics

# Kansas Medicaid & CHIP Enrollment Analytics

## Project Overview

This project analyzes **Kansas Medicaid and CHIP enrollment trends** using multiple public data sources.

The goal is to demonstrate an end-to-end analytics workflow that includes:

- Data acquisition from different sources
- Data cleaning and validation
- Handling preliminary and final records
- Missing-value treatment
- Data integration
- Trend analysis
- Statistical analysis
- Visualization
- Leadership-focused interpretation

The project was built in **Google Colab using Python**.

---

## Business Question

The primary question explored was:

> **How has Kansas Medicaid and CHIP enrollment changed over time, and how do those changes relate to Kansas unemployment trends and major Medicaid policy periods?**

The analysis focuses on the period from **June 2017 through June 2026**.

---

## Data Sources

### 1. CMS Medicaid & CHIP Data

**Source:** Centers for Medicare & Medicaid Services (CMS)

Dataset includes monthly state-level information such as:

- Medicaid and CHIP enrollment
- Medicaid enrollment
- CHIP enrollment
- Applications
- Eligibility determinations
- Processing-time measures
- Operational metrics

Data was obtained as a **CSV file** from the CMS Medicaid public data portal.

### 2. Bureau of Labor Statistics

**Source:** U.S. Bureau of Labor Statistics

**Series:** Kansas seasonally adjusted unemployment rate

**Acquisition method:** BLS Public Data API

The API returned monthly unemployment data in JSON format, which was converted into a pandas DataFrame and integrated with the CMS data.

---

## Project Workflow

```text
CMS Medicaid CSV
       |
       v
Data profiling and validation
       |
       v
Select best available state-month record
       |
       v
Kansas Medicaid analytical dataset
       |
       +------------------+
                          |
BLS Public Data API      |
       |                  |
       v                  |
JSON -> DataFrame         |
       |                  |
       v                  |
Clean unemployment data  |
       |                  |
       +---------> Join by Reporting Month
                          |
                          v
               Final analytical dataset
                          |
                          v
               Analysis and visualization
```

---

## Data Cleaning & Validation

Several data-quality checks were performed before analysis.

### CMS reporting versions

The CMS dataset included both:

- `P` — Preliminary records
- `U` — Updated records

The `Final Report` field showed:

- Preliminary records → `N`
- Updated records → `Y`

The analysis therefore prioritized the **final/updated record** for each state and reporting month.

If only a preliminary record was available, it was retained as the best available observation.

### Duplicate validation

The raw CMS dataset contained:

- **11,118 rows**
- **0 completely duplicated rows**

After selecting one best available record per state-month:

- **5,610 unique state-month records remained**
- **0 duplicated state-month combinations**

### Kansas analytical period

Kansas contained an isolated September 2013 observation followed by a gap.

To avoid presenting a misleading continuous trend, the primary analysis uses the continuous monthly period beginning in:

**June 2017**

### BLS missing value

The BLS unemployment dataset contained one missing observation:

**October 2025**

The original missing value was preserved, and a separate analytical field was created using **linear interpolation** between September and November 2025.

An imputation flag was also retained for transparency.

---

## Key Findings

### Enrollment changed substantially during the study period

Kansas Medicaid and CHIP enrollment reached:

- **Lowest enrollment:** 370,030 in June 2019
- **Highest enrollment:** 512,005 in April 2023

Enrollment increased by:

**141,975 people (+38.37%)**

from the lowest point to the peak.

---

### Enrollment declined after the April 2023 peak

By June 2026, enrollment had declined to:

**393,912**

This represents a decline of:

**118,093 people (-23.06%)**

from the April 2023 peak.

---

### Year-over-year enrollment changed significantly across policy periods

Average year-over-year enrollment change:

| Period | Average YoY Change |
|---|---:|
| Before March 2020 | -2.60% |
| March 2020 – March 2023 | +9.70% |
| April 2023 onward | -6.19% |

The largest year-over-year increase was:

**+15.44% in March 2021**

The largest year-over-year decline was:

**-15.78% in June 2024**

---

### Unemployment alone did not explain enrollment trends

The correlation between Kansas unemployment and Medicaid/CHIP enrollment was approximately:

**-0.28**

This indicates only a weak negative linear relationship.

Unemployment increased sharply during the beginning of the pandemic but later declined, while Medicaid enrollment continued increasing for several years.

This suggests that unemployment alone does not explain the enrollment trend.

The timing of enrollment changes also aligns with the pandemic-era Medicaid continuous-enrollment period and the later resumption of regular eligibility renewals.

This analysis identifies associations and timing patterns but does **not establish causation**.

---

## Visualizations

The project includes three primary visualizations:

1. **Kansas Medicaid and CHIP Enrollment Trend**
2. **Kansas Unemployment Rate Trend**
3. **Kansas Medicaid and CHIP Year-over-Year Enrollment Change**

These visuals are stored in the `charts/` directory.

---

## Repository Structure

```text
kansas-medicaid-analytics/
│
├── notebook/
│   └── 01_Kansas_Medicaid_Data_Pipeline.ipynb
│
├── data/
│   └── kansas_medicaid_bls_combined.csv
│
├── charts/
│   ├── kansas_medicaid_enrollment_trend.png
│   ├── kansas_unemployment_trend.png
│   └── kansas_enrollment_yoy_change.png
│
└── README.md
```

---

## Tools & Technologies

- Python
- Google Colab
- Pandas
- Matplotlib
- BLS Public Data API
- JSON
- CSV
- Google Drive
- GitHub

---

## Analytical Concepts Demonstrated

This project demonstrates:

- Multi-source data acquisition
- REST API integration
- Data profiling
- Missing-value handling
- Duplicate validation
- Data reconciliation
- Date transformations
- Data integration and joins
- Time-series analysis
- Year-over-year calculations
- Correlation analysis
- Data visualization
- Analytical interpretation
- Data-quality documentation
- Communicating findings to non-technical stakeholders

---

## Limitations

This analysis has several important limitations:

- The analysis uses publicly available aggregate state-level data.
- Correlation does not establish causation.
- Medicaid enrollment is influenced by multiple factors beyond unemployment.
- Policy changes, eligibility rules, administrative processes, and demographic factors were not modeled directly.
- One unemployment observation was interpolated for analytical continuity.
- Some CMS operational fields had limited historical reporting availability and were therefore not used as primary metrics.

---

## Potential Next Steps

With additional time, the project could be expanded by:

- Adding state-to-state comparisons
- Incorporating demographic and economic indicators
- Analyzing Medicaid application and eligibility-processing trends
- Adding county-level public health data
- Developing predictive or anomaly-detection models
- Building an interactive Power BI dashboard
- Evaluating additional policy periods and lag relationships

---

## Purpose

This project was developed as a practical healthcare analytics case study demonstrating how public healthcare and economic data can be transformed into clear, reproducible, leadership-focused insights.
