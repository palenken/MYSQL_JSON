# MYSQL_JSON
activity made by Sir Paweks

1.1.SELECT name, description FROM products;
1.2.SELECT  name, description, 
            JSON_EXTRACT(attributes,'$.color') AS color,
            JSON_EXTRACT(attributes,'$.size') AS size,
            JSON_EXTRACT(attributes,'$.prize') AS prize
    FROM products;

2.1.SELECT o.order_date, o.customer_id, p.name AS product_name,
           od.quantity, od.price
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    JOIN products p ON od.product_id = p.product_id;
2.2.SELECT o.order_id, SUM(od.quantity * od.price) AS total_cost
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    GROUP BY o.order_id;

3.1.SELECT * FROM products WHERE JSON_EXTRACT(attributes,'$.prize') > 50;
3.2.SELECT name, JSON_EXTRACT(attributes,'$.prize') AS price
    FROM products
    JSON_EXTRACT(attributes,'$.color') = 'Salmon'
    AND JSON_EXTRACT(attributes,'$.brand') = 'Martin-Smith';

4.1.SELECT p.name, SUM(od.quantity * od.price) AS total_revenue
    FROM products p
    JOIN order_details od ON p.product_id = od.product_id
    GROUP BY p.name;

4.2.SELECT p.name, SUM(od.quantity) AS total_quantity_ordered
    FROM products p
    JOIN order_details od ON p.product_id = od.product_id
    GROUP BY p.name;

5.1.SELECT p.name, SUM(od.quantity) AS total_quantity_sold
    FROM products p
    JOIN order_details od ON p.product_id = od.product_id
    GROUP BY p.name
    ORDER BY total_quantity_sold DESC
    LIMIT 5;
5.2.SELECT AVG(CAST(JSON_EXTRACT(attributes,'$.prize') AS DECIMAL)) AS avg_price
    FROM products
    WHERE JSON_EXTRACT(attributes,'$.brand') = 'Meyer Inc';

6.1.SELECT JSON_EXTRACT(attributes,'$.color') AS color,
            JSON_EXTRACT(attributes,'$.size') AS size
    FROM products
    WHERE product_id = 1;
6.2.SELECT JSON_EXTRACT(attributes,'$.color') AS color,
            JSON_EXTRACT(attributes,'$.size') AS size,
            JSON_EXTRACT(attributes,'$.prize') AS prize,
            JSON_EXTRACT(attributes,'$.brand') AS brand
    FROM products;

7.1.SELECT o.order_id, o.order_date, o.customer_id, p.name AS product_name,
       od.quantity
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    JOIN products p ON od.product_id = p.product_id;
7.2.SELECT o.customer_id, SUM(od.quantity * od.price) AS total_revenue
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    GROUP BY o.customer_id;

8.1.UPDATE products
    SET attributes = JSON_SET(attributes, '$.price', '61')
    WHERE product_id = 1;
8.2.UPDATE products
    SET attributes = JSON_SET(attributes, '$.bagong_COlumn ', 'mao_NANI');

9.1.SELECT *
    FROM products
    WHERE JSON_CONTAINS_PATH(attributes, 'one', '$.color') = 1;
9.2. SELECT JSON_EXTRACT(attributes, '$.color[0]') AS first_feature
      FROM products;
