# Question by Gemini for PowerBI

>[!NOTE]
> There're two tables - 'Date Table' & 'Expenses'

>[!IMPORTANT]
> The dashboard applies a filter according to the selected **Month** & **Year** by default

I. Basic Data Exploration & Summarization (Getting Started):

- [x] What's my total spending for a given period (e.g., this month, last month, this year)? (Measures, DAX SUM function)
<details>
   <summary>Total Expenses for the month</summary>
   Using DAX Measure - To find the total for the month

```
ThisMonthTotalExpenses = 
VAR TotalExpenses = SUM(Expenses[Amount])
RETURN
TotalExpenses
```

>Use the two slicers to change the Month and Year

</details>

- [ ] What's my average daily/weekly/monthly spending? (Measures, DAX AVERAGE function)
<details>
   <summary>Daily Average for the Month</summary>
  Invoking the 'Average()' function doesn't work as each day's expenses are broken down to different rows.
  
  Instead, we will need to further processing to refine the table with two possible approaches.

 <details>
   <summary>Using PowerQuery</summary>
   Performs a GROUPBY function to group all transactions according to the date.

```
let
    Source = Expenses,
    #"Grouped Rows" = Table.Group(Source, {"Date"}, {{"GroupBy Amount", each List.Sum([Amount]), type nullable number}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Grouped Rows",{{"GroupBy Amount", Currency.Type}}),
    #"Duplicated Column" = Table.DuplicateColumn(#"Changed Type", "Date", "Date - Copy"),
    #"Duplicated Column1" = Table.DuplicateColumn(#"Duplicated Column", "Date", "Date - Copy.1"),
    #"Duplicated Column2" = Table.DuplicateColumn(#"Duplicated Column1", "Date", "Date - Copy.2"),
    #"Extracted Day" = Table.TransformColumns(#"Duplicated Column2",{{"Date - Copy", Date.Day, Int64.Type}}),
    #"Extracted Month Name" = Table.TransformColumns(#"Extracted Day", {{"Date - Copy.1", each Date.MonthName(_), type text}}),
    #"Extracted Year" = Table.TransformColumns(#"Extracted Month Name",{{"Date - Copy.2", Date.Year, Int64.Type}}),
    #"Changed Type1" = Table.TransformColumnTypes(#"Extracted Year",{{"Date - Copy.2", Int64.Type}}),
    #"Duplicated Column3" = Table.DuplicateColumn(#"Changed Type1", "Date", "Date - Copy.3"),
    #"Extracted Month" = Table.TransformColumns(#"Duplicated Column3",{{"Date - Copy.3", Date.Month, Int64.Type}}),
    #"Added Custom" = Table.AddColumn(#"Extracted Month", "Custom", each ((([#"Date - Copy.2"]*100) + [#"Date - Copy.3"]) * 100) + [#"Date - Copy"]),
    #"Changed Type2" = Table.TransformColumnTypes(#"Added Custom",{{"Custom", Int64.Type}, {"Date - Copy.2", type text}}),
    #"Renamed Columns" = Table.RenameColumns(#"Changed Type2",{{"Date - Copy", "Day"},{"Date - Copy.1", "Month"},{"Date - Copy.2", "Year"},{"Date - Copy.3", "Month_Num"},{"Custom", "DateKey"}}),
    #"Reordered Columns" = Table.ReorderColumns(#"Renamed Columns",{"Date", "GroupBy Amount", "Day", "Month_Num", "Month", "Year"})
in
    #"Reordered Columns"
```
</details>

<details>
  <summary>Using DAX Measure</summary>
  Invoke the AVERAGE() function on the [GroupBy Amount] column to the average per day.

```
DailyAverageExpenses = 
VAR SelectedMonth = SELECTEDVALUE('Expenses'[Month]) // get the value from the month slicer
VAR SelectedYear = SELECTEDVALUE('Expenses'[Year]) // get the value from the year slicer
RETURN

CALCULATE(
    AVERAGE('GroupBy Table'[GroupBy Amount]),
    'GroupBy Table'[Month] = SelectedMonth,
    'GroupBy Table'[Year] = SelectedYear
)
```
</details>
</details>

<details>
   <summary>Weekly Average for the Month</summary>
   One Approach is to create a table grouping records based on the **week of the month**. However, this is not recommended because this is not efficient.

<details>
  <summary>Using PowerQuery</summary>
   
```

```

</details>

<details>
  <summary>Using DAX Measure</summary>
   
```

```

</details>

</details>

- [ ] How much did I spend in each category (e.g., food, transportation, entertainment)? (Visualizations like bar charts, pie charts; grouping and aggregation)
- [ ] What are my top 5 expense categories? (Sorting, Top N filters)
- [ ] How does my spending vary by day of the week or month? (Line charts, column charts; date hierarchies)
- [ ] What's the distribution of my expenses (e.g., how many transactions are under $10, between $10 and $50, etc.)? (Histograms, bins)

II. Time Intelligence & Trends (Deeper Analysis):

- [ ] How has my spending changed over time? (Line charts, time series analysis)
- [ ] What's the trend of my spending in a specific category? (Filtered line charts)
- [ ] How does my spending this month compare to last month, or the same month last year? (DAX functions like SAMEPERIODLASTYEAR, DATEADD; calculations of variance)
- [ ] What's my rolling average spending (e.g., 7-day or 30-day moving average)? (DAX functions like CALCULATE and AVERAGEX)
- [ ] Can I forecast my spending for the next month based on past trends? (While Power BI has some basic forecasting, this might be a good opportunity to explore more advanced techniques or integrations with other tools later on)

III. Advanced Analysis & Insights (Level Up):

- [ ] Is there a correlation between my spending in different categories? (Scatter plots, correlation analysis)
- [ ] Can I identify any outliers in my spending? (Box and whisker plots, conditional formatting)
- [ ] Can I create a budget and track my progress against it? (Calculated measures, conditional formatting to highlight overspending)
- [ ] Can I segment my expenses by different criteria (e.g., payment method, location)? (Slicers, filters)
- [ ] Can I drill down into specific transactions from summary visualizations? (Drillthrough functionality)
- [ ] Can I create interactive dashboards that allow me to explore my data from different angles? (Cross-filtering, tooltips)
- [ ] If you have multiple accounts, can you combine the data and analyze spending across all accounts? (Data modeling, relationships)

IV.  Power BI Specific Skills to Focus On:

- [ ] Data Cleaning and Transformation: Learn Power Query to clean up your expense data (e.g., handling missing values, changing data types, splitting columns).
- [ ] DAX (Data Analysis Expressions): Master basic DAX functions (SUM, AVERAGE, COUNT, etc.) and gradually learn more advanced functions (e.g., time intelligence, filtering).
- [ ] Visualizations: Experiment with different chart types and learn how to format them effectively.
- [ ] Data Modeling: Understand how to create relationships between tables if you have more complex data.
- [ ] Interactivity: Learn how to use slicers, filters, and drillthrough to make your dashboards interactive.
- [ ] Publishing and Sharing: Once you're happy with your dashboard, learn how to publish it to the Power BI service and share it with others.

Tips for Learning:

* Start simple: Don't try to tackle everything at once. Focus on one or two questions at a time.
* Use online resources: There are tons of great tutorials and documentation available online. Microsoft's website and YouTube are excellent places to start.
* Practice: The best way to learn Power BI is to practice. The more you use it, the better you'll become.
* Don't be afraid to experiment: Try different things and see what works best.
* Join the Power BI community: There are many online forums and communities where you can ask questions and get help.
