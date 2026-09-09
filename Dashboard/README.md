### 1. Understanding the Data

First, I started by understanding the dataset and the purpose of each table.

For each table, I asked four main questions:

* What does this table represent?
* What is the primary key?
* Which columns can connect it to other tables?
* What business questions can I answer using this table?

I also went through the columns one by one to understand what information each column contains and how it could be useful from a business point of view.

I tried to think like a company owner and ask: **What can I learn from this data?**

--
### 2. Understanding the Relationships

After understanding each table, I started thinking about how the tables could be connected.

I identified the primary keys and foreign keys, such as `Order ID`, `Product ID`, `Customer ID`, and `Supplier ID`.

These keys allow me to connect the tables and use information from different tables together.

For example, by connecting Orders with Shipments, I could use the order date, shipment date, and delivery date to get useful information such as:

* Shipping Days
* Delivery Days
* Total Delivery Days

I also identified the data needed to calculate Revenue.

--

### 3. Data Preparation – Power Query

After understanding the data, I started preparing it using Power Query.

I checked the tables for:

* Duplicate values
* Null values
* Correct data types

I also added some useful columns, such as `Full Name` and `Revenue`.

The goal was to make sure the data was clean and ready for the next step.

--

### 4. Data Modeling – Power Pivot

After preparing the data, I moved to Power Pivot to build the data model.

I created relationships between the tables using the primary and foreign keys.

The main relationships were:

* Customers → Orders
* Orders → Order Items
* Products → Order Items
* Suppliers → Products
* Orders → Payments
* Orders → Shipments
* Customers → Reviews
* Products → Reviews

I also calculated:

**Shipping Days**

```DAX
=DATEDIFF(
    RELATED(Orders[order_date]),
    Shipments[shipment_date],
    DAY
)
```

**Delivery Days**

```DAX
=DATEDIFF(
    Shipments[shipment_date],
    Shipments[delivery_date],
    DAY
)
```

**Total Delivery Days**

```DAX
=DATEDIFF(
    RELATED(Orders[order_date]),
    Shipments[delivery_date],
    DAY
)
```

--

### 5. KPIs

Next, I created KPIs to summarize the main information in a few numbers.

The KPIs were:

* **Total Revenue**
* **Total Orders**
* **Total Customers**
* **Total Quantity**
* **Average Order Value**
* **Average Total Delivery Days**

These KPIs give a quick overview of the overall business performance.

--

### 6. Analysis

After building the data model and KPIs, I started analyzing the data to answer different business questions.

For example:

* Which customers generate the highest revenue?
* Which suppliers generate the highest revenue?
* Which months have the highest sales?
* How are the ratings distributed?
* Which categories have the highest average rating?

These analyses helped me understand the business from different angles and find useful information from the data.

--

### 7. Interactive Dashboard

Finally, I created an interactive dashboard using PivotTables and PivotCharts.

I added slicers for:

* **Year**
* **Category**
* **Supplier Name**

This allows the user to filter the dashboard and easily explore the results for different years, categories, and suppliers.

The final dashboard brings the main KPIs and analysis together in one place.

