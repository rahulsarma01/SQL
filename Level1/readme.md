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
  SELECT *
  FROM symbolic-truth-379604.bellabeat.sales
  WHERE product_name = 'Product A'
```

![a1](https://user-images.githubusercontent.com/113444489/231825869-e7ec90ea-f987-4169-9497-152d570b604d.png)


--


LEVEL 2

Task: Use SQL JOINS to Combine Multiple Tables into a New Table







