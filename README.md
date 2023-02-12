# Домашнее задание к занятию 12.2 "Работа с данными (DDL/DML)" - "Червяков Антон"

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

![Скриншот-1](https://github.com/BadaBo0m/sdb-homework-12-02/blob/main/images/1.png)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

![Скриншот-2](https://github.com/BadaBo0m/sdb-homework-12-02/blob/main/images/2.png)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

![Скриншот-3](https://github.com/BadaBo0m/sdb-homework-12-02/blob/main/images/3.png)

```
mysql -u root -p
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';
CREATE DATABASE sakila DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
GRANT ALL PRIVILEGES ON sakila.* TO 'sys_temp'@'localhost';
FLUSH PRIVILEGES;

wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
cd ./sakila-db/
mysql -usys_temp -p sakila < ./sakila-schema.sql
mysql -usys_temp -p sakila < ./sakila-data.sql

mysql -u sys_temp -p
USE sakila;
SHOW TABLES;
```

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```
```sql
select s.TABLE_NAME tname, s.INDEX_NAME, s.COLUMN_NAME from information_schema.STATISTICS s where s.TABLE_SCHEMA ='sakila' AND s.INDEX_NAME='PRIMARY';
```
![Скриншот-4](https://github.com/BadaBo0m/sdb-homework-12-02/blob/main/images/4.png)


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 3*
3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*
