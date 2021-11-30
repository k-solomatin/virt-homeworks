# Домашнее задание к занятию "6.3. MySQL"

## Введение

Перед выполнением задания вы можете ознакомиться с
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/tree/master/additional/README.md).

## Задача 1

Используя docker поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-03-mysql/test_data) и
восстановитесь из него.

Перейдите в управляющую консоль `mysql` внутри контейнера.

Используя команду `\h` получите список управляющих команд.

Найдите команду для выдачи статуса БД и **приведите в ответе** из ее вывода версию сервера БД.

Подключитесь к восстановленной БД и получите список таблиц из этой БД.

**Приведите в ответе** количество записей с `price` > 300.

В следующих заданиях мы будем продолжать работу с данным контейнером.

## Задача 2

Создайте пользователя test в БД c паролем test-pass, используя:
- плагин авторизации mysql_native_password
- срок истечения пароля - 180 дней
- количество попыток авторизации - 3
- максимальное количество запросов в час - 100
- аттрибуты пользователя:
    - Фамилия "Pretty"
    - Имя "James"

Предоставьте привелегии пользователю `test` на операции SELECT базы `test_db`.

Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES получите данные по пользователю `test` и
**приведите в ответе к задаче**.

## Задача 3

Установите профилирование `SET profiling = 1`.
Изучите вывод профилирования команд `SHOW PROFILES;`.

Исследуйте, какой `engine` используется в таблице БД `test_db` и **приведите в ответе**.

Измените `engine` и **приведите время выполнения и запрос на изменения из профайлера в ответе**:
- на `MyISAM`
- на `InnoDB`

## Задача 4

Изучите файл `my.cnf` в директории /etc/mysql.

Измените его согласно ТЗ (движок InnoDB):
- Скорость IO важнее сохранности данных
- Нужна компрессия таблиц для экономии места на диске
- Размер буффера с незакомиченными транзакциями 1 Мб
- Буффер кеширования 30% от ОЗУ
- Размер файла логов операций 100 Мб

Приведите в ответе измененный файл `my.cnf`.

---

### Решение
## Задача 1

docker pull mysql:8.0  
docker volume create vol_mysql  
docker run --rm --name mysql-docker -e MYSQL_ROOT_PASSWORD=mysql -ti -p 3306:3306 -v vol_mysql:/etc/mysql/ mysql:8.0  
![Obraz](1.png)  
use temp_db;  
show tables;  
select count(*) from orders where price >300;  
## Задача 2  
mysql> CREATE USER 'test'@'localhost' IDENTIFIED BY 'test-pass';  
Query OK, 0 rows affected (0.02 sec)  

mysql> ALTER USER 'test'@'localhost' ATTRIBUTE '{"fname":"James", "lname":"Pretty"}';  
Query OK, 0 rows affected (0.00 sec)  

mysql> ALTER USER 'test'@'localhost'  
    -> IDENTIFIED BY 'test-pass'  
    -> WITH  
    -> MAX_QUERIES_PER_HOUR 100  
    -> PASSWORD EXPIRE INTERVAL 180 DAY  
    -> FAILED_LOGIN_ATTEMPTS 3 PASSWORD_LOCK_TIME 2;  
Query OK, 0 rows affected (0.00 sec)  

mysql> GRANT SELECT ON temp_db.orders TO 'test'@'localhost';  
Query OK, 0 rows affected, 1 warning (0.00 sec)  

mysql> SELECT * FROM INFORMATION_SCHEMA.USER_ATTRIBUTES WHERE USER='test';  
+------+-----------+---------------------------------------+  
| USER | HOST      | ATTRIBUTE                             |  
+------+-----------+---------------------------------------+  
| test | localhost | {"fname": "James", "lname": "Pretty"} |  
+------+-----------+---------------------------------------+  
1 row in set (0.00 sec)  

---
