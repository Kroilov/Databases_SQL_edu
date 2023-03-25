```mySQL
CREATE TABLE staff 
(
	id INT AUTO_INCREMENT PRIMARY KEY, 
	firstname VARCHAR(45),
	lastname VARCHAR(45),
	post VARCHAR(100),
	seniority INT, 
	salary INT, 
	age INT
);

INSERT INTO staff (firstname, lastname, post, seniority, salary, age)
VALUES
  ('Вася', 'Петров', 'Начальник', '40', 100000, 60),
  ('Петр', 'Власов', 'Начальник', '8', 70000, 30),
  ('Катя', 'Катина', 'Инженер', '2', 70000, 25),
  ('Саша', 'Сасин', 'Инженер', '12', 50000, 35),
  ('Иван', 'Иванов', 'Рабочий', '40', 30000, 59),
  ('Петр', 'Петров', 'Рабочий', '20', 25000, 40),
  ('Сидр', 'Сидоров', 'Рабочий', '10', 20000, 35),
  ('Антон', 'Антонов', 'Рабочий', '8', 19000, 28),
  ('Юрий', 'Юрков', 'Рабочий', '5', 15000, 25),
  ('Максим', 'Максимов', 'Рабочий', '2', 11000, 22),
  ('Юрий', 'Галкин', 'Рабочий', '3', 12000, 24),
  ('Людмила', 'Маркина', 'Уборщик', '10', 10000, 49);
```

### 1. Отсортируйте данные по полю заработная плата (salary) в порядке: убывания; возрастания
```mySQL
SELECT firstname, lastname, post, seniority, salary, age
FROM staff
ORDER BY salary DESC;
```
![image](https://user-images.githubusercontent.com/118007838/227710857-98394950-c847-47c1-a3ad-23e8e6b132e8.png)

### 2. Выведите 5 максимальных заработных плат (saraly)
```mySQL
SELECT salary, post, firstname, lastname
FROM staff
ORDER BY salary DESC
LIMIT 5;
```
![image](https://user-images.githubusercontent.com/118007838/227710979-0d560081-e0f1-4b84-b9c6-3f2cde5354e6.png)

### 3. Посчитайте суммарную зарплату (salary) по каждой специальности (роst)
```mySQL
SELECT post, SUM(salary) as total_salary
FROM staff
GROUP BY post;
```
![image](https://user-images.githubusercontent.com/118007838/227711053-a02caa89-5584-43b5-a59b-0a09a2353534.png)

### 4. Найдите кол-во сотрудников с специальностью (post) «Рабочий» в возрасте от 24 до 49 лет включительно
```mySQL
SELECT COUNT(*) AS num_workers
FROM staff
WHERE post = 'Рабочий' AND age BETWEEN 24 AND 49;
```
![image](https://user-images.githubusercontent.com/118007838/227711217-e590f04f-8070-46e0-8555-0b1292a8ac7b.png)

### 5. Найдите количество специальностей
```mySQL
SELECT COUNT(DISTINCT post) AS num_posts
FROM staff;
```
![image](https://user-images.githubusercontent.com/118007838/227711287-700b4e23-e2ed-4c63-a5b3-905c68b8ebdc.png)

### 6. Выведите специальности, у которых средний возраст сотрудников меньше 30 лет
Меньше 30 таблица пустая, изменил на 34:

```mySQL
SELECT post
FROM staff
GROUP BY post
HAVING AVG(age) < 34;
```

![image](https://user-images.githubusercontent.com/118007838/227711442-590fb860-0cfd-4203-83dd-eaa70251bfb0.png)
