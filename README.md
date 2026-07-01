# Power-BI---Assignment

1. Data Import:

○ Import List of Orders.csv into Power BI.

○ Open the list of orders in the Power Query Editor using the Transform Data option.

○ Import Order Details.csv and Sales Target.csv into Power Query Editor.

2. Row Limiting & Data Types:

○ Restrict the List of Orders table to the first 500 rows.

○ Set the Order Date column to the Date data type.

○ Change the Amount and Target columns to fixed decimal numbers.

3. Text Formatting:
   
○ Format the CustomerName column to proper case to ensure consistent capitalization.

4. Column Creation:

○ Merge the City and State columns to create a new column named Location in the format:
City, State

○ Create a custom column named Profit Margin calculated as: Profit / Amount (expressed as
a percentage)

5. Conditional Column:

○ Add a conditional column named Profit Status based on:
■ Profit < 0 → Loss
■ Profit = 0 → Break-Even
■ Profit > 0 → Profit

6. Merging Data (Joins)

○ Merge the List of Orders and Order Details tables using Order ID.

○ Name the merged output table as Orders Data.
7. Handling Missing Data & Duplicate Data

● Identify missing values across all tables.

● Define and apply appropriate strategies such as:

○ Replacing missing values

○ Removing records

○ Retaining nulls with justification

● Identify duplicate rows and define a suitable handling strategy based on business logic.

8. Sorting and Filtering Data

● Sort records in the Orders Data table by Order Date in descending order.

● Apply filters to analyze orders from a specific state (e.g., Tamil Nadu).

9. Grouping and Aggregating Data

● Duplicate the Order Details table and perform the following:

○ Count of Order ID

○ Average Profit by Category

○ Total Amount by Sub-Category

● Duplicate the Sales Target table and aggregate the total Target by Month of order date.

10. Data Modeling:

● Establish a relationship between:

○ List of Orders and Order Details using Order ID

● Establish a relationship between:

○ Order Details and Sales Target using Category
