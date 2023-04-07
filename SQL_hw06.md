### 1. Создайте таблицу users_old, аналогичную таблице users. Создайте процедуру,  с помощью которой можно переместить любого (одного) пользователя из таблицы users в таблицу users_old. (использование транзакции с выбором commit или rollback – обязательно).
```mySQL
DROP PROCEDURE IF EXISTS replace_user;
DELIMITER //
CREATE PROCEDURE replace_user(user_id INT, to_old BOOLEAN)
BEGIN
    DECLARE _rollback BIT DEFAULT 0;
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION BEGIN SET _rollback = 1; END;
    IF to_old = 1 THEN
        START TRANSACTION;
        INSERT INTO users_old SELECT * FROM users WHERE id = user_id;
        DELETE FROM users WHERE id = user_id;
        IF _rollback THEN
            ROLLBACK;
        ELSE
            COMMIT;
        END IF;
    ELSE
        START TRANSACTION;
        INSERT INTO users SELECT * FROM users_old WHERE id = user_id;
        DELETE FROM users_old WHERE id = user_id;
        IF _rollback THEN
            ROLLBACK;
        ELSE
            COMMIT;
        END IF;
    END IF;
END//
DELIMITER ;
```

### 2. Создайте хранимую функцию hello(), которая будет возвращать приветствие, в зависимости от текущего времени суток. С 6:00 до 12:00 функция должна возвращать фразу "Доброе утро", с 12:00 до 18:00 функция должна возвращать фразу "Добрый день", с 18:00 до 00:00 — "Добрый вечер", с 00:00 до 6:00 — "Доброй ночи".
```mySQL
CREATE FUNCTION hello() RETURNS VARCHAR(12) READS SQL DATA
BEGIN
    DECLARE time_current INT;
    SET time_current = (SELECT HOUR(NOW()));
    IF time_current >= 6 AND time_current < 12 THEN
        RETURN "Good morning";
    ELSEIF time_current >= 12 AND time_current < 18 THEN
        RETURN "Good afternoon";
    ELSEIF time_current >= 18 AND time_current < 24 THEN
        RETURN "Good evening";
    ELSE
        RETURN "Good night";
    END IF;
END//
DELIMITER ;

SELECT hello();
```
![image](https://user-images.githubusercontent.com/118007838/230641819-b6ce1529-a71c-4a42-bea1-4c9af8389f2f.png)
