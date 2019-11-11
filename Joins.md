
## What is Joins In DB :
Joins used to combine data or rows from two or more tables based on a common field between them.

## Types of JOIN :
1. inner join
2. Left outer join
3. Right outer join 
4. Full outer join
5. Cross join

1. Inner Join : Returns records that have matching values in both tables.It is also referred to as an EQUIJOIN.
  
  Syntax:
  SELECT table1.column1, table2.column2...<br />
  FROM table1<br />
  INNER JOIN table2<br />
  ON table1.common_field = table2.common_field;<br />
  
  For example: Suppose there is a Customer Table and an Order Tabel. We have to find the customer with their order details.

| ID | NAME     | AGE | ADDRESS   | SALARY   |
|----|----------|-----|-----------|----------|
|  1 | Ramesh   |  32 | Ahmedabad |  2000.00 |
|  2 | Khilan   |  25 | Delhi     |  1500.00 |
|  3 | kaushik  |  23 | Kota      |  2000.00 |
|  4 | Chaitali |  25 | Mumbai    |  6500.00 |
|  5 | Hardik   |  27 | Bhopal    |  8500.00 |
|  6 | Komal    |  22 | MP        |  4500.00 |
|  7 | Muffy    |  24 | Indore    | 10000.00 |


| OID | DATE                | CUSTOMER_ID | AMOUNT |
|-----|---------------------|-------------|--------|
| 102 | 2009-10-08 00:00:00 |           3 |   3000 |
| 100 | 2009-10-08 00:00:00 |           3 |   1500 |
| 101 | 2009-11-20 00:00:00 |           2 |   1560 |
| 103 | 2008-05-20 00:00:00 |           4 |   2060 |

We can write the inner join query for above query,
   SELECT  ID, NAME, AMOUNT, DATE<br />
   FROM CUSTOMERS<br />
   INNER JOIN ORDERS<br />
   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;<br />
   
Result is, <br />

| ID | NAME     | AMOUNT | DATE                |
|----|----------|--------|---------------------|
|  3 | kaushik  |   3000 | 2009-10-08 00:00:00 |
|  3 | kaushik  |   1500 | 2009-10-08 00:00:00 |
|  2 | Khilan   |   1560 | 2009-11-20 00:00:00 |
|  4 | Chaitali |   2060 | 2008-05-20 00:00:00 |


2. Left outer join : Returns all records from the left table, and the matched records from the right table.

  Syntax:
  SELECT table1.column1, table2.column2...<br />
  FROM table1<br />
  LEFT JOIN table2<br />
  ON table1.common_field = table2.common_field;<br />
  
  For example: Consider same Customer Table and an Order Tabel and same query i.e find the customer with their order details..
  We can write the left join query for above query,<br />
   
   SELECT  ID, NAME, AMOUNT, DATE<br />
   FROM CUSTOMERS<br />
   LEFT JOIN ORDERS<br />
   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;<br />
   
  Result is,<br />

| ID | NAME     | AMOUNT | DATE                |
|----|----------|--------|---------------------|
|  1 | Ramesh   |   NULL | NULL                |
|  2 | Khilan   |   1560 | 2009-11-20 00:00:00 |
|  3 | kaushik  |   3000 | 2009-10-08 00:00:00 |
|  3 | kaushik  |   1500 | 2009-10-08 00:00:00 |
|  4 | Chaitali |   2060 | 2008-05-20 00:00:00 |
|  5 | Hardik   |   NULL | NULL                |
|  6 | Komal    |   NULL | NULL                |
|  7 | Muffy    |   NULL | NULL                |



3. Right outer join : Returns all records from the right table, and the matched records from the left table.

  Syntax: 
  SELECT table1.column1, table2.column2...<br />
  FROM table1<br />
  RIGHT JOIN table2<br />
  ON table1.common_field = table2.common_field;<br />
  
  For example: Consider same Customer Table and an Order Tabel and same query i.e find the customer with their                  order details..<br />
 We can write the right join query for above query,<br /><br />
   SELECT  ID, NAME, AMOUNT, DATE<br />
   FROM CUSTOMERS<br />
   RIGHT JOIN ORDERS<br />
   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;<br />
   
Result is, 

| ID   | NAME     | AMOUNT | DATE                |
|------|----------|--------|---------------------|
|    3 | kaushik  |   3000 | 2009-10-08 00:00:00 |
|    3 | kaushik  |   1500 | 2009-10-08 00:00:00 |
|    2 | Khilan   |   1560 | 2009-11-20 00:00:00 |
|    4 | Chaitali |   2060 | 2008-05-20 00:00:00 |

  

4. Full outer join : Returns all records when there is a match in either left or right table.
  
  Syntax: 
  SELECT table1.column1, table2.column2...<br />
  FROM table1<br />
  FULL JOIN table2<br />
  ON table1.common_field = table2.common_field;<br />
  
  For example: Consider same Customer Table and an Order Tabel and same query i.e find the customer with their                  order details..
 We can write the full join query for above query,<br />
  
   SELECT  ID, NAME, AMOUNT, DATE<br />
   FROM CUSTOMERS<br />
   FULL JOIN ORDERS<br />
   ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;<br />

| ID   | NAME     | AMOUNT | DATE                |
|------|----------|--------|---------------------|
|    1 | Ramesh   |   NULL | NULL                |
|    2 | Khilan   |   1560 | 2009-11-20 00:00:00 |
|    3 | kaushik  |   3000 | 2009-10-08 00:00:00 |
|    3 | kaushik  |   1500 | 2009-10-08 00:00:00 |
|    4 | Chaitali |   2060 | 2008-05-20 00:00:00 |
|    5 | Hardik   |   NULL | NULL                |
|    6 | Komal    |   NULL | NULL                |
|    7 | Muffy    |   NULL | NULL                |
|    3 | kaushik  |   3000 | 2009-10-08 00:00:00 |
|    3 | kaushik  |   1500 | 2009-10-08 00:00:00 |
|    2 | Khilan   |   1560 | 2009-11-20 00:00:00 |
|    4 | Chaitali |   2060 | 2008-05-20 00:00:00 |



5. Cross join : The SQL CROSS JOIN produces a result set which is the number of rows in the first table multiplied by            the number of rows in the second table if no WHERE clause is used along with CROSS JOIN.This kind of result is called          as Cartesian Product.

  Syntax: 
  SELECT table1.column1, table2.column2...<br />
  FROM  table1, table2 [, table3 ]<br />
  
  For example: Consider same Customer Table and an Order Tabel and same query i.e find the customer with their                  order details..
 We can write the cross join query for above query,<br />
 
   SELECT  ID, NAME, AMOUNT, DATE<br />
   FROM CUSTOMERS, ORDERS;<br />
   
 Result is,
 
| ID | NAME     | AMOUNT | DATE                |
|----|----------|--------|---------------------|
|  1 | Ramesh   |   3000 | 2009-10-08 00:00:00 |
|  1 | Ramesh   |   1500 | 2009-10-08 00:00:00 |
|  1 | Ramesh   |   1560 | 2009-11-20 00:00:00 |
|  1 | Ramesh   |   2060 | 2008-05-20 00:00:00 |
|  2 | Khilan   |   3000 | 2009-10-08 00:00:00 |
|  2 | Khilan   |   1500 | 2009-10-08 00:00:00 |
|  2 | Khilan   |   1560 | 2009-11-20 00:00:00 |
|  2 | Khilan   |   2060 | 2008-05-20 00:00:00 |
|  3 | kaushik  |   3000 | 2009-10-08 00:00:00 |
|  3 | kaushik  |   1500 | 2009-10-08 00:00:00 |
|  3 | kaushik  |   1560 | 2009-11-20 00:00:00 |
|  3 | kaushik  |   2060 | 2008-05-20 00:00:00 |
|  4 | Chaitali |   3000 | 2009-10-08 00:00:00 |
|  4 | Chaitali |   1500 | 2009-10-08 00:00:00 |
|  4 | Chaitali |   1560 | 2009-11-20 00:00:00 |
|  4 | Chaitali |   2060 | 2008-05-20 00:00:00 |
|  5 | Hardik   |   3000 | 2009-10-08 00:00:00 |
|  5 | Hardik   |   1500 | 2009-10-08 00:00:00 |
|  5 | Hardik   |   1560 | 2009-11-20 00:00:00 |
|  5 | Hardik   |   2060 | 2008-05-20 00:00:00 |
|  6 | Komal    |   3000 | 2009-10-08 00:00:00 |
|  6 | Komal    |   1500 | 2009-10-08 00:00:00 |
|  6 | Komal    |   1560 | 2009-11-20 00:00:00 |
|  6 | Komal    |   2060 | 2008-05-20 00:00:00 |
|  7 | Muffy    |   3000 | 2009-10-08 00:00:00 |
|  7 | Muffy    |   1500 | 2009-10-08 00:00:00 |
|  7 | Muffy    |   1560 | 2009-11-20 00:00:00 |
|  7 | Muffy    |   2060 | 2008-05-20 00:00:00 |

6. Self Join : used to join a table to itself as if the table were two tables

  Syntax:
  SELECT a.column_name, b.column_name...<br />
  FROM table1 a, table1 b<br />
  WHERE a.common_field = b.common_field;<br />
  
  
  
  

  
