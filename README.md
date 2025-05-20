# Expenses_Analysis

## Short Description
This project involves the development of a personal expense tracking system that integrates data aggregation and visualization capabilities. Personal financial transactions are currently logged across multiple Google Spreadsheets. To streamline analysis, the project leverages Google Sheets API to programmatically extract and consolidate transaction data from these disparate sources into a unified dataset. The consolidated data is then imported into Power BI, where it is transformed into interactive dashboards and visualizations to facilitate insightful analysis of spending patterns and financial habits.

## Problem Statement
Managing personal finances effectively is crucial, especially in today’s cost-conscious environment. It’s easy to lose track of how spending fluctuates throughout the week, potentially leading to unintentional overspending during weekends or public holidays when routines change.

This project aims to analyze my personal expense data to gain a clear understanding of how my spending habits differ on weekdays, weekends, and Singapore public holidays. By identifying these patterns, I can:

* Detect days or periods when I tend to spend more than usual

* Pinpoint categories where spending may be less controlled

* Monitor my financial health more closely by recognizing behavioral triggers of overspending

* Make informed adjustments to budgeting and spending habits to ensure my finances remain balanced and sustainable

The goal is to use data-driven insights to take control of my financial status, avoid surprises, and build better money management habits that align with my financial goals.

## ETL Process
The ETL process will consist of data ingestion (through the use of Google API). There will be no transformation required as transaction data is well-formatted and ready for consumption as a Single Source of Truth (SSOT)

>[!NOTE]
>Refer to 'Google_API.md' for technical documentation

## Data Analytics
* MS PowerBI - a business analytics service by Microsoft that provides interactive visualizations and business intelligence capabilities with an easy-to-use interface for end users to create their own reports and dashboards.
>[!IMPORTANT]
> The SSOT will be directly imported into PowerBI through the Google Sheet connector found in PowerBI.

>[!NOTE]
> Refer to 'Data_Analysis.md' for the next part
