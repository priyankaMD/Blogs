
### Null Means:
Null (or NULL) is a special marker used in SQL to indicate that a data value does not exist in the database.
Relational database management systems (RDBMS) support a representation of "missing information and undefined information".


### Aggregate functions and Null

Count(*) vs Count(col_name)

mysql> select * from tab;
+------+
| str  |
+------+
| NULL |
| NULL |
| NULL |
+------+
3 rows in set (0.00 sec)

mysql> select count(*) from tab;
+----------+
| count(*) |
+----------+
|        3 |
+----------+
1 row in set (0.01 sec)

mysql> select count(str) from tab;
+------------+
| count(str) |
+------------+
|          0 |
+------------+
1 row in set (0.00 sec)


------------------------------------------------
Null values stored in the database

mysql> insert into employee values (1,"Meena","D",12000,200,"Pune");
Query OK, 1 row affected (0.01 sec)

mysql> insert into employee values (2,"Sid","I",24000,2000,"Mumbai");
Query OK, 1 row affected (0.00 sec)

mysql> insert into employee values (3,"Dip","R",14000,500,"Mumbai");
Query OK, 1 row affected (0.01 sec)

mysql> insert into employee values (4,"Jan","R",19000,null,"Mumbai"); // give explicite value in column list
Query OK, 1 row affected (0.00 sec)

mysql> insert into employee values (5,'John','O',40000,0,'Mumbai');
Query OK, 1 row affected (0.01 sec)

mysql> insert into employee(id,fname,lname,salary,address) values (6,'Sarah','P',8000,'Mumbai'); // just omit it from the column list
Query OK, 1 row affected (0.00 sec)




Operations on Null
mysql> select * from employee;
+----+-------+-------+--------+------------+---------+
| id | fname | lname | salary | commission | address |
+----+-------+-------+--------+------------+---------+
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
+----+-------+-------+--------+------------+---------+
6 rows in set (0.00 sec)

mysql> select id, salary, commission from employee;
+----+--------+------------+
| id | salary | commission |
+----+--------+------------+
|  1 |  12000 |        200 |
|  2 |  24000 |       2000 |
|  3 |  14000 |        500 |
|  4 |  19000 |       NULL |
|  5 |  40000 |          0 |
|  6 |   8000 |       NULL |
+----+--------+------------+
6 rows in set (0.00 sec)

mysql> select id, salary, commission, salary+commission eff_sal from employee;
+----+--------+------------+---------+
| id | salary | commission | eff_sal |
+----+--------+------------+---------+
|  1 |  12000 |        200 |   12200 |
|  2 |  24000 |       2000 |   26000 |
|  3 |  14000 |        500 |   14500 |
|  4 |  19000 |       NULL |    NULL |
|  5 |  40000 |          0 |   40000 |
|  6 |   8000 |       NULL |    NULL |
+----+--------+------------+---------+
6 rows in set (0.00 sec)









-- Null Values are not the same as 0. (IS NULL and IS NOT NULL)

mysql> select fname, commission  from employee where commission is null;
+-------+------------+
| fname | commission |
+-------+------------+
| Jan   |       NULL |
| Sarah |       NULL |
+-------+------------+
2 rows in set (0.00 sec)

mysql> select fname, commission  from employee where commission is not null;
+-------+------------+
| fname | commission |
+-------+------------+
| Meena |        200 |
| Sid   |       2000 |
| Dip   |        500 |
| John  |          0 |
+-------+------------+
4 rows in set (0.00 sec)

mysql> select 1 is null, 1 is not null;
+-----------+---------------+
| 1 is null | 1 is not null |
+-----------+---------------+
|         0 |             1 |
+-----------+---------------+
1 row in set (0.00 sec)



mysql> SELECT 1 = NULL, 1 <> NULL, 1 < NULL, 1 > NULL;
+----------+-----------+----------+----------+
| 1 = NULL | 1 <> NULL | 1 < NULL | 1 > NULL |
+----------+-----------+----------+----------+
|     NULL |      NULL |     NULL |     NULL |
+----------+-----------+----------+----------+
1 row in set (0.00 sec)

mysql> SELECT 1 = NULL, 1 != NULL, 1 < NULL, 1 > NULL;
+----------+-----------+----------+----------+
| 1 = NULL | 1 != NULL | 1 < NULL | 1 > NULL |
+----------+-----------+----------+----------+
|     NULL |      NULL |     NULL |     NULL |
+----------+-----------+----------+----------+
1 row in set (0.00 sec)

mysql> SELECT 1 = NULL, 1 != NULL, 1 < NULL, 1 > NULL;
+----------+-----------+----------+----------+
| 1 = NULL | 1 != NULL | 1 < NULL | 1 > NULL |
+----------+-----------+----------+----------+
|     NULL |      NULL |     NULL |     NULL |
+----------+-----------+----------+----------+
1 row in set (0.00 sec)

mysql> SELECT 0 IS NULL, 0 IS NOT NULL, '' IS NULL, '' IS NOT NULL;
+-----------+---------------+------------+----------------+
| 0 IS NULL | 0 IS NOT NULL | '' IS NULL | '' IS NOT NULL |
+-----------+---------------+------------+----------------+
|         0 |             1 |          0 |              1 |
+-----------+---------------+------------+----------------+
1 row in set (0.00 sec)


Null Functions
IFNULL(): It is a single row function that means it is executed on each row one by one.

Syntax:
IFNULL(expr1,expr2) : if expr1 is null then it returns expr2 else it returns expr1.

For example, Query to find effective salary of employees of all employees. 

mysql> select * from employee;
+----+-------+-------+--------+------------+---------+
| id | fname | lname | salary | commission | address |
+----+-------+-------+--------+------------+---------+
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
+----+-------+-------+--------+------------+---------+
6 rows in set (0.00 sec)




mysql> select fname, salary, salary + ifnull(commission,0) as eff_sal from employee;
+-------+--------+---------+
| fname | salary | eff_sal |
+-------+--------+---------+
| Meena |  12000 |   12200 |
| Sid   |  24000 |   26000 |
| Dip   |  14000 |   14500 |
| Jan   |  19000 |   19000 |
| John  |  40000 |   40000 |
| Sarah |   8000 |    8000 |
+-------+--------+---------+
6 rows in set (0.00 sec)

-- How would you know that the employee gets only a salary or salary plus commission?

mysql> select fname, salary, salary + ifnull(commission,0) , if(commission is null,'sal','sal+commi') as eff_sal from employee;
+-------+--------+-------------------------------+-----------+
| fname | salary | salary + ifnull(commission,0) | eff_sal   |
+-------+--------+-------------------------------+-----------+
| Meena |  12000 |                         12200 | sal+commi |
| Sid   |  24000 |                         26000 | sal+commi |
| Dip   |  14000 |                         14500 | sal+commi |
| Jan   |  19000 |                         19000 | sal       |
| John  |  40000 |                         40000 | sal+commi |
| Sarah |   8000 |                          8000 | sal       |
+-------+--------+-------------------------------+-----------+
6 rows in set (0.00 sec)









Coalesce(): 
Returns First not null expression in list

mysql> select coalesce(null,null,null,2);
+----------------------------+
| coalesce(null,null,null,2) |
+----------------------------+
|                          2 |
+----------------------------+
1 row in set (0.00 sec)

mysql> select coalesce(null,1,null,2);
+-------------------------+
| coalesce(null,1,null,2) |
+-------------------------+
|                       1 |
+-------------------------+
1 row in set (0.00 sec)

IF expression combined IS NULL and IS NOT NULL Statement 

mysql> select if (commission is not null, commission, 0) from employee;
+--------------------------------------------+
| if (commission is not null, commission, 0) |
+--------------------------------------------+
|                                        200 |
|                                       2000 |
|                                        500 |
|                                          0 |
|                                          0 |
|                                          0 |
|                                         70 |
+--------------------------------------------+
7 rows in set (0.00 sec)



Case expression combined IS NULL and IS NOT NULL Statement 

mysql> select 
    -> CASE
    -> when commission is not null then commission
    -> else 0
    -> end as result
    -> from employee;



+--------+
| result |
+--------+
|    200 |
|   2000 |
|    500 |
|      0 |
|      0 |
|      0 |
|     70 |
+--------+
7 rows in set (0.00 sec)

OrderBy with Null
If you use the order by clause to sort the result, MySQL considers NULL values are lower than other values, therefore, it presents the NULL values first.

mysql> select * from employee order by commission;
+----+-------+-------+--------+------------+---------+
| id | fname | lname | salary | commission | address |
+----+-------+-------+--------+------------+---------+
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  7 | SDC   | G     |  12000 |         70 | null    |
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
+----+-------+-------+--------+------------+---------+
7 rows in set (0.04 sec)

mysql> select * from employee order by commission desc;
+----+-------+-------+--------+------------+---------+
| id | fname | lname | salary | commission | address |
+----+-------+-------+--------+------------+---------+
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  7 | SDC   | G     |  12000 |         70 | null    |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
+----+-------+-------+--------+------------+---------+
7 rows in set (0.00 sec)


GroupBy with Null
In the group by null is a valid value,It consider the null values and group by on that.

mysql> select * from employee;
+----+-------+-------+--------+------------+---------+
| id | fname | lname | salary | commission | address |
+----+-------+-------+--------+------------+---------+
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
|  7 | SDC   | G     |  12000 |         70 | null    |
|  8 | hshg  | hsgh  |   1298 |        100 | NULL    |
+----+-------+-------+--------+------------+---------+
8 rows in set (0.00 sec)

mysql> select address,count(*) from employee group by address;
+---------+----------+
| address | count(*) |
+---------+----------+
| Pune    |        1 |
| Mumbai  |        5 |
| null    |        1 |
| NULL    |        1 |
+---------+----------+

Distinct with Null
If we are fetching unique data points from the database and it contains multiple Null values, the MySQL Distinct statement will only include a single Null value.

mysql> select distinct address from employee;
+---------+
| address |
+---------+
| Pune    |
| Mumbai  |
| null    |
| NULL    |
+---------+
4 rows in set (0.00 sec)
Unique constraint with Null
MySQL allows multiple NULLs in a column with a unique constraint.
This is not true for all databases. SQL Server 2005 and older, for example, only allows a single NULL value in a column that has a unique constraint.

mysql> create table demo1(x int null unique);
Query OK, 0 rows affected (0.04 sec)

mysql> desc demo1;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| x     | int(11) | YES  | UNI | NULL    |       |
+-------+---------+------+-----+---------+-------+
1 row in set (0.01 sec)

mysql> insert into demo1 values(1);
Query OK, 1 row affected (0.00 sec)

mysql> insert into demo1 values(2);
Query OK, 1 row affected (0.01 sec)

mysql> insert into demo1 values(null);
Query OK, 1 row affected (0.00 sec)

mysql> insert into demo1 values(null);
Query OK, 1 row affected (0.00 sec)

mysql> insert into demo1 values(null);
Query OK, 1 row affected (0.00 sec)

mysql> select * from demo1;
+------+
| x    |
+------+
| NULL |
| NULL |
| NULL |
|    1 |
|    2 |
+------+
5 rows in set (0.00 sec)


Unique indexes with Null
MySQL allows multiple NULLs with unique index column.

mysql> create table person(id int,name varchar(20),email varchar(20));
Query OK, 0 rows affected (0.04 sec)

mysql> create UNIQUE INDEX idx_name_mail on person(name,email);
Query OK, 0 rows affected (0.05 sec)

mysql> insert into person values(1,'ABC','wer@gmail.com');
Query OK, 1 row affected (0.00 sec)

mysql> insert into person values(1,'ABC','wer@gmail.com');
ERROR 1062 (23000): Duplicate entry 'ABC-wer@gmail.com' for key 'idx_name_mail'

mysql> insert into person values(1,'ABC',null);
Query OK, 1 row affected (0.00 sec)

mysql> insert into person values(1,'ABC',null);
Query OK, 1 row affected (0.01 sec)


mysql> select * from person;
+------+------+---------------+
| id   | name | email         |
+------+------+---------------+
|    1 | ABC  | wer@gmail.com |
|    1 | ABC  | NULL          |
|    1 | ABC  | NULL          |
+------+------+---------------+
6 rows in set (0.00 sec)


 
