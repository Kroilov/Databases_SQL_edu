### 1. Подсчитать общее количество лайков, которые получили пользователи младше 12 лет.
```mySQL
SELECT COUNT(*) as total_likes
FROM likes
JOIN profiles ON likes.user_id = profiles.user_id
WHERE TIMESTAMPDIFF(YEAR, profiles.birthday, CURDATE()) < 12;
```
![image](https://user-images.githubusercontent.com/118007838/227801008-50eeb4ec-9a9c-4cb9-bd0b-571b79faa590.png)

### 2. Определить кто больше поставил лайков (всего): мужчины или женщины.
```mySQL
SELECT profiles.gender, COUNT(likes.user_id) as total_likes
FROM likes
JOIN profiles ON likes.user_id = profiles.user_id
GROUP BY profiles.gender;
```
![image](https://user-images.githubusercontent.com/118007838/227801172-e323badc-f71a-41a8-98e1-deb25ddab92e.png)

### 3. Вывести всех пользователей, которые не отправляли сообщения.
```mySQL
SELECT users.*
FROM users
LEFT JOIN messages ON users.id = messages.from_user_id
WHERE messages.from_user_id IS NULL;
```
![image](https://user-images.githubusercontent.com/118007838/227801348-ae563e7a-2593-44c6-a07b-a4017832589a.png)

### 4. Пусть задан некоторый пользователь. Из всех друзей этого пользователя найдите человека, который больше всех написал ему сообщений.
```mySQL
SELECT users.firstname, users.lastname, COUNT(*) AS messages_count
FROM users
JOIN messages ON users.id = messages.from_user_id
WHERE messages.to_user_id = 1
GROUP BY messages.from_user_id
ORDER BY messages_count DESC
LIMIT 1;
```
![image](https://user-images.githubusercontent.com/118007838/227801720-c3513cfa-c5af-46a9-9db8-ed129736c059.png)
