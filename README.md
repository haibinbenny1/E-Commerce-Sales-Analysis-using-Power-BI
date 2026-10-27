# E-Commerce Sales Analysis using Power BI

## 1. Calculated Columns

### 1.1 Category Type

**Description:** Combined Category and Sub-Category into one column.

**Explanation:** Used the `&` operator to combine both columns with a space.

```dax
Category Type = 'Order Details'[Category] & " " & 'Order Details'[Sub-Category]
```

### 1.2 Revenue per Order

**Description:** Created a column to calculate revenue for each row.

**Explanation:** Multiplied Amount by Quantity to calculate revenue.

```dax
Revenue per Order = 'Order Details'[Amount] * 'Order Details'[Quantity]
```

### 1.3 Sales Category

**Description:** Categorized sales as Above Average or Below Average.

**Explanation:** Used `IF()` and `AVERAGE()` to compare each Amount with the average Amount.

```dax
Sales Category = IF('Order Details'[Amount] > AVERAGE('Order Details'[Amount]), "Above Average", "Below Average")
```

## 2. Calculated Measures

### 2.1 Order Count

**Description:** Counted the Order ID entries in the Order Details table.

**Explanation:** Used `COUNT()` to count the Order ID entries.

```dax
Order Count = COUNT('Order Details'[Order ID])
```

### 2.2 Average Profit in Delhi

**Description:** Calculated the average profit for orders placed in Delhi.

**Explanation:** Used `CALCULATE()` and `AVERAGE()` to filter the data for Delhi.

```dax
Average Profit in Delhi = CALCULATE(AVERAGE('Order Details'[Profit]), 'List of Orders'[City] = "Delhi")
```

### 2.3 Year-to-Date (YTD) Sales

**Description:** Calculated total sales and accumulated YTD sales.

**Explanation:** Used `SUM()` and `TOTALYTD()` to calculate sales over time.

```dax
Total Sales = SUM('Order Details'[Amount])
```

```dax
YTD Sales = TOTALYTD([Total Sales], 'List of Orders'[Order Date])
```

## 3. Data Visualization

### 3.1 Sales Target Achievement by Category

**Description:** Created a clustered column chart to compare actual sales with sales targets by category.

**Explanation:** Used Actual Sales and Sales Target measures to compare category-wise performance.

```dax
Actual Sales = SUM('Order Details'[Amount])
```

```dax
Sales Target = SUM('Sales target'[Target])
```

### 3.2 Max Profit Margin by Sub-Category

**Description:** Created a donut chart to compare profit margins across sub-categories.

**Explanation:** Used Sub-Category and Profit Margin to display profitability.

```dax
Profit Margin = DIVIDE(SUM('Order Details'[Profit]), SUM('Order Details'[Amount]), 0)
```

### 3.3 Monthly Sales Trend

**Description:** Created a line chart to show monthly sales over time.

**Explanation:** Used Order Date on the X-axis and Total Sales on the Y-axis.

### 3.4 Comparison of Profit and Quantity by Sub-Category

**Description:** Created a scatter chart to compare profit and quantity sold across sub-categories.

**Explanation:** Used Quantity on the X-axis, Profit on the Y-axis, and Sub-Category to identify each data point.

### 3.5 Comparison of Total Sales Amount and Target

**Description:** Created Card visuals to display total sales and sales targets, along with a Multi-row Card to show the minimum target for each segment.

**Explanation:** Used Total Sales, Sales Target, and a minimum target measure for comparison.

```dax
Minimum Target = MIN('Sales target'[Target])
```

### 3.6 Sales Performance Matrix

**Description:** Created a matrix to compare actual sales with sales targets across categories and months.

**Explanation:** Used Category in Rows, Month in Columns, and Total Sales and Sales Target in Values.

### 3.7 Geographic Sales Analysis

**Description:** Created a map to display total sales across different cities.

**Explanation:** Used City as the location and Total Sales as the bubble size to identify regional sales patterns.

### 3.8 Sales Distribution by Sub-Category

**Description:** Created a treemap to show sales distribution across sub-categories.

**Explanation:** Used Sub-Category and Total Sales to compare sales values.

### 3.9 Order Count Analysis by State

**Description:** Created a funnel chart to visualize order counts across different states.

**Explanation:** Used State as the category and a distinct order count measure to compare order distribution.

```dax
Order Count by State = DISTINCTCOUNT('List of Orders'[Order ID])
```
