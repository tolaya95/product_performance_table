# product_performance_table
This query creates a table called product_performance that stores aggregated sales data for each product in the online_shop_2024 database.
USE online_shop_2024;
CREATE TABLE product_performance (
    product_name VARCHAR(255),
    total_quantity INT,
    total_sales DECIMAL(10, 2)
);
INSERT INTO product_performance (product_name, total_quantity, total_sales)
SELECT p.product_name, 
       SUM(oi.quantity) AS total_quantity, 
       SUM(oi.quantity * oi.price_at_purchase) AS total_sales
FROM order_items oi
INNER JOIN products p ON oi.product_id = p.product_id
GROUP BY p.product_name;
