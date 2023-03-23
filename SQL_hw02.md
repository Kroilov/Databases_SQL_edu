```mySQL
CREATE TABLE sales
(
	  id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    order_date DATE,
    count_product INT UNSIGNED
);
INSERT INTO sales(order_date, count_product)
VALUES
	('2022-01-01', 156),
	('2022-01-02', 180),
	('2022-01-03', 21),
	('2022-01-04', 124),
	('2022-01-05', 341);

SELECT id,
	CASE
		    WHEN count_product < 100 THEN 'Small order'
        WHEN count_product >= 100 AND count_product <= 300 THEN 'Medium order'
        ELSE 'Large order'
	END AS order_type
FROM sales;
```
![image](https://user-images.githubusercontent.com/118007838/227318423-b4afe57d-9e85-4e6b-b8fe-0ec75c405f98.png)
```mySQL
CREATE TABLE orders
(
	  id INT AUTO_INCREMENT PRIMARY KEY,
	  employee_id VARCHAR(16) NOT NULL,
    amount FLOAT,
    order_status VARCHAR(16)
);

INSERT INTO orders(employee_id,	amount,	order_status)
VALUES
	('e03',	15.00, 'OPEN'),
	('e01', 25.50, 'OPEN'),
	('e05', 100.70,	'CLOSED'),
	('e02', 22.18, 'OPEN'),
	('e04', 9.50, 'CANCELLED');

SELECT id,
	CASE
		    WHEN order_status = 'OPEN' THEN 'Order is in open state'
        WHEN order_status = 'CLOSED' THEN 'Order is closed'
        WHEN order_status = 'CANCELLED' THEN 'Order is cancelled'
        ELSE 'Undefined'
	END AS full_order_status
FROM orders;
```
![image](https://user-images.githubusercontent.com/118007838/227318355-eddc820f-f116-4585-8e0f-23817ce967b8.png)


В контексте баз данных, 0 и NULL - это разные значения.

0 - это конкретное числовое значение, которое обозначает ноль; его использовать его в математических вычислениях.

NULL - это отсутствие значения; используется, когда нет конкретного значения для поля в строке таблицы.
