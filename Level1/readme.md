Welcome to the very first level of my sql game!

Level 1

Task 1: Ingest a csv, create a table, and load data

Tools used: Google Bigquery

```sql 
  
  -- Create the sales table 
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

Task 2: Show all the information about only those customers who purchased `Product A' only

```sql
  
  -- select all data where product name is A
  SELECT *
  FROM symbolic-truth-379604.bellabeat.sales
  WHERE product_name = 'Product A'
```

![a1](https://user-images.githubusercontent.com/113444489/231825869-e7ec90ea-f987-4169-9497-152d570b604d.png)


--


LEVEL 2

Task: Use SQL JOINS to Combine Multiple Tables into a New Table

Below, I join two tables within the warehouse_orders dataset.


![p01](https://user-images.githubusercontent.com/113444489/231931590-43baf8b7-3b32-4925-9b4f-f051ae169041.png)


Tools used: `Google Bigquery`

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


LEVEL 3

TASK: Create one or more views — with output

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



LEVEL 4

TASK: Write a SQL script








