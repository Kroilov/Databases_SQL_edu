### 1. Создайте представление, в которое попадет информация о пользователях (имя, фамилия, город и пол), которые не старше 20 лет.

```mySQL
CREATE OR REPLACE VIEW v_user 
AS SELECT firstname, lastname, hometown, gender 
FROM users u JOIN profiles p ON p.user_id = u.id 
WHERE ((YEAR(CURRENT_DATE) - YEAR(p.birthday)) - (RIGHT(CURRENT_DATE, 5) < RIGHT(p.birthday, 5))) < 21;

SELECT firstname, lastname, hometown, gender FROM v_user;
```
![image](https://user-images.githubusercontent.com/118007838/230638592-17b76d5d-fd67-47e0-8cbf-b7eeddf3aa4c.png)


### 2. Найдите кол-во, отправленных сообщений каждым пользователем и выведите ранжированный список пользователей, указав имя и фамилию пользователя, количество отправленных сообщений и место в рейтинге (первое место у пользователя с максимальным количеством сообщений)
```mySQL
SELECT firstname, lastname, count_sent_message, 
DENSE_RANK() OVER (ORDER BY count_sent_message DESC) as 'place'
FROM ( SELECT from_user_id, COUNT(*) as count_sent_message 
FROM messages GROUP BY from_user_id ) AS rank_user_message 
JOIN users ON users.id = rank_user_message.from_user_id 
ORDER BY count_sent_message DESC;
```
![image](https://user-images.githubusercontent.com/118007838/230640126-398069fd-5b8d-4f58-a7d8-ba4d24d3ab08.png)


### 3. Выберите все сообщения, отсортируйте сообщения по возрастанию даты отправления (created_at) и найдите разницу дат отправления между соседними сообщениями, получившегося списка.
```mySQL
SELECT from_user_id as 'from', 
to_user_id as 'to whom', 
body as 'text', 
created_at as 'created', 
(LAG(created_at) OVER (ORDER BY created_at) - created_at) / -100 AS 'time diff' 
FROM messages ORDER BY created_at;
```
![image](https://user-images.githubusercontent.com/118007838/230639810-9539fe8b-139a-4ed4-b2e1-2ce30f4085d3.png)

### 4. 
