```mySQL
CREATE DATABASE hw01;
USE hw01;
CREATE TABLE mobile_phones(
	id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    product_name VARCHAR(45) NOT NULL,
    manufacturer VARCHAR(45) NOT NULL,
    product_count INT UNSIGNED,
    price INT UNSIGNED
    );
    
INSERT INTO mobile_phones(product_name, manufacturer, product_count, price)
VALUES
	('NOKIA 3310', 'Nokia', 344, 4300),
	('NOKIA 6600', 'Nokia', 12, 7300),
    ('iPhone XS', 'Apple', 43, 23544),
    ('iPhone 11', 'Apple', 12, 43333),
    ('P20', 'Huawei', 3, 30400);
SELECT * FROM mobile_phones;
```

![image](https://user-images.githubusercontent.com/118007838/226559643-9415adc7-909f-46dc-9006-f5aa42e7800b.png)

```mySQL
SELECT product_name, manufacturer, price
FROM mobile_phones
WHERE product_count > 12;
```

![image](https://user-images.githubusercontent.com/118007838/226561946-6c44108e-8988-4465-9699-ca5bdf7478d5.png)

```mySQL
SELECT product_name, product_count, price
FROM mobile_phones
WHERE manufacturer = 'Nokia';
```

![image](https://user-images.githubusercontent.com/118007838/226561580-57b0d9a7-303f-47a6-b794-23ba7cf10ea2.png)
