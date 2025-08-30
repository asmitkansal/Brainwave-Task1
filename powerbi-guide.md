# Power BI Dashboard Creation Guide - Commercial Store Sales Analysis

## Prerequisites
- Microsoft Power BI Desktop (free download from Microsoft)
- Sales data CSV files (provided in analysis)

## Step 1: Data Import and Setup

### 1.1 Import the Main Dataset
1. Open Power BI Desktop
2. Click "Get Data" > "Text/CSV"
3. Select the `commercial_store_sales_data.csv` file
4. Preview the data and click "Transform Data" to open Power Query Editor

### 1.2 Data Cleaning and Transformation
In Power Query Editor:
1. **Date Column**: Change data type to "Date" for the date column
2. **Numeric Columns**: Ensure all financial columns (total, unit_price, vat, etc.) are set to "Decimal Number"
3. **Text Columns**: Set branch, city, customer_type, gender, product_line, payment_method as "Text"
4. **Add Calculated Columns**:
   - Month: `Date.MonthName([date])`
   - Year: `Date.Year([date])`
   - Day of Week: `Date.DayOfWeekName([date])`
   - Hour: Extract hour from time column

### 1.3 Create Date Table
1. Go to "Modeling" tab > "New Table"
2. Create a date table: `DateTable = CALENDAR(MIN(sales_data[date]), MAX(sales_data[date]))`
3. Add columns for Month, Quarter, Year using DAX functions

## Step 2: Data Modeling

### 2.1 Relationships
1. Create relationship between DateTable[Date] and sales_data[date]
2. Mark DateTable as Date Table in "Table Tools"

### 2.2 Measures Creation
Create the following measures in the "Modeling" tab:

```DAX
Total Revenue = SUM(sales_data[total])
Total Transactions = COUNT(sales_data[invoice_id])
Average Transaction Value = DIVIDE([Total Revenue], [Total Transactions])
Total Gross Income = SUM(sales_data[gross_income])
Gross Profit Margin = DIVIDE([Total Gross Income], [Total Revenue]) * 100
Average Rating = AVERAGE(sales_data[rating])
Total Quantity Sold = SUM(sales_data[quantity])
```

## Step 3: Dashboard Layout Setup

### 3.1 Page Setup
1. Go to "View" tab > "Page view" > set to "Fit to Width"
2. In Format pane > Page > set custom size 1920x1080 for full HD
3. Set page background color to light gray (#F8F9FA)

### 3.2 Header Section
1. Insert Text Box for title "Commercial Store Sales Analytics Dashboard"
2. Format: Arial, 24pt, Bold, Dark Blue (#1F2937)
3. Add company logo placeholder using Shapes > Rectangle

## Step 4: KPI Cards Creation

Create 5 KPI cards in the top row:

### 4.1 Total Revenue Card
1. Insert "Card" visualization
2. Drag "Total Revenue" measure to Values
3. Format: 
   - Data Label: Font size 32, Bold
   - Category Label: "Total Revenue"
   - Background: Light Blue (#EBF8FF)

### 4.2 Total Transactions Card
1. Insert "Card" visualization  
2. Drag "Total Transactions" measure to Values
3. Format similar to Revenue card with Green background (#F0FDF4)

### 4.3 Average Transaction Value Card
1. Insert "Card" visualization
2. Drag "Average Transaction Value" measure to Values  
3. Format with Orange background (#FFF7ED)

### 4.4 Gross Profit Margin Card
1. Insert "Card" visualization
2. Drag "Gross Profit Margin" measure to Values
3. Add "%" symbol in formatting
4. Format with Purple background (#F3E8FF)

### 4.5 Average Rating Card  
1. Insert "Card" visualization
2. Drag "Average Rating" measure to Values
3. Format with Teal background (#F0FDFA)

## Step 5: Main Visualizations

### 5.1 Branch Performance Bar Chart
1. Insert "Clustered Column Chart"
2. X-axis: branch
3. Y-axis: Total Revenue measure
4. Add data labels showing values
5. Format:
   - Colors: Blue gradient
   - Title: "Sales Performance by Branch"
   - X-axis title: "Branch"
   - Y-axis title: "Revenue ($)"

### 5.2 Product Line Revenue Bar Chart
1. Insert "Clustered Bar Chart" (horizontal)
2. Y-axis: product_line  
3. X-axis: Total Revenue measure
4. Sort by Total Revenue (descending)
5. Format:
   - Colors: Teal gradient  
   - Title: "Revenue by Product Line"
   - Data labels: On

### 5.3 Monthly Sales Trend Line Chart
1. Insert "Line Chart"
2. X-axis: DateTable[Month] 
3. Y-axis: Total Revenue measure
4. Add markers for data points
5. Format:
   - Line color: Dark blue
   - Title: "Monthly Sales Trends 2024"
   - Y-axis: Format as currency

### 5.4 Payment Method Pie Chart
1. Insert "Pie Chart"
2. Legend: payment_method
3. Values: Total Revenue measure  
4. Format:
   - Show percentages
   - Title: "Payment Method Distribution"
   - Legend position: Right

### 5.5 Customer Segmentation Stacked Bar Chart
1. Insert "Stacked Column Chart"
2. X-axis: customer_type
3. Y-axis: Total Revenue measure
4. Legend: gender
5. Format:
   - Colors: Custom (Blue for Male, Pink for Female)
   - Title: "Sales by Customer Segment"

### 5.6 Customer Satisfaction Scatter Plot
1. Insert "Scatter Chart"
2. X-axis: total (transaction value)
3. Y-axis: rating (customer rating)
4. Legend: product_line
5. Format:
   - Different colors for each product line
   - Title: "Transaction Value vs Customer Rating"
   - Add trend line if needed

## Step 6: Interactive Filters (Slicers)

### 6.1 Branch Filter
1. Insert "Slicer" visualization
2. Field: branch
3. Format as dropdown
4. Position in left sidebar

### 6.2 Product Line Filter  
1. Insert "Slicer" visualization
2. Field: product_line
3. Format as list with checkboxes
4. Position below branch filter

### 6.3 Customer Type Filter
1. Insert "Slicer" visualization  
2. Field: customer_type
3. Format as button style
4. Position in sidebar

### 6.4 Payment Method Filter
1. Insert "Slicer" visualization
2. Field: payment_method  
3. Format as tiles
4. Position in sidebar

### 6.5 Date Range Filter
1. Insert "Slicer" visualization
2. Field: DateTable[Date]
3. Format as date range slider
4. Position at top of sidebar

## Step 7: Advanced Formatting and Interactions

### 7.1 Color Theme
1. Go to "View" tab > "Themes"
2. Select or create custom theme with:
   - Primary: #1F2937 (Dark Gray)
   - Secondary: #3B82F6 (Blue) 
   - Accent: #10B981 (Teal)

### 7.2 Cross-Filtering Setup
1. Select each visualization
2. Go to "Format" > "Edit interactions"  
3. Set appropriate filter/highlight relationships
4. Ensure slicers affect all relevant visuals

### 7.3 Tooltips Enhancement
1. For each chart, go to "Format" pane
2. Enable "Tooltips" 
3. Add relevant fields for detailed information
4. Customize tooltip pages if needed

## Step 8: Mobile Layout (Optional)

### 8.1 Mobile View Setup  
1. Go to "View" tab > "Mobile layout"
2. Arrange visuals for mobile viewing
3. Prioritize KPIs and most important charts
4. Test on different mobile sizes

## Step 9: Publishing and Sharing

### 9.1 Save and Publish
1. Save the .pbix file locally
2. Click "Publish" to publish to Power BI Service
3. Select appropriate workspace

### 9.2 Dashboard Creation in Service
1. In Power BI Service, go to your published report
2. Pin key visuals to a new dashboard
3. Arrange tiles in logical order
4. Set up automatic refresh schedule

## Step 10: Advanced Features

### 10.1 Bookmarks for Navigation
1. Create bookmarks for different views
2. Add navigation buttons
3. Set up story flow for presentations

### 10.2 Row-Level Security (if needed)
1. Define RLS roles in Power BI Desktop
2. Set up user permissions
3. Test security implementation

### 10.3 Alert Configuration
1. Set up data alerts for KPIs
2. Configure threshold values  
3. Set notification preferences

## Troubleshooting Tips

1. **Performance Issues**: Reduce data granularity, use aggregations
2. **Relationship Errors**: Check data types and cardinality
3. **Measure Errors**: Verify DAX syntax and context
4. **Visual Issues**: Check field data types and formatting

## Best Practices

1. **Consistent Formatting**: Use same fonts, colors, and sizes
2. **Clear Titles**: Descriptive and concise chart titles
3. **Appropriate Charts**: Match visualization type to data story
4. **White Space**: Don't overcrowd the dashboard
5. **User Testing**: Get feedback from end users
6. **Documentation**: Maintain data dictionary and user guide

This guide will help you recreate the comprehensive sales analytics dashboard in Power BI with full interactivity and professional presentation.