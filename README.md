# MYSQL_JSON
activity made by Sir Paweks

1.1.SELECT name, description FROM products;
![1 1](https://github.com/palenken/MYSQL_JSON/assets/150796420/6ec2f17b-4f71-4778-b019-9de2c29129b6)

1.2.SELECT  name, description, 
            JSON_EXTRACT(attributes,'$.color') AS color,
            JSON_EXTRACT(attributes,'$.size') AS size,
            JSON_EXTRACT(attributes,'$.prize') AS prize
    FROM products;
![1 2](https://github.com/palenken/MYSQL_JSON/assets/150796420/13487ad3-c185-4056-a161-eea1595eb172)

2.1.SELECT o.order_date, o.customer_id, p.name AS product_name,
           od.quantity, od.price
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    JOIN products p ON od.product_id = p.product_id;
![2 1](https://github.com/palenken/MYSQL_JSON/assets/150796420/41ca1b0a-e255-4996-ab30-05314a8b1f22)

2.2.SELECT o.order_id, SUM(od.quantity * od.price) AS total_cost
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    GROUP BY o.order_id;
![2 2](https://github.com/palenken/MYSQL_JSON/assets/150796420/3765bf6f-66aa-4ff9-9f45-5d528a03ab15)

3.1.SELECT * FROM products WHERE JSON_EXTRACT(attributes,'$.prize') > 50;
![3 1](https://github.com/palenken/MYSQL_JSON/assets/150796420/83e71fe9-ffc3-4d64-82b9-50df35911309)
3.2.SELECT name, JSON_EXTRACT(attributes,'$.prize') AS price
    FROM products
    JSON_EXTRACT(attributes,'$.color') = 'Salmon'
    AND JSON_EXTRACT(attributes,'$.brand') = 'Martin-Smith';
![3 2](https://github.com/palenken/MYSQL_JSON/assets/150796420/2f155e1c-50f8-4695-885a-ba9c7308123b)

4.1.SELECT p.name, SUM(od.quantity * od.price) AS total_revenue
    FROM products p
    JOIN order_details od ON p.product_id = od.product_id
    GROUP BY p.name;
![4 1](https://github.com/palenken/MYSQL_JSON/assets/150796420/9f4b8df5-61ad-4f4c-9925-acb854656983)
4.2.SELECT p.name, SUM(od.quantity) AS total_quantity_ordered
    FROM products p
    JOIN order_details od ON p.product_id = od.product_id
    GROUP BY p.name;
![4 2](https://github.com/palenken/MYSQL_JSON/assets/150796420/fb5e084c-47da-4d23-b930-147f0131039b)

5.1.SELECT p.name, SUM(od.quantity) AS total_quantity_sold
    FROM products p
    JOIN order_details od ON p.product_id = od.product_id
    GROUP BY p.name
    ORDER BY total_quantity_sold DESC
    LIMIT 5;
![5 1](https://github.com/palenken/MYSQL_JSON/assets/150796420/4456dcd5-2140-4020-9ab5-d00baf9019dd)
5.2.SELECT AVG(CAST(JSON_EXTRACT(attributes,'$.prize') AS DECIMAL)) AS avg_price
    FROM products
    WHERE JSON_EXTRACT(attributes,'$.brand') = 'Meyer Inc';
![5 2](https://github.com/palenken/MYSQL_JSON/assets/150796420/b0bc162d-dc4d-4d19-9a70-a98b81074c07)

6.1.SELECT JSON_EXTRACT(attributes,'$.color') AS color,
            JSON_EXTRACT(attributes,'$.size') AS size
    FROM products
    WHERE product_id = 1;
![6 1](https://github.com/palenken/MYSQL_JSON/assets/150796420/ab611c33-5c23-4e99-9ee3-d7e11d3bfeed)
6.2.SELECT JSON_EXTRACT(attributes,'$.color') AS color,
            JSON_EXTRACT(attributes,'$.size') AS size,
            JSON_EXTRACT(attributes,'$.prize') AS prize,
            JSON_EXTRACT(attributes,'$.brand') AS brand
    FROM products;
    ![6 2](https://github.com/palenken/MYSQL_JSON/assets/150796420/94d27d81-0662-4828-bf5d-c5011097c7ce)

7.1.SELECT o.order_id, o.order_date, o.customer_id, p.name AS product_name,
       od.quantity
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    JOIN products p ON od.product_id = p.product_id;
    ![7 1](https://github.com/palenken/MYSQL_JSON/assets/150796420/592ab790-7d98-4e1d-807a-ec52a2b491dd)
7.2.SELECT o.customer_id, SUM(od.quantity * od.price) AS total_revenue
    FROM orders o
    JOIN order_details od ON o.order_id = od.order_id
    GROUP BY o.customer_id;
    ![7 2](https://github.com/palenken/MYSQL_JSON/assets/150796420/e65bb10f-4fe2-4126-b14f-d132731d2931)

8.1.UPDATE products
    SET attributes = JSON_SET(attributes, '$.price', '61')
    WHERE product_id = 1;
![8 1 after](https://github.com/palenken/MYSQL_JSON/assets/150796420/19bc08c7-b54c-44c8-88ba-187647d46f9a)
![8 1 before  (1)](https://github.com/palenken/MYSQL_JSON/assets/150796420/1bc42c00-8825-4de2-9126-092e6a605546)
![8 1 query  (3)](https://github.com/palenken/MYSQL_JSON/assets/150796420/5127cf53-7442-485e-a1c8-e70c1c4be2ac)

8.2.UPDATE products
    SET attributes = JSON_SET(attributes, '$.bagong_COlumn ', 'mao_NANI');
![8 2 query](https://github.com/palenken/MYSQL_JSON/assets/150796420/2533984a-f746-4cd0-981b-d95a54b11a63)

9.1.SELECT *
    FROM products
    WHERE JSON_CONTAINS_PATH(attributes, 'one', '$.color') = 1;
![9](https://github.com/palenken/MYSQL_JSON/assets/150796420/17bf1941-d654-4479-9274-156f9aeec14a)

9.2. SELECT JSON_EXTRACT(attributes, '$.color[0]') AS first_feature
      FROM products;
![Uploading 9.2.png…]()
