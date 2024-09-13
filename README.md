# Coffee Sales Dashboard

The Coffee Sales Dashboard features three interactive graphs and five customizable slicers, allowing users to filter sales data based on specific dates, coffee types, roast types, sizes, and loyalty status. Below is a summary of the dashboard’s features and the steps taken to create it:

## Features

- **Interactive Graphs**: Three graphs that update based on user selections.
- **Customizable Slicers**: Five slicers to filter data by date, coffee types, roast types, sizes, and loyalty status.

## Steps to Create the Dashboard

1. **Data Preparation**

   I began by downloading the dataset from the GitHub repository shared by Mo and opened it in Excel. The file, in xlsx format, contained three sheets: Orders, Customers, and Products.

2. **Data Integration Using XLOOKUP**

    To consolidate data from different sheets, I used the XLOOKUP function to merge information into a single sheet. This included customer details such as Name, Email, and Country. For example, to populate the Customer Name column, I used:
   
   ```=XLOOKUP(C2, customers!$A$2:$A$1001, customers!$B$2:$B$1001, "", 0)```

   For email addresses, to handle cells without data and avoid zeros, I used an IF statement:
   
   ```=IF(XLOOKUP(C2, customers!$A$2:$A$1001, customers!$C$2:$C$1001, "") = 0, "", XLOOKUP(C2, customers!$A$2:$A$1001, customers!$C$2:$C$1001))```

   The formula to fill the Country column was:
   
   ```=XLOOKUP(C2, customers!$A$2:$A$1001, customers!$G$2:$G$1001, "", 0)```

4. **Dynamic Data Filling with INDEX + MATCH**

   To simplify data retrieval from the Products sheet, I utilized INDEX and MATCH functions. The formula used was:
   
   ```=INDEX(products!$A$1:$G$49, MATCH(orders!$D2, products!$A$1:$A$49, 0), MATCH(I$1, products!$A$1:$G$1, 0))```

6. **Calculating Sales**

   I created a Sales column by multiplying the Price and Quantity columns using:
   `=L2 * E2`
   
7. **Enhanced Data Formatting with IF Statements**

   For better readability, I added a column for Coffee Type Name using an IF statement:
   
   ```=IF(I2="Rob", "Robusta", IF(I2="Exc", "Excelsa", IF(I2="Ara", "Arabica", IF(I2="Lib", "Liberica"))))```
   
   Similarly, I created a column for Roast Types:
   
   ```=IF(J2="M", "Medium", IF(J2="L", "Light", IF(J2="D", "Dark")))```
   
9. **Formatting Dates and Currency**

   I adjusted the date format to `dd-mmm-yyyy` to display months as three-letter abbreviations and formatted currency values to USD.

11. **Data Cleaning**

    Although the dataset was in good condition, I used the Remove Duplicates feature to ensure there were no duplicate entries.

13. **Converting Range to Table**

    To facilitate updates and dynamic data handling in pivot tables, I converted the data range into a structured table.

15. **Creating Pivot Tables and Formatting**

    I generated a pivot table to analyze sales over time. I grouped sales by Coffee Type Name and Date, and formatted the data to display monthly and yearly trends. A line chart was added to visualize these trends.

17. **Adding and Customizing a Timeline**

    I incorporated a date slider to enable users to select specific time periods. The timeline was customized to enhance its visual appeal.

19. **Incorporating Slicers**

    I added slicers for Coffee Type, Roast Type, Size, and Loyalty to allow users to filter data interactively. The Loyalty slicer required a new column created with XLOOKUP to retrieve loyalty information.

21. **Sales Analysis by Country and Top 5 Customers**

    I created pivot tables to show sales by country and the top 5 customers. The sales by country graph was formatted to match the overall style of the dashboard, while the top 5 customers pivot table was filtered to show only the top five.

23. **Assembling the Dashboard**

    I assembled the final dashboard by copying and arranging the graphs into a new sheet, aligning them neatly, and adjusting cell sizes. Gridlines were removed for a cleaner presentation. The completed dashboard is shown at the top of this article.

