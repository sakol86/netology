# Домашнее задание к занятию 12.2. «Работа с данными (DDL/DML)» - Ковбаса Анна

---

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных.

![1-1](https://github.com/kovbasaad/12-2-homework/blob/main/img/1-1.JPG)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. 
![1-2](https://github.com/kovbasaad/12-2-homework/blob/main/img/1-2.JPG)
![1-3](https://github.com/kovbasaad/12-2-homework/blob/main/img/1-3.JPG)

1.6. Переподключитесь к базе данных от имени sys_temp.

1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.8. Восстановите дамп в базу данных.

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных.
![1-4](https://github.com/kovbasaad/12-2-homework/blob/main/img/photo1674996577.jpeg)

```sql
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'cbcntvg-gfcc';
SELECT user FROM mysql.user;
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';
SHOW GRANTS FOR 'sys_temp'@'localhost';
```


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. 
![2-1](https://github.com/kovbasaad/12-2-homework/blob/main/img/2-1.JPG)
