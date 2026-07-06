# Power-BI---Assignment

1. Data Ingestion

Launch Power BI Desktop.

Navigate to Get Data > Text/CSV and ingest List of Orders.csv.

Select Transform Data to launch the Power Query Editor.

From inside the Power Query Editor interface, navigate to Home > New Source > Text/CSV to load Order Details.csv and Sales target.csv.

2. Row Constraints & Strict Schema Typing
Row Retention Constraint: Select the List of Orders query. In the Home tab, choose Keep Rows > Keep Top Rows and configure the value to 500.

Data Type Enforcement:

In List of Orders, cast Order Date to the Date data type.

In Order Details, cast Amount to a Fixed decimal number ($).

In Sales target, cast Target to a Fixed decimal number ($).

3. Text & Casing Standardization

Select the List of Orders query.

Right-click the CustomerName column header (or use the Transform tab ribbon) and select Format > Capitalize Each Word to ensure proper case consistency across all customer records.

4. Advanced Column Engineering

Geographic Concatenation (Location):

In List of Orders, select the City column, hold down Ctrl, and select the State column.

Navigate to Add Column > Merge Columns.

Configure the separator as a Comma and name the resulting column Location (e.g., City, State).

Calculated Financial Expression (Profit Margin):

Select Order Details. Navigate to Add Column > Custom Column.

Name the column Profit Margin.

Apply the following Power Query formula:

Code snippet

[Profit] / [Amount]

Commit the change, then cast the new column to Percentage (%).

5. Conditional Business Logic Evaluation

In Order Details, navigate to Add Column > Conditional Column.

Create a dynamic rule evaluation named Profit Status leveraging this conditional matrix:

IF [Profit] < 0  👉 "Loss"
LN [Profit] = 0  👉 "Break-Even"
LN [Profit] > 0  👉 "Profit"

6. Query Joins & Flat Denormalization

From the Home tab ribbon dropdown, click Merge Queries > Merge Queries as New.

Select List of Orders as the primary (left) table and Order Details as the secondary (right) table, joining them via the Order ID column.

Select Left Outer as the Join Kind. Click OK.

Rename the output query to Orders Data.

Click the structural Expand icon (two divergent arrows) in the merged column header to systematically pull the requested performance metrics into the flattened query workspace.

7. Data Cleansing & Key Deduplication Strategies

Missing Value Resolution Strategy:

Metrics: Retain explicit null flags in performance metrics like Profit or Amount if they signify non-transaction lines.

Attributes: Missing structural descriptive text fields (e.g., City or State) should be transformed via Replace Values from null to "Unknown".


8. Structural Sorting & Query Filtering

Chronological Sorting: Within the Orders Data table, click the dropdown on Order Date and execute a Sort Descending rule to prioritize immediate visual data freshness.

Geographic Filtering: Isolate regional segments by clicking the dropdown filter on State and selecting specific states (e.g., Tamil Nadu).

9. Query Duplication & Downstream Aggregations

Granular Product Aggregations: 

Right-click Order Details in the Queries pane and select Duplicate. Rename this reporting layer to Order Details Aggregations. Navigate to Transform > Group By > Advanced:

Group variables by: Category and Sub-Category.

Define metric 1: Count of Order ID $\rightarrow$ 

Operation: Count Rows.

Define metric 2: Average Profit $\rightarrow$ 

Operation: Average on column Profit.

Define metric 3: Total Amount $\rightarrow$ 

Operation: Sum on column Amount.
