# Sales-Analysis-with-PowerBI

Business Requirements
1.	Metrics: Sales, Profit % of returned orders. Show % change vs PY
2.	Compare Sales performance versus previous year overtime 
3.	Determine the most profitable product and the most loss-making product
4.	Find out the place where the most profit is being made
5.	Find out the sales by segment
6.	Find out our customer base by region


**Exploratory Data Analysis

*Created a DAX expression to create a date table using the CALENDAR function to cover the range between the minimum and maximum order dates from the Orders table, and then it adds an additional column to determine the "Start of Month" for each date

The DAX formula  calculates the percentage of returned orders. Here's a breakdown of how it works:
1.	VAR _total_orders = DISTINCTCOUNT(Orders[Order ID]):
This variable calculates the total number of distinct orders from the Orders table. It counts the unique Order ID values in the Orders table.
2.	VAR _returned_orders = DISTINCTCOUNT(Returns2[Order ID]):
This variable calculates the number of distinct orders that have corresponding returns in the Returns2 table. It counts the unique Order ID values in the Returns2 table, assuming this table contains information about returned orders.
3.	VAR _perc = DIVIDE(_returned_orders, _total_orders):
This variable calculates the percentage of returned orders by dividing the number of returned orders (_returned_orders) by the total number of orders (_total_orders). The DIVIDE function is used to safely perform the division, avoiding any potential divide-by-zero errors.
4.	RETURN _perc:
The final step returns the percentage value that was calculated in the _perc variable.


The DAX formula written calculates Sales from the Previous Year (PY) by using the SAMEPERIODLASTYEAR function, which shifts the date context by one year back. Let's break down how it works:

Formula:
DAX
Copy
Edit
Sales PY = CALCULATE([Sales], SAMEPERIODLASTYEAR('Date Table'[Date]))
Breakdown:
[Sales]:

This refers to an existing measure or column in the data model that calculates the sales value (e.g., total sales amount). It could be something like SUM(Orders[SalesAmount]) if it's defined as a measure.
SAMEPERIODLASTYEAR('Date Table'[Date]):

This function shifts the current date context by one year back. It looks at the current date column ('Date Table'[Date]) and returns a set of dates that corresponds to the same period from the previous year.
For example, if the current filter context includes the month of March 2025, SAMEPERIODLASTYEAR would return the dates for March 2024.
CALCULATE:

The CALCULATE function modifies the filter context in which the [Sales] measure is evaluated. In this case, it applies the filter for the same period from the previous year using the SAMEPERIODLASTYEAR function.
