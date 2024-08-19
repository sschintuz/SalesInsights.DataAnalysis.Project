# Sales Insights Power BI Project

## Project Overview
This project involves analyzing sales data using SQL and Power BI. The goal is to extract meaningful insights from the sales transactions data, focusing on various metrics such as customer records, market-specific transactions, revenue, and more.

## Getting Started

### Prerequisites
Before starting, ensure you have the following installed on your local machine:
- MySQL (for running SQL queries)
- Power BI Desktop (for data visualization)

### MySQL Setup Instructions
1. **Install MySQL**: Follow the steps in [this video](https://www.youtube.com/watch?v=WuBcTJnIuzo) to install MySQL on your local computer.

2. **Import the Database**:
    - Download the `db_dump.sql` file from this repository.
    - Import the database dump file into MySQL as per the instructions provided in the tutorial video linked above.

### Data Analysis Using SQL
Once your MySQL setup is complete, you can run the following SQL queries to analyze the data:

1. **Show all customer records**:
    ```sql
    SELECT * FROM customers;
    ```

2. **Show total number of customers**:
    ```sql
    SELECT count(*) FROM customers;
    ```

3. **Show transactions for Chennai market (market code for Chennai is Mark001)**:
    ```sql
    SELECT * FROM transactions WHERE market_code='Mark001';
    ```

4. **Show distinct product codes that were sold in Chennai**:
    ```sql
    SELECT DISTINCT product_code FROM transactions WHERE market_code='Mark001';
    ```

5. **Show transactions where currency is US dollars**:
    ```sql
    SELECT * FROM transactions WHERE currency='USD';
    ```

6. **Show transactions in 2020 joined by date table**:
    ```sql
    SELECT transactions.*, date.* 
    FROM transactions 
    INNER JOIN date 
    ON transactions.order_date = date.date 
    WHERE date.year = 2020;
    ```

7. **Show total revenue in the year 2020**:
    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date 
    ON transactions.order_date = date.date 
    WHERE date.year = 2020 
    AND (transactions.currency = 'INR\r' OR transactions.currency = 'USD\r');
    ```

8. **Show total revenue in January 2020**:
    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date 
    ON transactions.order_date = date.date 
    WHERE date.year = 2020 
    AND date.month_name = 'January' 
    AND (transactions.currency = 'INR\r' OR transactions.currency = 'USD\r');
    ```

9. **Show total revenue in 2020 in Chennai**:
    ```sql
    SELECT SUM(transactions.sales_amount) 
    FROM transactions 
    INNER JOIN date 
    ON transactions.order_date = date.date 
    WHERE date.year = 2020 
    AND transactions.market_code = 'Mark001';
    ```

### Data Analysis Using Power BI

1. **Normalization Formula**:
    - To create a `norm_amount` column in Power BI, use the following formula:
    ```powerquery
    = Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
    ```

## Additional Information
- The SQL queries provided are used to extract specific insights from the database.
- The Power BI formula is used to normalize sales amounts by converting USD to INR.

## Conclusion
This project showcases the process of setting up a MySQL database, running SQL queries for data analysis, and visualizing insights using Power BI. By following the steps outlined above, you will be able to replicate the analysis and gain insights into the sales data.

