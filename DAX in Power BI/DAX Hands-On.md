# DAX Functions with Example

- ### MATHs & STATs Functions
<details>
  					<summary> Click Here for Functions </summary>

- ### SUM - Calculates the total sum of a column. 
		Total Sales = SUM(Table[Sales])
- ### AVERAGE - Calculates the AVG of column.
  		Average Sales = AVERAGE(Table[Sales])
- ### MAX/MIN - Finds the maximum or minimum value in a column.
		Max Sale = MAX(Table[Sales])
		Min Sale = MIN(Table[Sales])
- ### DIVIDE - Divides two numbers, with an option to specify an alternate result if the denominator is zero.
		AVG Price per Unit = DIVIDE([Total Sales], SUM(Maths_State_Funct[Quantity]))
- ### COUNT/COUNTA - Counts the number of rows or non-blank values in a column.
- ### CountRows - Counts the number of rows in a table or table expression.
- ### DistinctCount - Counts the number of unique, non-blank values in a column.
  		Count Measure = Count(Maths_State_Funct[ID])
  		CountA Measure = COUNTA(Maths_State_Funct[Quantity])
		CountRow Measure = COUNTROWS(Maths_State_Funct)
  		DistinctCount Measure = DISTINCTCOUNT(Maths_State_Funct[Price])
- ### Iterator Functions
Iterator functions in DAX (Data Analysis Expressions) are a category of functions that evaluate an expression for each row of a table and then aggregate the results. Unlike simple aggregation functions like SUM or AVERAGE, which operate on entire columns, iterator functions work row by row, allowing for more complex calculations.

- #### SUMX - Sums up the results of an expression evaluated for each row in a table.
		SUMX Funct = SUMX(Maths_State_Funct, Maths_State_Funct[Price]*Maths_State_Funct[Quantity])
- #### AVERAGEX - Averages the results of an expression evaluated for each row in a table.
  		Average Sales Per Transaction = AVERAGEX(Table, Table[Sales])
- #### MAX/MIN - Finds the maximum or minimum value in a column.
		Max Profit = MAXX(Table, Table[Sales] - Table[Quantity])
		Min Profit = MINX(Table, Table[Sales] - Table[Quantity])
- #### DIVIDE - Divides two numbers, with an option to specify an alternate result if the denominator is zero.
		AVG Price per Unit = DIVIDE([Total Sales], SUM(Maths_State_Funct[Quantity]))
- #### COUNTX - Counts the rows that result from an expression evaluated for each row in a table.
  		CountX Funct = COUNTAX(Maths_State_Funct, if(Maths_State_Funct[Quantity] > 90, 1, BLANK()))
</details>

- ### Logical Functions
<details>
  <summary> Click Here for Functions </summary>

- #### IF - The IF function checks a condition and returns one value if the condition is true and another value if the condition is false.
		Simple If Funct = IF([Total Sales LF] > 9000, "Great", "Good")
		Nested If Funct = IF([Total Sales LF] >= 50000, "High", IF([Total Sales LF] < 50000 & [Total Sales LF] >= 10000, "Medium", "Low"))
  		Bonus = IF(Sales[Total Sales] > 50000, Sales[Total Sales] * 0.1, Sales[Total Sales] * 0.05)
- #### AND - The AND function returns TRUE if all arguments are true, and FALSE otherwise
  		High_Performer = IF(AND(Sales[Total Sales] > 50000, Sales[Attendance] > 95), "Yes", "No")
- #### OR - The OR function returns TRUE if at least one of the conditions is true.
		Qualified = IF(OR(Sales[Total Sales] > 50000, Sales[Experience] > 5), "Yes", "No")
- #### NOT - The NOT function reverses the result of a logical expression.
		Below_Average = IF(NOT(Sales[Total Sales] > 30000), "Yes", "No")
- #### SWITCH - The SWITCH function evaluates an expression against a list of values and returns one based on matching results.
  		CountX Funct = COUNTAX(Maths_State_Funct, if(Maths_State_Funct[Quantity] > 90, 1, BLANK()))
- #### IFERROR - The IFERROR function returns a specified value if an expression results in an error.
		DivisionResult = IFERROR(Sales[Total Sales] / Sales[No. of Products], "Error")
- #### TRUE and FALSE - TRUE and FALSE return the respective logical values.
		AlwaysTrue = TRUE()
		AlwaysFalse = FALSE()
</details>

- ### Text Functions
<details>
  <summary> Click Here for Functions </summary>

- #### CONCATENATE - Combines two text strings into one.
		FullName = CONCATENATE(Orders[FirstName], Orders[LastName])
- #### COMBINEVALUES - Joins multiple text strings with a specified delimiter.
  		FullNameWithSpace = COMBINEVALUES(" ", Orders[FirstName], Orders[LastName])
- #### FORMAT - Converts a value to text according to a specified format.
		FormattedDate = FORMAT(Orders[OrderDate], "DD/MM/YYYY")
- #### LEFT/MID/RIGHT - Extracts a specified number of characters from the start / Extracts characters from the middle / Extracts a specified number of characters from the end.
 		LeftPart = LEFT(Orders[ProductCode], 3)
		MidPart = MID(Orders[ProductCode], 2, 3)
		RightPart = RIGHT(Orders[ProductCode], 4)
- #### UPPER/LOWER - Converts text to uppercase or lowercase.
  		UpperCase = UPPER(Orders[ProductName])
		LowerCase = LOWER(Orders[ProductName])
- #### LEN - Returns the number of characters in a text string.
		LengthOfName = LEN(Orders[ProductName])
- #### SEARCH/FIND - Finds the starting position of a substring within a string.
		Position = SEARCH("top", Orders[ProductName], 1, 0)
- #### REPLACE - Replaces part of a text string with another text string.
  		ReplacedText = REPLACE(Orders[ProductCode], 2, 3, "XYZ")
- #### SUBSTITUTE - Substitutes old text with new text in a string.
		SubstitutedText = SUBSTITUTE(Orders[ProductName], "top", "phone")
- #### TRIM - Removes all spaces from text except for single spaces between words.
		TrimmedText = TRIM(Orders[ProductName])
</details>

- ### Filter Functions
<details>
  <summary> Click Here for Functions </summary>

- #### CALCULATE - The CALCULATE function is one of the most powerful functions in DAX. It modifies the context in which data is filtered and then performs a calculation based on that modified context.
		Calculate = CALCULATE(SUM('Filter Functions'[Salary]), 'Filter Functions'[Department] = "IT")
- #### FILTER - The FILTER function returns a table that represents a subset of another table based on a condition.
  		Filter tb = FILTER('Filter Functions', 'Filter Functions'[Age] > 50)
- #### ALL - The ALL function removes all filters from a specified column or table. It is often used to create calculations that do not consider any existing filters.
		All Funct = CALCULATE(SUM('Filter Functions'[Salary]), ALL('Filter Functions'[Department]))
- #### ALLEXCEPT - The ALLEXCEPT function removes all filters from the specified table or column except for the ones mentioned.
 		AllExcept Funct = CALCULATE(SUM('Filter Functions'[Salary]), ALLEXCEPT('Filter Functions', 'Filter Functions'[Department]))
- #### ALLSELECTED - The ALLSELECTED function returns all rows in a table or all values in a column by ignoring any filters that might have been applied, except for those set by a visual or slicer.
		AllSelected Funct = CALCULATE(SUM('Filter Functions'[Salary]), ALLSELECTED('Filter Functions'))
- #### KEEPFILTERS - The KEEPFILTERS function applies a filter on top of an existing filter, ensuring that the new filter is respected.
  		UpperCase = UPPER(Orders[ProductName])
		LowerCase = LOWER(Orders[ProductName])
- #### REMOVEFILTERS - The REMOVEFILTERS function clears any filters that have been applied to the columns or tables specified.
		Position = SEARCH("top", Orders[ProductName], 1, 0)
- #### SELECTEDVALUE - The SELECTEDVALUE function returns the value of a column when only one value is selected, or it returns an alternative result when multiple values are selected.
  		SelectedValue = IF(HASONEVALUE('Filter Functions'[Department]), SUM('Filter Functions'[Salary]), BLANK())
  		SelectedValue Funct = SELECTEDVALUE('Filter Functions'[Department], "Select a Department")
- #### HASONEVALUE - The HASONEVALUE function in DAX is used to check whether there is exactly one distinct value in the current filter context for a specified column or expression. It returns a Boolean value: TRUE if there is exactly one distinct value and FALSE otherwise.
  		SalesInformation = SWITCH(TRUE(), HASONEVALUE(Product[Category]), SUM(Sales[SalesAmount]),
  			ISFILTERED(Product[Category]), "Multiple Categories Selected",
    			"No Category Selected")
- #### ISFILTERED - The ISFILTERED function in DAX checks whether a column or table has been filtered in the current context. It returns a Boolean value: TRUE if the column or table is filtered and FALSE otherwise.
  		Isfiltered = if(ISFILTERED('Filter Functions'[Department]), "Yes", "No")
</details>

- ### Table Functions
<details>
  <summary> Click Here for Functions </summary>

- #### SUMMARIZE - The SUMMARIZE function creates a summary table for the requested columns of a table. It groups the data by the specified columns and can calculate aggregations.
		Summarize tb = 
    			SUMMARIZE('Table Function', 
        			'Table Function'[Category], 
        			'Table Function'[SubCategory],
        			"Total Sales", SUM('Table Function'[SalesAmount]),
        			"Total Quantity", SUM('Table Function'[QuantitySold])
    			)
- #### ADDCOLUMNS - The ADDCOLUMNS function adds calculated columns to a table.
  		AddColumn tb = 
    			ADDCOLUMNS('Table Function',
        			"Profit", 'Table Function'[SalesAmount] - 100
    			)
- #### DISTINCT - The DISTINCT function returns a one-column table that contains the distinct values from the specified column.
		Distinct Funct = DISTINCT('Table Function'[Category])
- #### VALUES - The VALUES function returns a one-column table that contains the distinct values in a column or a one-row table that contains the distinct values in the columns.
 		Value Funct = VALUES('Table Function'[Category]) 
- #### UNION - The UNION function combines two or more tables by combining their rows.
		Union Funct = UNION('Table Function', 'Filter Functions')
- #### INTERSECT - The INTERSECT function returns a table that contains only the rows that are present in both tables.
  		Intersect tb = INTERSECT('Table Function', 'Logical Functions')
- #### TOPN - The TOPN function returns the top N rows of a table, based on a specified expression.
		Topn Funct = TOPN(10, 'Table Function', 'Table Function'[ID], ASC)
</details>

- ### Relationship Functions
<details>
  <summary> Click Here for Functions </summary>

- #### RELATED Function (Calculated Column) - The RELATED function in Power BI DAX is a powerful tool that allows you to fetch related data from another table based on an existing relationship between the tables. It is particularly useful in scenarios where you want to enrich your data model by pulling in additional details from a related table.
		Price = RELATED(Products_Relationship_F1[Price])
- #### RELATEDTABLE Function - The RELATEDTABLE function in Power BI DAX is used to retrieve a table containing all rows from a related table that are associated with the current row. It is particularly useful when you have a one-to-many relationship and you want to aggregate or analyze related rows from the "many" side of the relationship.
  		OrderCount = COUNTROWS(RELATEDTABLE(Orders_Relationship_F2))
</details>

- ### Date & Time Functions
<details>
  <summary> Click Here for Functions </summary>

- #### DATE - Creates a date in datetime format from individual year, month, and day values.
		Date Funct = DATE(2024, 8, 20)
- #### DATEDIFF - Returns the difference between two dates in specified units (e.g., days, months, years).
  		DateDiff Funct = DATEDIFF([StartDate], [EndDate], DAY)
- #### YEAR/MONTH/DAY - Extracts the year, month, or day from a date.
		Year Funct = YEAR([StartDate])
  		Month Funct = MONTH([StartDate])
		Day Funct = Day([StartDate])
- #### HOUR - Extracts the hour from a time value.
 		Hour Funct = HOUR(NOW())
- #### TODAY/NOW - Returns the current date (TODAY) or current date and time (NOW).
		Today Funct = = TODAY()
- #### WEEKDAY Number - Returns the day of the week corresponding to a date.
  		WeekDay Funct = WEEKDAY('Date Time Function'[StartDate], 2)
- #### WEEKNUM - Returns the week number for a date.
		WeekNum Funct = WEEKNUM('Date Time Function'[StartDate], 2)
- #### NETWORKDAYS - Returns the number of whole working days between two dates.
 		NETWORKDAYS Funct = NETWORKDAYS = NETWORKDAYS('Date Time Function'[StartDate], 'Date Time Function'[EndDate])

- ### Time Intelligence Functions

- #### DATESYTD - Returns a table that contains a column of the dates for the year to date.
		DatesYTD = DATESYTD('Date Time Function'[StartDate])
- #### DATESMTD - Returns a table containing the dates in the month to date.
  		DatesMTD = DATESMTD('Date Time Function'[StartDate].[Date])
- #### DATEADD - Returns a table with a shifted set of dates by a specified interval.
		DATEADD = DATEADD('Date Time Function'[EndDate], -1, YEAR)
- #### DATESBETWEEN - Returns a table with dates between a specified start and end date.
  		DATESBETWEEN = DATESBETWEEN('Date Time Function'[StartDate], DATE(2020, 01, 01), DATE(2022, 01, 01))

</details>

- ### VAR & RETURN
#### In Power BI DAX (Data Analysis Expressions), VAR and RETURN are used to define and work with variables within a DAX formula. They help simplify complex calculations and improve readability. 
<details>
  <summary> Click Here </summary>

- #### VAR (Variable) - Define a variable to store an intermediate value or result within a DAX formula.
		VAR <VariableName> = <Expression>
		Total Sales = 
			VAR TotalAmount = SUM(Sales[Amount])
			VAR TotalQuantity = SUM(Sales[Quantity])
			RETURN
				TotalAmount / TotalQuantity

- #### RETURN - Specify the final expression or calculation to be evaluated and returned as the result of the formula.
  		RETURN <Expression>
		Average Sales per Unit = 
			VAR TotalSalesAmount = SUM(Sales[Amount])
			VAR TotalUnits = SUM(Sales[Quantity])
			RETURN
				TotalSalesAmount / TotalUnits
- ### Example 1: Calculating Profit Margin
- #### Suppose you have a table Sales with columns Revenue and Cost. You want to calculate the profit margin.
			Profit Margin (%) =
  				VAR TotalRevenue = SUM(Sales[Revenue])
				VAR TotalCost = SUM(Sales[Cost])
				VAR Profit = TotalRevenue - TotalCost
				RETURN
					IF(TotalRevenue > 0, (Profit / TotalRevenue) * 100, 0)
	- TotalRevenue and TotalCost are variables holding the sum of Revenue and Cost, respectively.
	- Profit calculates the difference between Revenue and Cost.
	- The RETURN statement calculates the profit margin as a percentage and ensures that the calculation only occurs if TotalRevenue is greater than zero.

- ### Example 2: Year-to-Date (YTD) Sales
- #### You want to calculate the year-to-date sales for the current year.
		YTD Sales = 
			VAR CurrentYear = YEAR(TODAY())
			VAR SalesYTD = 
			    CALCULATE(
			        SUM(Sales[Amount]),
			        DATESYTD(Sales[Date])
			    )
			RETURN
				IF(YEAR(MAX(Sales[Date])) = CurrentYear, SalesYTD, BLANK())
	- CurrentYear stores the current year.
	- SalesYTD calculates the year-to-date sales using the DATESYTD function.
	- The RETURN statement ensures that YTD sales are only shown for the current year.
   
- ### Example 3: Average Sales per Customer
- #### You want to calculate the average sales per customer.
		Average Sales per Customer = 
			VAR TotalSales = SUM(Sales[Amount])
			VAR CustomerCount = DISTINCTCOUNT(Sales[CustomerID])
			RETURN
				IF(CustomerCount > 0, TotalSales / CustomerCount, 0)
	- TotalSales holds the sum of Amount from the Sales table.
	- CustomerCount calculates the number of distinct customers.
	- The RETURN statement computes the average sales per customer, ensuring that the result is only calculated if there are customers.

- ### Example 4: Total Sales with Adjustments
- #### Suppose you want to calculate total sales, including a 5% adjustment.
		Adjusted Sales = 
			VAR TotalSales = SUM(Sales[Amount])
			VAR AdjustmentFactor = 1.05
			RETURN
				TotalSales * AdjustmentFactor
	- TotalSales calculates the total sales amount.
	- AdjustmentFactor represents a 5% increase.
	- The RETURN statement applies the adjustment factor to the total sales amount.

- ### Example 5: Sales Growth from Last Year
- #### You want to calculate the growth in sales compared to the previous year.
  
		Sales Growth (%) = 
			VAR CurrentYearSales = SUM(Sales[Amount])
			VAR PreviousYearSales = 
		    	CALCULATE(
		        	SUM(Sales[Amount]),
		        	SAMEPERIODLASTYEAR(Sales[Date])
		    	)
			VAR Growth = CurrentYearSales - PreviousYearSales
			RETURN
				IF(PreviousYearSales > 0, (Growth / PreviousYearSales) * 100, 0)
	- CurrentYearSales stores the sum of sales for the current period.
	- PreviousYearSales calculates the sum of sales for the same period last year using SAMEPERIODLASTYEAR.
	- Growth computes the difference between current and previous year sales.
	- The RETURN statement calculates the sales growth percentage, ensuring it's only shown if there were sales in the previous year.

</details>

- #### DAX by ChatGPT - https://chatgpt.com/share/d4a256b7-e8c4-405e-ab70-cc83b4b14437
