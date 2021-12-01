# Домашнее задание к занятию "6.4. PostgreSQL"



# Решение

## Задача 1  
```docker pull postgres:13```  
```docker volume create vol_postgres```  
```run --rm --name pg-docker -e POSTGRES_PASSWORD=postgres -ti -p 5432:5432 -v vol_postgres:/var/lib/postgresql/data postgres:13```  
```docker exec -it pg-docker bash```  
```psql -h localhost -p 5432 -U postgres -W```  
Список БД ```\l```  
Подключение к БД ```\c postgres```   
Вывод списка таблиц ```\dtS```  
Вывод описания содержимого таблиц ```\dS+ pg_index```  
Выход из psql ```\q```  

## Задача 2  
Создание БД ```CREATE DATABASE test_database;```  
Востановим бекап ```psql -U postgres -f ./pg_backup.sql test_database```  
Зайдем в БД   
postgres=# \c test_database  
Password:   
You are now connected to database "test_database" as user "postgres".  
test_database=# \dt  
         List of relations  
 Schema |  Name  | Type  |  Owner     
--------+--------+-------+----------  
 public | orders | table | postgres  
(1 row)  
Операция ANALYZE  
test_database=# ANALYZE VERBOSE public.orders;  
INFO:  analyzing "public.orders"  
INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows  
ANALYZE  

test_database=# select avg_width from pg_stats where tablename='orders';  
 avg_width   
-----------  
         4  
        16  
         4  
(3 rows)  

## Задача 3  

Для начала нужно преобразовать существующую таблицу в партиционированную, поэтому пересоздадим таблицу  
test_database=# alter table orders rename to orders_simple;  
ALTER TABLE  
test_database=# create table orders (id integer, title varchar(80), price integer) partition by range(price);  
CREATE TABLE  
test_database=# create table orders_less499 partition of orders for values from (0) to (499);  
CREATE TABLE  
test_database=# create table orders_more499 partition of orders for values from (499) to (999999999);  
CREATE TABLE  
test_database=# insert into orders (id, title, price) select * from orders_simple;  
INSERT 0 8  
test_database=#   
С самого начала, можно было сделать ее секционированной, тогда не пришлось бы переименовывать исходную таблицу и переносить данные в новую.

##Задача 4  

pg_dump -U postgres -d test_database >database_dump.sql  
Для уникальности можно добавить индекс или первичный ключ.  
    CREATE INDEX ON orders ((lower(title)));  
---  
