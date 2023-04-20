![SQL WITH RAHUL](https://user-images.githubusercontent.com/113444489/233425026-a6e4da71-90e8-4423-86ac-743e9f54257c.png)
![Untitled design](https://user-images.githubusercontent.com/113444489/233426320-208a7a86-2bf7-4104-9a3e-c6049f15056b.png)


📌 Ingest a csv, create a table, and load data


```sql 
  
  -- Create a sales table 
  DROP TABLE IF EXISTS symbolic-truth-379604.bellabeat.sales;
  CREATE TABLE symbolic-truth-379604.bellabeat.sales (
    sale_id INT64 NOT NULL,
    sale_date DATE NOT NULL,
    product_name STRING NOT NULL,
    price NUMERIC NOT NULL,
    quantity INT64 NOT NULL,
    customer_name STRING NOT NULL
  );

  -- Load sample data into the sales table
  INSERT INTO symbolic-truth-379604.bellabeat.sales (sale_id, sale_date, product_name, price, quantity, customer_name)
  VALUES
    (1, '2022-01-01', 'Product A', 100.00, 2, 'A'),
    (2, '2022-01-02', 'Product B', 50.00, 1, 'B'),
    (3, '2022-01-03', 'Product C', 75.00, 3, 'C'),
    (4, '2022-01-04', 'Product A', 100.00, 1, 'D'),
    (5, '2022-01-05', 'Product B', 50.00, 2, 'E');
```

📌 Show all the information about only those customers who purchased `Product A' only

```sql
  
  -- select all data where product name is A
  SELECT *
  FROM symbolic-truth-379604.bellabeat.sales
  WHERE product_name = 'Product A'
```

![a1](https://user-images.githubusercontent.com/113444489/231825869-e7ec90ea-f987-4169-9497-152d570b604d.png)



![Untitled design (1)](https://user-images.githubusercontent.com/113444489/233427941-297030ab-88b8-4ead-a7d2-b7bd6d1b3ede.png)


📌 Use SQL JOINS to Combine Multiple Tables into a New Table

Below, I join two tables within the warehouse_orders dataset.


![p01](https://user-images.githubusercontent.com/113444489/231931590-43baf8b7-3b32-4925-9b4f-f051ae169041.png)


```sql
  
  -- order table
  
  WITH order_cte AS (
  SELECT *
  FROM symbolic-truth-379604.warehouse_orders.order_table
  WHERE order_date > '2019-01-01'
  ),
  
  -- warehouse table
  
  warehouse_cte AS (
  SELECT warehouse_id, employee_total
  FROM symbolic-truth-379604.warehouse_orders.warehouse_table
  )
  
  -- join both tables
  
  SELECT order_cte.*, warehouse_cte.employee_total
  FROM order_cte
  LEFT JOIN warehouse_cte
  ON order_cte.warehouse_id = warehouse_cte.warehouse_id;
```

![p02](https://user-images.githubusercontent.com/113444489/231931898-cd340ee3-0982-4331-89a4-db6b5086b1ca.png)


![Untitled design (2)](https://user-images.githubusercontent.com/113444489/233427982-1b72a0b6-43b7-4a0d-b2bd-3dd8bd3f0255.png)


📌 Create one or more views — with output

```sql
    SELECT * FROM Products
```

![p001](https://user-images.githubusercontent.com/113444489/231936887-5a66059e-2d65-4c0a-873f-6cd0e352fac6.png)

Let's create a view for products above average price

```sql
    
    -- create a view
    
    CREATE VIEW Products_above_average_price AS
    SELECT ProductName, Price
    FROM Products
    WHERE Price > (SELECT AVG(Price) FROM Products);
```

```sql
    
    -- query from view
    
    SELECT *
    FROM Products_above_average_price
 ```
 
 ![p002](https://user-images.githubusercontent.com/113444489/231937659-ee7ac805-ce61-4b61-8c64-e74f1afd0994.png)


![LEVEL 4](https://user-images.githubusercontent.com/113444489/233428016-99b4e888-9855-4a8e-b256-4e28747ea02c.png)



📌 Write a SQL script that should include some of these elements:

- Variable declarations for values used repeatedly
- Dynamic filtering, i.e. using CURRENT_DATE() instead of a STRING DATE
- In-line comments to explain the flow of execution
- Proper documentation

📌 write a sql script that shows the number of orders that were deleted( placed more than 90 days ago) 

```sql

  -- This script deletes all orders that were placed more than 90 days ago.
  -- It uses a variable to store the cutoff date and dynamic filtering with CURRENT_DATE().
  -- The script is properly documented with comments to explain each step.

  -- Declare a variable to store the cutoff date
     DECLARE @cutoff_date DATE;

  -- Set the cutoff date to 90 days ago from the current date
     SET @cutoff_date = DATEADD(day, -90, CURRENT_DATE());

  -- Delete orders that were placed before the cutoff date
     DELETE FROM orders
     WHERE order_date < @cutoff_date;

  -- Display the number of orders that were deleted
     SELECT COUNT(*) AS num_deleted
     FROM orders
     WHERE order_date < @cutoff_date;
```

|num_deleted|
|---|
|51|
 
 

![LEVEL 4 (1)](https://user-images.githubusercontent.com/113444489/233428050-f473f513-b816-4dfe-a2c9-c9bfe96f28e1.png)

📌 Create a Dashboard








