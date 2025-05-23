# An Introduction into PowerBI - An Analysis of Expenses
The PowerBI Dashboard (DB) provides an overview of personal expenses, and breaksdown each category of expenses into varying levels of granularity. It analyses the spending habits of the user to gain some insight on the expenses incurred.  

The DB applies different skillsets (e.g. DAX, Data Modelling practices, ETL(using Python, Power Query & M) and answer various question about the user spending habits.
For Example,

* What is the total expenses to date?
* What is the average spending?
* Which category incurred the most expense? 
* Is there a difference in spending between the weekday and weekend

The PBIB consist of two pages of report. The first page provides an bird's eye view of the dataset, while the second page breaks down each month's expenses in greater detail.

## Summary Page

<img src ="https://github.com/user-attachments/assets/b68b887f-12fb-4314-b93a-ab5bd842fb76" width= "800"></img>

[Streamlit Implementation](https://mainpy-t6ryjmv5dd4yxeoz5wxtna.streamlit.app/)


<details>
  <summary>Panels</summary>

  ### Panel #01
  Panel #01 serves as an general overview of expenses for the selected year, displaying several key statistics such as the total expenses and average expenses per month. It also highlights the month with the highest and lowest expenses. The line chart visually summurise expenses as a monthly basis, visually highlighting months with abnormally high expense.    
  
  ### Panel #02
  Panel #02 presents monthly expenses in tabular form, comparing monthly expenses relative to the previous month's expenses. The `Month over Month Change (%)` column has been color-coded to visually present the Month over Month changes. Red(Green) denote an expense increase(decrease) from the prior month. This allows the audience to quickly identify a month of interest and drill in for further details. One leading example is October, from panel #01, the month of October is observed to have an sharp **increase of 119%** from the previous month. 
  
  The button enables a graphic representation of the relative changes between each month, providing a more condensed view.
  
  ### Panel #03 & Panel #04
  Panel #03 take a different approach to analysing expenses by highlighting the top 3 categories. By default, the bar chart aggregates the top 3 categories based on the entire year's expenses. This can be narrowed to a particular month by selecting a month in panel #02. 
  
  The button enables an aggregated view of the top 3 categories on an annual basis, displaying each category for each month and it's cumulative total. 
  
  Panel #04 provides a greater level of granularity by breaking down expenses into sub-categories relative to the total expenses. This allows the audience to gain a better understanding of their spending habits, giving them insight to better manage their financials.
  
  ### Obervation
  An steep increase in expenses was observed in October 2024. This increase in expenses amounted to 119% from September and it is an significant increase, considering the fact that expenses in September had risen by 41%. One unintended side effect of this sudden spike is that average expenses has been skewed towards the higher end, leading to the false impression of a higher average expense. This could result in an overly-inflated forecast of future expenses. 
  
  From panel #03, the 'Food' category has the lion's share of annual expenses (63.1%). This is to be expected as Food is an consistent expense incurred daily by everyone, regardless of their financial commitment. Panel #04 breaks down the 'Food' category further, and notice that bulk of this expenses originated from 'Dinner'. This implies that one possible strategy to reducing expenses is to source of cheaper food alternative.
  
  The second highest category is 'Personal', amounting to 24.22% of overall expenses. Breaking the category down, 'S24 FE' sub category refers to a one-time big ticket purchase and carries the highest weightage, accounting for 71%(35%) of 'Personal'(Overall) expenses. This articificially inflate average expenses as this is not a recurring expenses. A realistic approach is to spread the cost across an arbitrary period for an more accurate estimate of average expenses. One suggestion is to use the expected lifespan of the device.

</details>

<img src ="https://github.com/user-attachments/assets/1c9d182a-7443-4da4-b5c3-1d60855232a4" width= "500"></img>

<details>
  <summary>Spending comparison between Weekend and Weekday</summary>

  ### Panel #05
  Overall, the weekend and weekday expenses are rather consistent with minor fluctuation around the $20 - $40 range.  
  From the period of January to May, weekend expenses are consistently higher than weekday expenses.  
  Following the period of June to September, weekday expenses have increased and overtook weekend expenses.   
  Finally, a weekend expenses spike in October was observed. Afterwhich, a 'V'-shaped increase is observed in November and December.  


</details>

<img src ="https://github.com/user-attachments/assets/b7a798de-0045-4e87-b245-b9c32175e23b" width= "500"></img>

<details>
  <summary>Annual Growth of Top 3 Expenses</summary>


### Panel #06
Panel 6 displays the annual growth of the top 3 expenses. Food and Home expenses have seen linear growth, implying that spendings have been consistent and predictable.  
Personal expenses have seen linear growth from the period of January to September before having a steep spike in October. This is attributed to the big ticket purchase

</details>


## Breakdown Page

<img src="https://github.com/user-attachments/assets/70524d63-d814-45dc-a236-f877d653c15f" width="500"></img>

<details>
  <summary>Breakdown Page</summary>
  
The breakdown page takes a concentrated approach and breakdowns the monthly expenses into different time intervals. Considering that expenses have been rather consistent throughout the months, apart from October, we will focus on attention on October.  

The total amount of expenses incurred is $1,952.05 which is 109.26% more than last month. Even when comparing against two month moving average, October's expenses is still 131.61% more. This establishes October as the month with the highest expense.  

Personal (43.85%), Food (27.75%) and Health/Medical (16.62%) are the top 3 category of expenses. This contracts the finding from the summary page which found that the top 3 expenses are Food, Personal and Home. Delving further, the top 3 expenses by sub-categories are 'S24 FE', 'Dinner', 'IP Insurance'. One implication is the presense of an re-occuring annual expense (IP Insurance).

The table visual breakdowns the change in each expenses relative to last month. Health/Medical expenses increased by 286.19% which is in order of magnitude higher than home expense, which explains the change in rankings.

The weekday averages and weekend average compares and contrast the average expenses between weekdays and weekend to determine spending pattern. This is supported by the adjacent weekly table to identify the distribution of expenses across the month. It is observed that Week 4 of October has the highest weekly expenses, contributing 52.34% for October. 



Finally, the line chart provides an overview of daily expenses. Majority of daily expenses are below the average, which is skewed by the abnormally high expense incurred. The tooltip displays each associated expenses to provide immediate feedback to users.

</details>

## Conclusion

