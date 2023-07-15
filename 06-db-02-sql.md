# Домашнее задание к занятию 2. «SQL» - Соколов Александер

## Введение

Перед выполнением задания вы можете ознакомиться с 
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/blob/virt-11/additional/README.md).

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.



Приведите получившуюся команду или docker-compose-манифест.

'Ответ':

docker run -e POSTGRES_PASSWORD=postgres -e PGDATA=/var/lib/postgresql/data -p 5432:5432 -v /tmp/postgres/data:/var/lib/postgresql/data -v /tmp/postgres/backups:/var/lib/postgresql/backups -d postgres

## Задача 2

В БД из задачи 1: 

- создайте пользователя test-admin-user и БД test_db;
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже);
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db;
- создайте пользователя test-simple-user;
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE этих таблиц БД test_db.

Таблица orders:

- id (serial primary key);
- наименование (string);
- цена (integer).

Таблица clients:

- id (serial primary key);
- фамилия (string);
- страна проживания (string, index);
- заказ (foreign key orders).

Приведите:

- итоговый список БД после выполнения пунктов выше;
- описание таблиц (describe);
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db;
- список пользователей с правами над таблицами test_db.

'Ответ':

test_db=# \l
                                <br> List of databases

| Name      | Owner    | Encoding | Collate    | Ctype      | Access privileges                                                     |
|-----------|----------|----------|------------|------------|-----------------------------------------------------------------------|
| postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |                                                                       |
| template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres + postgres=CTc/postgres                                   |
| template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres + postgres=CTc/postgres                                   |
| test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres + postgres=CTc/postgres + "test-admin-user"=CTc/postgres |
(4 rows)

<br>
test_db-# \d+ orders<br>
Table "public.orders"<br>

| Column       | Type    | Collation | Nullable | Default                            | Storage  | Stats target | Description |
|--------------|---------|-----------|----------|------------------------------------|----------|--------------|-------------|
| id           | integer |           | not null | nextval('orders_id_seq'::regclass) | plain    |              |             |
| наименование | text    |           |          |                                    | extended |              |             |
| цена         | numeric |           |          |                                    | main     |              |             |
<p>Indexes:
    "orders_pkey" PRIMARY KEY, btree (id)
<p>Referenced by:
    TABLE "clients" CONSTRAINT "clients_заказ_fkey" FOREIGN KEY ("заказ") REFERENCES orders(id)
<p>Access method: heap

<br>
<br>
<br>
test_db-# \d+ clients
<p> Table "public.clients"

| Column            | Type    | Collation | Nullable | Default                            | Storage  | Stats target | Description |
|-------------------|---------|-----------|----------|------------------------------------|----------|--------------|-------------|
| id                | integer |           | not null | nextval('orders_id_seq'::regclass) | plain    |              |             |
| фамилия           | text    |           |          |                                    | extended |              |             |
| страна проживания | заказ   |           |          |                                    | extended |              |             |
| заказ             | заказ   |           |          |                                    | extended |              |             |

<p>Indexes:
    "clients_pkey" PRIMARY KEY, btree (id)
    "clients_страна проживания_idx" btree ("страна проживания")
<p>Foreign-key constraints:
    "clients_заказ_fkey" FOREIGN KEY ("заказ") REFERENCES orders(id)
<p>Access method: heap

<br>
<br>
<br>
SELECT grantee,table_catalog, table_schema, table_name, privilege_type
FROM   information_schema.table_privileges 
WHERE  grantee not in ('postgres','PUBLIC');

  |      grantee     | table_name | privilege_type |
|:----------------:|:----------:|:--------------:|
| test-admin-user  | orders     | INSERT         |
| test-admin-user  | orders     | SELECT         |
| test-admin-user  | orders     | UPDATE         |
| test-admin-user  | orders     | DELETE         |
| test-admin-user  | orders     | TRUNCATE       |
| test-admin-user  | orders     | REFERENCES     |
| test-admin-user  | orders     | TRIGGER        |
| test-admin-user  | clients    | INSERT         |
| test-admin-user  | clients    | SELECT         |
| test-admin-user  | clients    | UPDATE         |
| test-admin-user  | clients    | DELETE         |
| test-admin-user  | clients    | TRUNCATE       |
| test-admin-user  | clients    | REFERENCES     |
| test-admin-user  | clients    | TRIGGER        |
| test-simple-user | orders     | INSERT         |
| test-simple-user | orders     | SELECT         |
| test-simple-user | orders     | UPDATE         |
| test-simple-user | orders     | DELETE         |
| test-simple-user | clients    | INSERT         |
| test-simple-user | clients    | SELECT         |
| test-simple-user | clients    | UPDATE         |
| test-simple-user | clients    | DELETE         |

## Задача 3

Используя SQL-синтаксис, наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

Используя SQL-синтаксис:
- вычислите количество записей для каждой таблицы.

'Ответ':

INSERT INTO orders (наименование, цена) VALUES ('Шоколад',10),('Принтер',3000),('Книга',500),('Монитор',7000),('Гитара',4000);
INSERT INTO clients ("фамилия", "страна проживания") VALUES ('Иванов Иван Иванович','USA'),('Петров Петр Петрович','Canada'),('Иоганн Себастьян Бах','Japan'),('Ронни Джеймс Дио','Russia'),('Ritchie Blackmore','Russia');

select count(*) from orders;
 count
---
     5
(1 row)
<br>
<br>
select count(*) from clients;
 count
---
     5
(1 row)


## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys, свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения этих операций.

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод этого запроса.
 
Подсказка: используйте директиву `UPDATE`.

'Ответ':

update clients
set заказ = orders.наименование
from orders
where clients.id = 1
and orders.id = 3;

update clients
set заказ = orders.наименование
from orders
where clients.id = 2
and orders.id = 4;

update clients
set заказ = orders.наименование
from orders
where clients.id = 3
and orders.id = 5;
<br><br><br>
test_db=# select фамилия from clients where "заказ" is not null;
       
| фамилия              |
|----------------------|
| Иванов Иван Иванович |
| Петров Петр Петрович |
| Иоганн Себастьян Бах |
| (3 rows)             |

## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните, что значат полученные значения.

'Ответ':

<p>test_db=# explain select фамилия from clients where "заказ" is not null;
                        <p>QUERY PLAN<p>
-----------------------------------------------------------
 <p>Seq Scan on clients  (cost=0.00..16.30 rows=627 width=32)
   Filter: ("заказ" IS NOT NULL)
(2 rows)
<p>видим что идёт последовательное сканирование таблицы клиент с применением фильтра "заказ" IS NOT NULL

## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. задачу 1).

Остановите контейнер с PostgreSQL, но не удаляйте volumes.

Поднимите новый пустой контейнер с PostgreSQL.

Восстановите БД test_db в новом контейнере.

Приведите список операций, который вы применяли для бэкапа данных и восстановления. 

'Ответ':

pg_dump -U postgres test_db > /var/lib/postgresql/backups/test_db.sql
<p>psql -U postgres test_db < /var/lib/postgresql/backups/test_db.sql

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

