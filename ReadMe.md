## Designing a Vendor Analytics Pipeline Using Power Query

### Part 1: The Problem

AdventureWorks operates a transactional database with over 100 vendors. Decision-makers face significant challenges in conducting effective analysis:

1. **Limited Oversight:** With over 100 vendors, it’s difficult and time-consuming to review performance regularly. The lack of visibility into supplier performance issues reduces effective decision-making.
2. **Undefined KPIs:** The key performance indicators (KPIs) for evaluating vendors are not well-defined.
3. **Lack of Projects:** There are no existing projects focusing on vendor performance at AdventureWorks, making it hard to establish best practices.
4. **Disconnected Data:** There is no direct link between supplier performance and its impact.

### Part 2: The Solution

To address these challenges, we developed a comprehensive vendor performance tracking solution using Power Query in Power BI and Excel. The solution is a data pipeline that allows different types of analysis.

#### Goals of the Solution

- Create a solution usable in Power BI or Excel.
- Optimize data for analysis.
- Save time by targeting the right vendors or products.
- Provide control over the parameters of the KPIs.
- Allow discrimination by multiple dimensions.

### ETL Process Overview

We extracted relevant tables from the SQL database, including:

1. **Purchase Order Header Table**
2. **Purchase Order Detail Table:** Includes order-specific information such as order quantity, received quantity, rejected quantity, and dates.
3. **ProductVendor Table**
4. **Vendor Table:** Contains vendor details like name, credit rating, preferred status, and state.
5. **Product Table:** Contains product details including product name, safety stock levels, and reorder points.
6. **UnitMeasure Table**
7. **MonthTable:** Created as a date table.

#### Creating the Fact Table

We summarized monthly delivery performance in a fact table. This fact table answers key questions:

- **Order Quantity:** How many orders are there for each vendor-product association?
- **Delivery Performance:** For each association, how did the delivery go? Did they ship on time? Did we receive it on time?
- **Fulfillment Rate:** How well are we doing on fulfillment? Did we receive the full quantity we ordered? At what rate do we reject products?

**Step 1: Merge**

We merged the Purchase Order Header, Purchase Order Detail, and ProductVendor tables. This combined order details data (such as quantity ordered, received, and rejected by product) with header data (like date, vendor, shipping date, and order status). Using the product ID combined with the vendor ID, we could get specific contract information related to that vendor-product association. The fields combined include average lead time, minimum and maximum quantities, and unit measure.

**Step 2: Filters**

We created the YearMonth column to filter orders before the current month to avoid incomplete data. Although not necessary for our case since the data is from 2014, we also filtered to include only complete transactions.

**Step 3: Calculated Columns**

With the merged data, we calculated the following metrics:

1. **Days to Ship:** The number of business days between the order date and the ship date.
2. **Shipped On Time:** A binary value (1 or 0) indicating whether the order was shipped within the expected time frame.
3. **Order Fulfillment Rate:** The ratio of stocked quantity to ordered quantity.
4. **Rejected Quantity Rate:** The ratio of rejected quantity to received quantity.
5. **Expected Delivery Date:** The calculated date based on the order date and average lead time.
6. **Delivered On Time:** A binary value (1 or 0) indicating whether the order was delivered by the expected delivery date.

**Step 4: Aggregation**

We aggregated by month, vendor, product, and unit measure (optional). The resulting metrics are:

#### Key Metrics

We developed the following metrics to evaluate vendor performance:

1. **On-Time Delivery Rate:** Measures the percentage of orders delivered by the promised date.
2. **On-Time Shipped Rate:** Reflects the percentage of orders shipped on time.
3. **Order Fulfillment Rate:** The ratio of orders fully fulfilled to the total orders placed.
4. **Rejected Quantity Rate:** The percentage of items rejected due to non-compliance with quality standards.
5. **Overall Score:** A weighted average of all the above metrics to provide a comprehensive performance score.
6. **Most Common Issue:** Identifies the most frequent issue encountered with each supplier based on the lowest metric scores.

#### Parameters of Metrics

Users can set the following parameters to customize the analysis:

- **Days to Ship:** Default is 7 days.
- **Weight for Delivery:** Default is 0.
- **Weight for Shipping:** Default is 0.5.
- **Weight for Rejected:** Default is 0.2.
- **Weight for Fulfillment:** Default is 0.3.

#### Dimensions

1. **Vendor Dimension:** Includes vendor-specific details to help target regions and assess credit rating performance.
2. **Product Dimension:** Contains product information to evaluate stockout risks based on delivery performance.
3. **Delivery Type Dimension (Optional):** Differentiates performance based on delivery methods like containers, LTL, and full load.
4. **Month Table:** Generated programmatically to enhance time dimensions with additional layers such as peak seasons or specific months.

### Results

The final deliverables include:

- **PBIX File:** A Power BI file with the vendor performance dashboard.
- **Excel Sheets:** Data and analysis sheets for further manipulation and review.

### Analysis Examples

Using the provided tools, multiple analyses can be conducted, such as:

- **Vendor Performance Analysis:** Track and compare vendor performance over time.
- **Risk Analysis:** Evaluate potential risks based on delivery and fulfillment performance.

