# Kansas Medicaid Analytics

This project looks at how Kansas Medicaid and CHIP enrollment changed over time and how those changes relate to unemployment trends.

## Data Sources

- CMS Medicaid and CHIP enrollment data
- U.S. Bureau of Labor Statistics (BLS) Public Data API

## What I Did

- Loaded and cleaned CMS Medicaid enrollment data
- Handled preliminary vs. final reporting records
- Pulled Kansas unemployment data using the BLS API
- Joined both datasets by reporting month
- Checked missing values and data quality
- Calculated enrollment trends and year-over-year changes
- Created simple visualizations for leadership-level insights

## Key Findings

- Kansas Medicaid/CHIP enrollment reached a low of about **370K in June 2019**
- Enrollment peaked at about **512K in April 2023**
- Enrollment increased about **38% from the 2019 low to the 2023 peak**
- Enrollment declined about **23% from the peak to June 2026**
- The correlation between unemployment and enrollment was weak at about **-0.28**, suggesting unemployment alone does not explain the enrollment trend

## Tools Used

Python, Pandas, Matplotlib, Google Colab, Google Drive, CMS public data, and BLS API.

## Project Files

- Colab notebook with the full workflow
- Final combined analytical dataset
- Enrollment and unemployment trend charts

## Note

This project is an exploratory analysis using public data. The findings show patterns and associations, not causal relationships.
