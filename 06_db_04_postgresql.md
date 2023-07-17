# Домашнее задание к занятию "6.4. PostgreSQL" - Соколов Александер

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

Подключитесь к БД PostgreSQL используя `psql`.

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:
- вывода списка БД
- подключения к БД
- вывода списка таблиц
- вывода описания содержимого таблиц
- выхода из psql


`Ответ:`

- `подготовим необходимые директории и файл docker-compose`
```
vagrant@vagrant:~/docker-compose-yam-postgre$ mkdir /home/vagrant/postgresql-db
vagrant@vagrant:~/docker-compose-yam-postgre$ mkdir /home/vagrant/postgresql-db/backup
vagrant@vagrant:~/docker-compose-yam-postgre$ mkdir /home/vagrant/postgresql-db/data

- vagrant@vagrant:~/docker-compose-yam-postgre$ nano docker-compose.yml
vagrant@vagrant:~/docker-compose-yam-postgre$ cat docker-compose.yml
version: '2.1'
services:
  db2:
    image: postgres:13
    environment:
      POSTGRES_PASSWORD: example
    volumes:
      - /home/vagrant/postgresql-db/data:/var/db-data
      - /home/vagrant/postgresql-db/backup:/var/db-backup
```
- `создадим сервис и запустим его:`
```
vagrant@vagrant:~/docker-compose-yam-postgre$ sudo docker compose build
vagrant@vagrant:~/docker-compose-yam-postgre$ sudo docker compose create
[+] Running 14/14
 ⠿ db3 Pulled                                                                                                                                                                                              24.2s
   ⠿ 31b3f1ad4ce1 Pull complete                                                                                                                                                                            10.2s
   ⠿ dc97844d0cd5 Pull complete                                                                                                                                                                            11.3s
   ⠿ 9ad9b1166fde Pull complete                                                                                                                                                                            11.4s
   ⠿ 286c4682b24d Pull complete                                                                                                                                                                            11.5s
   ⠿ 1d3679a4a1a1 Pull complete                                                                                                                                                                            12.1s
   ⠿ 5f2e6cdc8503 Pull complete                                                                                                                                                                            12.3s
   ⠿ 0f7dc70f54e8 Pull complete                                                                                                                                                                            12.4s
   ⠿ a090c7442692 Pull complete                                                                                                                                                                            12.4s
   ⠿ 20161a5651fc Pull complete                                                                                                                                                                            20.7s
   ⠿ bda56b4caa52 Pull complete                                                                                                                                                                            20.7s
   ⠿ 3d510a204ab2 Pull complete                                                                                                                                                                            20.8s
   ⠿ b6ee599a1b2e Pull complete                                                                                                                                                                            20.9s
   ⠿ 6b8197a3d2b1 Pull complete                                                                                                                                                                            21.0s
[+] Running 2/2
 ⠿ Network docker-compose-yam-postgre_default  Created                                                                                                                                                      0.1s
 ⠿ Container docker-compose-yam-postgre-db3-1  Created                                                                                                                                                      1.4s
vagrant@vagrant:~/docker-compose-yam-postgre$ sudo docker compose up
[+] Running 1/1
 ⠿ Container docker-compose-yam-postgre-db3-1  Recreated                                                                                                                                                    0.1s
Attaching to docker-compose-yam-postgre-db3-1
docker-compose-yam-postgre-db3-1  | The files belonging to this database system will be owned by user "postgres".
docker-compose-yam-postgre-db3-1  | This user must also own the server process.
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | The database cluster will be initialized with locale "en_US.utf8".
docker-compose-yam-postgre-db3-1  | The default database encoding has accordingly been set to "UTF8".
docker-compose-yam-postgre-db3-1  | The default text search configuration will be set to "english".
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | Data page checksums are disabled.
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | fixing permissions on existing directory /var/lib/postgresql/data ... ok
docker-compose-yam-postgre-db3-1  | creating subdirectories ... ok
docker-compose-yam-postgre-db3-1  | selecting dynamic shared memory implementation ... posix
docker-compose-yam-postgre-db3-1  | selecting default max_connections ... 100
docker-compose-yam-postgre-db3-1  | selecting default shared_buffers ... 128MB
docker-compose-yam-postgre-db3-1  | selecting default time zone ... Etc/UTC
docker-compose-yam-postgre-db3-1  | creating configuration files ... ok
docker-compose-yam-postgre-db3-1  | running bootstrap script ... ok
docker-compose-yam-postgre-db3-1  | performing post-bootstrap initialization ... ok
docker-compose-yam-postgre-db3-1  | syncing data to disk ... initdb: warning: enabling "trust" authentication for local connections
docker-compose-yam-postgre-db3-1  | You can change this by editing pg_hba.conf or using the option -A, or
docker-compose-yam-postgre-db3-1  | --auth-local and --auth-host, the next time you run initdb.
docker-compose-yam-postgre-db3-1  | ok
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | Success. You can now start the database server using:
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  |     pg_ctl -D /var/lib/postgresql/data -l logfile start
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | waiting for server to start....2022-09-11 03:09:35.605 UTC [47] LOG:  starting PostgreSQL 13.8 (Debian 13.8-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.608 UTC [47] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.614 UTC [48] LOG:  database system was shut down at 2022-09-11 03:09:35 UTC
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.620 UTC [47] LOG:  database system is ready to accept connections
docker-compose-yam-postgre-db3-1  |  done
docker-compose-yam-postgre-db3-1  | server started
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | waiting for server to shut down....2022-09-11 03:09:35.723 UTC [47] LOG:  received fast shutdown request
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.731 UTC [47] LOG:  aborting any active transactions
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.733 UTC [47] LOG:  background worker "logical replication launcher" (PID 54) exited with exit code 1
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.733 UTC [49] LOG:  shutting down
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.749 UTC [47] LOG:  database system is shut down
docker-compose-yam-postgre-db3-1  |  done
docker-compose-yam-postgre-db3-1  | server stopped
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | PostgreSQL init process complete; ready for start up.
docker-compose-yam-postgre-db3-1  |
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.850 UTC [1] LOG:  starting PostgreSQL 13.8 (Debian 13.8-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.850 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.850 UTC [1] LOG:  listening on IPv6 address "::", port 5432
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.870 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.875 UTC [59] LOG:  database system was shut down at 2022-09-11 03:09:35 UTC
docker-compose-yam-postgre-db3-1  | 2022-09-11 03:09:35.882 UTC [1] LOG:  database system is ready to accept connections

vagrant@vagrant:~/docker-compose-yam-postgre$ sudo docker compose ps
NAME                               COMMAND                  SERVICE             STATUS              PORTS
docker-compose-yam-postgre-db3-1   "docker-entrypoint.s…"   db3                 running             5432/tcp
```

- `подключимся к контейнеру и psql`
```
vagrant@vagrant:~/docker-compose-yam-postgre$ sudo docker exec -it docker-compose-yam-postgre-db3-1 bash
root@sokolov:/var# su - postgres
postgres@sokolov:~$ psql
psql (13.8 (Debian 13.8-1.pgdg110+1))
Type "help" for help.

LINE 1: /?
        ^
postgres=# \?
General
  \copyright             show PostgreSQL usage and distribution terms
  \crosstabview [COLUMNS] execute query and display results in crosstab
  \errverbose            show most recent error message at maximum verbosity
  \g [(OPTIONS)] [FILE]  execute query (and send results to file or |pipe);
                         \g with no arguments is equivalent to a semicolon
  \gdesc                 describe result of query, without executing it
  \gexec                 execute query, then execute each value in its result
  \gset [PREFIX]         execute query and store results in psql variables
  \gx [(OPTIONS)] [FILE] as \g, but forces expanded output mode
  \q                     quit psql
  \watch [SEC]           execute query every SEC seconds
```
- `вывода списка БД`
```
postgres=# \l+ *
                                                                   List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   |  Size   | Tablespace |                Description
-----------+----------+----------+------------+------------+-----------------------+---------+------------+--------------------------------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |                       | 7901 kB | pg_default | default administrative connection database
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +| 7753 kB | pg_default | unmodifiable empty database
           |          |          |            |            | postgres=CTc/postgres |         |            |
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +| 7753 kB | pg_default | default template for new databases
           |          |          |            |            | postgres=CTc/postgres |         |            |
(3 rows)
```

- `подключения к БД`
```
postgres=# \connect postgres;
You are now connected to database "postgres" as user "postgres".
```
- `вывода списка таблиц`
```
postgres=#  \dtS+
                                        List of relations
   Schema   |          Name           | Type  |  Owner   | Persistence |    Size    | Description
------------+-------------------------+-------+----------+-------------+------------+-------------
 pg_catalog | pg_aggregate            | table | postgres | permanent   | 56 kB      |
 pg_catalog | pg_am                   | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_amop                 | table | postgres | permanent   | 80 kB      |
 pg_catalog | pg_amproc               | table | postgres | permanent   | 64 kB      |
 pg_catalog | pg_attrdef              | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_attribute            | table | postgres | permanent   | 456 kB     |
 pg_catalog | pg_auth_members         | table | postgres | permanent   | 40 kB      |
 pg_catalog | pg_authid               | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_cast                 | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_class                | table | postgres | permanent   | 136 kB     |
 pg_catalog | pg_collation            | table | postgres | permanent   | 240 kB     |
 pg_catalog | pg_constraint           | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_conversion           | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_database             | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_db_role_setting      | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_default_acl          | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_depend               | table | postgres | permanent   | 488 kB     |
 pg_catalog | pg_description          | table | postgres | permanent   | 376 kB     |
 pg_catalog | pg_enum                 | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_event_trigger        | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_extension            | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_foreign_data_wrapper | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_foreign_server       | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_foreign_table        | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_index                | table | postgres | permanent   | 64 kB      |
 pg_catalog | pg_inherits             | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_init_privs           | table | postgres | permanent   | 56 kB      |
 pg_catalog | pg_language             | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_largeobject          | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_largeobject_metadata | table | postgres | permanent   | 0 bytes    |
 pg_catalog | pg_namespace            | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_opclass              | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_operator             | table | postgres | permanent   | 144 kB     |
 pg_catalog | pg_opfamily             | table | postgres | permanent   | 48 kB      |
 pg_catalog | pg_partitioned_table    | table | postgres | permanent   | 8192 bytes |
 pg_catalog | pg_policy               | table | postgres | permanent   | 8192 bytes |
```
- `вывода описания содержимого таблиц`
```
- postgres=# \dS+ pg_user_mapping
                             Table "pg_catalog.pg_user_mapping"
  Column   |  Type  | Collation | Nullable | Default | Storage  | Stats target | Description
-----------+--------+-----------+----------+---------+----------+--------------+-------------
 oid       | oid    |           | not null |         | plain    |              |
 umuser    | oid    |           | not null |         | plain    |              |
 umserver  | oid    |           | not null |         | plain    |              |
 umoptions | text[] | C         |          |         | extended |              |
Indexes:
    "pg_user_mapping_oid_index" UNIQUE, btree (oid)
    "pg_user_mapping_user_server_index" UNIQUE, btree (umuser, umserver)
Access method: heap
```
- `выход из psql`
```
postgres=# exit
postgres@sokolov:~$
```

## Задача 2

Используя `psql` создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления и полученный результат.

`Ответ:` 

- `присвоим права на папки для tablespace и папка для backup для пользователя postgres`
```
root@sokolov:/var# chown postgres:postgres /var/db-data/
root@sokolov:/var# chown postgres:postgres /var/db-backup/
root@sokolov:/var# ls -al
total 60
drwxr-xr-x 1 root     root     4096 Sep 11 03:09 .
drwxr-xr-x 1 root     root     4096 Sep 11 03:09 ..
drwxr-xr-x 2 root     root     4096 Sep  3 12:10 backups
drwxr-xr-x 1 root     root     4096 Sep 13  2022 cache
drwxrwxr-x 2 postgres postgres 4096 Sep 11 03:02 db-backup
drwxrwxr-x 2 postgres postgres 4096 Sep 11 03:05 db-data
drwxr-xr-x 1 root     root     4096 Sep 13  2022 lib
drwxrwsr-x 2 root     staff    4096 Sep  3 12:10 local
lrwxrwxrwx 1 root     root        9 Sep 12  2022 lock -> /run/lock
drwxr-xr-x 1 root     root     4096 Sep 13  2022 log
drwxrwsr-x 2 root     mail     4096 Sep 12  2022 mail
drwxr-xr-x 2 root     root     4096 Sep 12  2022 opt
lrwxrwxrwx 1 root     root        4 Sep 12  2022 run -> /run
drwxr-xr-x 2 root     root     4096 Sep 12  2022 spool
drwxrwxrwt 2 root     root     4096 Sep  3 12:10 tmp
```
- `скопируем бэкап БД в докер`
```
PS C:\Users\kapli> scp c:\Users\kapli\homeworks\06-db-04-postgresql\test_data\test_dump.sql vagrant@192.168.33.10:/home/vagrant/postgresql-db/
vagrant@192.168.33.10's password:
test_dump.sql
vagrant@vagrant:~/postgresql-db$ sudo cp test_dump.sql /backup
```
- `создадим бд`
```
postgres=# CREATE TABLESPACE "test-tablespace" OWNER CURRENT_USER
postgres-# LOCATION '/var/db-data';
CREATE TABLESPACE

postgres=# CREATE DATABASE "test_database" WITH TABLESPACE = "test-tablespace";
CREATE DATABASE
```
-- `загрузим backup`
```
postgres@sokolov:/var/db-backup$ psql --dbname=test_database --file=test_dump.sql
SET
SET
SET
SET
SET
 set_config
------------

(1 row)

SET
SET
SET
SET
SET
SET
CREATE TABLE
ALTER TABLE
CREATE SEQUENCE
ALTER TABLE
ALTER SEQUENCE
ALTER TABLE
COPY 8
 setval
--------
      8
(1 row)

ALTER TABLE
```
-- `проведем analyze`
```
postgres=# \connect test_database;
You are now connected to database "test_database" as user "postgres".
test_database=# analyze;
ANALYZE

test_database=# \dS+ orders;
                                                       Table "public.orders"
 Column |         Type          | Collation | Nullable |              Default               | Storage  | Stats target | Description
--------+-----------------------+-----------+----------+------------------------------------+----------+--------------+-------------
 id     | integer               |           | not null | nextval('orders_id_seq'::regclass) | plain    |              |
 title  | character varying(80) |           | not null |                                    | extended |              |
 price  | integer               |           |          | 0                                  | plain    |              |
Indexes:
    "orders_pkey" PRIMARY KEY, btree (id)
Access method: heap
```
- `использует select для выбора максимального значения:`
```
test_database=# select max(avg_width),attname from pg_stats where tablename ='orders' group by attname;
 max | attname
-----+---------
   4 | id
   4 | price
  16 | title
(3 rows)
```

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам, как успешному выпускнику курсов DevOps в нетологии предложили
провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).

Предложите SQL-транзакцию для проведения данной операции.

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?


`Ответ:`


- `можно выполнить следующий скрипт`
```
create table orders_500 as select * from orders where price>499;
delete from orders where price>499;
```
- `чтобы исключить ручное разбиение можно использовать использовать таблицу partion master table, сделаем две таблицы, объединенных одной общей и разделяемой по признаку price, например;`
```
test_database=# CREATE TABLE orders_master (
id  integer not null,
title varchar(80) not null,
price integer
)
PARTITION BY RANGE (PRICE);
CREATE TABLE

test_database=# create table orders_499 PARTITION OF orders_master FOR VALUES FROM (0) to (500);
CREATE TABLE
test_database=# create table orders_500 PARTITION OF orders_master FOR VALUES FROM (500) to (1000000);
CREATE TABLE

test_database=# insert into orders_500 select * from orders where price>499;
INSERT 0 3  
test_database=# select * from  orders_master;
 id |       title        | price
----+--------------------+-------
  2 | My little database |   500
  6 | WAL never lies     |   900
  8 | Dbiezdmin          |   501
(3 rows)

test_database=# insert into orders_499 select * from orders where price<500;
INSERT 0 5


test_database=# select * from  orders_master;
 id |        title         | price
----+----------------------+-------
  1 | War and peace        |   100
  3 | Adventure psql time  |   300
  4 | Server gravity falls |   300
  5 | Log gossips          |   123
  7 | Me and my bash-pet   |   499
  2 | My little database   |   500
  6 | WAL never lies       |   900
  8 | Dbiezdmin            |   501
(8 rows)
```
## Задача 4

Используя утилиту `pg_dump` создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

`Ответ:`

- `выгрузим dump`
```
postgres@sokolov:/var/db-backup$ pg_dump test_database > test_database.dmp
postgres@sokolov:/var/db-backup$ ls -al
total 20
drwxrwxr-x 2 postgres postgres 4096 Sep 11 16:04 .
drwxr-xr-x 1 root     root     4096 Sep 11 03:09 ..
-rw-r--r-- 1 postgres postgres 3714 Sep 11 16:04 test_database.dmp
-rw-rw-r-- 1     1000     1000 2181 Sep 11 03:54 test_dump.sql
postgres@sokolov:/var/db-backup$ cat test_database.dmp
--
-- PostgreSQL database dump
--

-- Dumped from database version 13.8 (Debian 13.8-1.pgdg110+1)
-- Dumped by pg_dump version 13.8 (Debian 13.8-1.pgdg110+1)

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

SET default_tablespace = '';

SET default_table_access_method = heap;

--
-- Name: orders; Type: TABLE; Schema: public; Owner: postgres
--

CREATE TABLE public.orders (
    id integer NOT NULL,
    title character varying(80) NOT NULL,
    price integer DEFAULT 0
```


- `Чтобы обеспечить уникальность добавить следующую директиву в файл backup:`

```
Alter table public.orders add UNIQUE ( title );
```
- `проверим:`
```
postgres=#  drop database test_database;
DROP DATABASE

postgres@sokolov:/var/db-backup$ psql --dbname=test_database --file=test_database.dmp
SET
SET
SET
SET
SET
 set_config
------------

(1 row)

SET
SET
SET
SET
SET
SET
CREATE TABLE
ALTER TABLE
CREATE TABLE
ALTER TABLE
CREATE TABLE
ALTER TABLE
ALTER TABLE
CREATE TABLE
ALTER TABLE
ALTER TABLE
CREATE SEQUENCE
ALTER TABLE
ALTER SEQUENCE
ALTER TABLE
COPY 8
COPY 5
COPY 3
 setval
--------
      8
(1 row)

ALTER TABLE
ALTER TABLE
```
- `проверим`
```
postgres=# \connect test_database;
You are now connected to database "test_database" as user "postgres".
test_database=# \dS+ orders
                                                       Table "public.orders"
 Column |         Type          | Collation | Nullable |              Default               | Storage  | Stats target | Description
--------+-----------------------+-----------+----------+------------------------------------+----------+--------------+-------------
 id     | integer               |           | not null | nextval('orders_id_seq'::regclass) | plain    |              |
 title  | character varying(80) |           | not null |                                    | extended |              |
 price  | integer               |           |          | 0                                  | plain    |              |
Indexes:
    "orders_pkey" PRIMARY KEY, btree (id)
    "orders_title_key" UNIQUE CONSTRAINT, btree (title)
Access method: heap
```
--- 


### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
