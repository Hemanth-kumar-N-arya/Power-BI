# Power-BI - HR Analysis 
1. Data Import and Transformation:

let
    Source = Excel.Workbook(File.Contents("C:\Path\To\Your\File.xlsx"), null, true),
    EmployeeTable = Source{[Item="EmployeeTable"]}[Data],
    RemoveColumns = Table.RemoveColumns(EmployeeTable, {"Column1", "Column2"}),
    RemoveNullRows = Table.SelectRows(RemoveColumns, each not List.IsEmpty(List.RemoveMatchingItems(Record.FieldValues(_), {null})))
in
    RemoveNullRows
2. Basic Visualization:
Create a bar chart with the 'Department' field on the axis and the count of employees on the values.

3. Filtering Data:
Add a slicer visualization, select the 'Job Role' field, and users can filter employees based on job role.

4. Joining Data:
Use an inner join to combine employee data with in-time and out-time data. This is assuming each record in the employee data has a corresponding record in the in-time and out-time data.

5. Calculated Columns:

AgeGroup = 
SWITCH(
    TRUE(),
    'Employee'[Age] < 30, "Under 30",
    'Employee'[Age] >= 30 && 'Employee'[Age] < 40, "30-40",
    'Employee'[Age] >= 40 && 'Employee'[Age] < 50, "40-50",
    'Employee'[Age] >= 50, "Over 50",
    BLANK()
)
6. Measures in DAX:

AverageMonthlyIncome = AVERAGE('Employee'[MonthlyIncome])

7. Time Intelligence:

YoYGrowth = 
CALCULATE(
    DIVIDE(
        [TotalIncome] - CALCULATE([TotalIncome], DATEADD('Calendar'[Date], -1, YEAR)),
        CALCULATE([TotalIncome], DATEADD('Calendar'[Date], -1, YEAR))
    ),
    ALL('Calendar')
)

8. Hierarchies:
Create a hierarchy by dragging 'Year', 'Month', and 'Day' columns into the hierarchy pane.

9. Advanced DAX Calculation:

AttritionRate = 
DIVIDE(
    CALCULATE(SUM('Employee'[Left])),
    CALCULATE(COUNTROWS('Employee')),
    0
) * 100

10. Advanced Join:
Use a left join to preserve all records in the employee data, potentially leading to null values in the additional dataset.

11. Complex Filtering:
Create a slicer with both 'Department' and 'Job Role' fields.

12. Advanced Time Intelligence:
See previous responses for the calculation of the moving average.

13. Conditional Formatting:
Apply conditional formatting to the 'Monthly Income' column in a table visualization based on values.

14. Parameter Tables:
Create a parameter table with thresholds, then use measures that refer to these parameters for performance ratings.

15. Custom Visualizations:
Explore custom visuals from the marketplace or create custom visuals using tools like Charticulator.

16. Aggregations:
Define aggregations to pre-calculate and optimize summaries for large datasets.

17. What-If Analysis:
Use What-If parameters to adjust factors like salary increase and observe the impact on attrition rates.

18. Cross-Filtering:
Enable cross-filtering between visuals so that selecting a data point in one visual filters others.

19. KPIs:
Create measures for various KPIs like sales per employee, customer satisfaction index, etc.

20. Dynamic Reporting:
Use bookmarks and buttons to switch between different report views or apply filters.

