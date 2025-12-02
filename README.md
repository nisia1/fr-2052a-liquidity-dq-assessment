# fr-2052a-liquidity-dq-assessment
FR 2052a liquidity reporting – data quality and transformation logic assessment using SQL, Python, and Power BI.

Project Overview

This project simulates a real-world FR 2052a liquidity reporting governance environment to evaluate data quality, bucket transformation accuracy, and trade-level exceptions across a synthetic dataset of liquidity transactions.

The workflow mirrors how Regulatory Reporting Governance, Internal Audit, and Data Quality Oversight teams review, validate, and escalate issues that impact liquidity reporting accuracy.

Tools & Technologies

Python (Pandas) – Data ingestion, DQ flag creation, export

SQL (SQLite) – Data quality checks, mismatch validation

Power BI – Executive dashboard & drilldown diagnostics

Excel – Initial data exploration

GitHub – Project versioning & documentation

Dataset Description

Synthetic dataset of 500 records representing typical liquidity trade activity.

Fields include:

ProductType

DaysToMaturity

LiquidityBucket_Label (Assigned)

ExpectedBucket

Amount

SourceSystem

Data Quality Flags (generated in Python)

Data Quality Rules Implemented (SQL-Based)
1. Missing Liquidity Bucket

Flags trades with null or blank LiquidityBucket_Label.

2. Negative Amount Check

Identifies economically invalid transactions.

3. Missing Source System

Detects deficiencies in upstream lineage or enrichment.

4. Liquidity Bucket Misclassification

Compares Assigned vs Expected bucket based on DaysToMaturity.

5. Row-Level Issue Aggregation

Creates DQ_HasIssue to consolidate all rule failures.

Key DQ Results

| Data Quality Issue          | Count   |
| --------------------------- | ------- |
| Bucket Mismatch             | **385** |
| Missing Liquidity Bucket    | **19**  |
| Missing Source System       | **17**  |
| Negative Amount             | **32**  |
| Total Records With ≥1 Issue | **399** |

Dashboard Overview (Power BI)

The dashboard contains two pages structured like a real regulatory reporting review.

## Tab 1 — Liquidity Overview Dashboard

![Liquidity Overview](images/tab1_overview_dashboard.png
.png)


This dashboard highlights…

Purpose: Executive-level diagnostic of reporting quality.

Visuals:

KPI Cards (Total Records, Issues, Bucket Mismatch Count)

Assigned vs Expected Liquidity Bucket Heatmap

Total Records by Product Type

Insight:
Significant off-diagonal activity indicates bucket transformation logic issues, particularly for long-dated trades incorrectly mapped into shorter-term buckets.

## Tab 2 — Trade-Level Data Quality Drilldown

![Trade-Level Drilldown](images/tab2_overview_dashboard.png
.png)

Purpose: Detailed investigation and root cause analysis.

Visuals:

Bucket Mismatches by Liquidity Bucket (Bar Chart)

Trade-Level Exception Table

Product Type Slicer

Insight:
Misclassifications are concentrated in 31–90D, 91–365D, and >365D expected buckets—suggesting transformation logic or upstream data enrichment weaknesses.

The drilldown table provides trade-level evidence required for issue management, internal audit testing, and regulatory review.

Key Insights & Business Impact
1. Transformation Logic Issues

Long-dated trades frequently map to incorrect liquidity buckets, affecting the reporting maturity profile in FR 2052a.

2. Product-Level Variability

Securities financing products show higher mismatch variability, indicating inconsistent mapping logic across systems.

3. Upstream Data Quality Gaps

Missing bucket assignments and missing source systems point to enrichment or lineage deficiencies.

4. Regulatory Risk & Control Impact

These findings would influence:

Liquidity risk measurement

LCR / NSFR interpretations

Supervisory expectations for data integrity

Regulatory issue management and remediation planning

Repository Contents

liquidity_data_clean.csv — Clean dataset

liquidity_with_dq_flags.csv — DQ-enhanced dataset

2052A_DQ_Checks.ipynb — Python notebook

sql_queries.sql — All DQ SQL rules

Liquidity_Reporting.pbix — Full Power BI dashboard

README.md — Project documentation
