# Домашнее задание к занятию "6.4. PostgreSQL"

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

## Задача 2

Используя `psql` создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders`
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления и полученный результат.

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам, как успешному выпускнику курсов DevOps в нетологии предложили
провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).

Предложите SQL-транзакцию для проведения данной операции.

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?

## Задача 4

Используя утилиту `pg_dump` создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

---

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






---
