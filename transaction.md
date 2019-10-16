### Transaction
  A transaction is a single logical unit of work which accesses and possibly modifies the contents of a database.
  
  Transactions access data using: <br>
    1. Read Operation <br>
    2. Write Operation <br><br>
  In order to maintain consistency in a database, before and after transaction, certain properties are followed. 
  These are called ACID properties. <br>
  1. Atomicity : (All or nothing rule) <br>
      Each transaction is considered as one unit and either runs to completion or is not executed at all. 
      It involves following two operations. <br>
        —Abort: If a transaction aborts, changes made to database are not visible. <br>
        —Commit: If a transaction commits, changes made are visible. <br>
  
   For Example:Consider the transaction T consisting of T1 and T2: Transfer of 100 from account X to account Y. <br>
                    Transaction T   <br>
            
            | Before : X = 500   | Y = 200 |
            | ------------- | ------------- |
            | T1 | T2 |
            | Read X  | Read Y |
            | X= X-100 | Y=Y+100  |
            | Write X | Write Y  |
            | After: X = 400  | Y = 300  |
       
                  
        
   If the transaction fails after completion of T1 but before completion of T2.( say, after write(X) but before write(Y)),    then amount has been deducted from X but not added to Y. This results in an inconsistent database state. Therefore, the transaction must be executed in entirety in order to ensure correctness of database state. <br>

  2.  Consistency : <br>
      Once the transaction is executed, it should move from one consistent state to another. The integrity  <br>
      constraints are maintained so that the database is consistent before and after the transaction. <br>
      For example, <br>
      Total before T occurs = 500+200=700 <br> 
      Total after T occurs= 400+300=700  <br>
      <br>
      Therefore, the database is consistent. In the case when T1 is completed but T2 fails, then inconsistency will occur.           <br>
  
  3.  Isolation :<br>
      It shows that the data which is used at the time of execution of a transaction cannot be used by the second transaction       until the first one is completed.<br>
      For example,<br>
      In isolation, if the transaction T1 is being executed and using the data item X, then that data item can't be accessed         by any other transaction T2 until the transaction T1 ends.<br>
      <br>
      The concurrency control subsystem of the DBMS enforced the isolation property.<br>
      <br>
  4. Durability :<br>
    The durability property is used to indicate the performance of the database's consistent state. It states that 
    the transaction made the permanent changes. <br>
    
    
 ### Transaction Control Statments
 
 ### How to see the 'autocommit' variable in mysql: 

mysql> show global variables like 'autocommit'; <br>

| Variable_name | Value |
|---------------|-------|
| autocommit    | ON    |

<br>
1 row in set (0.03 sec)

or

The @@ prefix denotes a server variable. The 1 means that autocommit is currently enabled.
mysql> select @@autocommit;

| @@autocommit |
|--------------|
|            1 |

1 row in set (0.01 sec)

### Rollback 

-This command can only be used to undo transactions since the last COMMIT or ROLLBACK command was issued.

If suppose we have a table called employee, now we insert one new row in it.

mysql> select * from employee;

| id | fname | lname | salary | commission | address |
|----|-------|-------|--------|------------|---------|
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
|  7 | SDC   | G     |  12000 |         70 | null    |
|  8 | hshg  | hsgh  |   1298 |        100 | NULL    |

8 rows in set (0.00 sec)

mysql> insert into employee values(9,'Nina','P',1200,100,'Pune');
Query OK, 1 row affected (0.02 sec)


After inserting new row now we don't want that new row inserted. We fire rollback command. 
mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from employee;

| id | fname | lname | salary | commission | address |
|----|-------|-------|--------|------------|---------|
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
|  7 | SDC   | G     |  12000 |         70 | null    |
|  8 | hshg  | hsgh  |   1298 |        100 | NULL    |
|  9 | Nina  | P     |   1200 |        100 | Pune    |

9 rows in set (0.00 sec)

There is no roll back as MySQL runs with autocommit mode enabled.
To disable autocommit mode, use the START TRANSACTION statement. See the following example :

mysql> start transaction;
Query OK, 0 rows affected (0.01 sec)

mysql> update employee set lname='Pawar' where id= 9;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from employee;<br>
| id | fname | lname | salary | commission | address |
|----|-------|-------|--------|------------|---------|
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
|  7 | SDC   | G     |  12000 |         70 | null    |
|  8 | hshg  | hsgh  |   1298 |        100 | NULL    |
|  9 | Nina  | Pawar |   1200 |        100 | Pune    |
9 rows in set (0.00 sec)

mysql> rollback;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from employee;<br>
| id | fname | lname | salary | commission | address |
|----|-------|-------|--------|------------|---------|
|  1 | Meena | D     |  12000 |        200 | Pune    |
|  2 | Sid   | I     |  24000 |       2000 | Mumbai  |
|  3 | Dip   | R     |  14000 |        500 | Mumbai  |
|  4 | Jan   | R     |  19000 |       NULL | Mumbai  |
|  5 | John  | O     |  40000 |          0 | Mumbai  |
|  6 | Sarah | P     |   8000 |       NULL | Mumbai  |
|  7 | SDC   | G     |  12000 |         70 | null    |
|  8 | hshg  | hsgh  |   1298 |        100 | NULL    |
|  9 | Nina  | P     |   1200 |        100 | Pune    |
9 rows in set (0.00 sec)



### Note:

Transactional control commands are only used with the DML Commands such as - INSERT, UPDATE and DELETE only. They cannot be used while creating tables or dropping them because these operations are automatically committed in the database.


### Commit
Use commit for commits the current transaction, making its changes permanent.

For example: 
mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into employee values(11,'geetu','p',1211,20,'mumbai');
Query OK, 1 row affected (0.00 sec)

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
|  9 | Nina  | P     |   1200 |        100 | Pune    |
| 10 | gita  | T     |   1201 |         10 | mumbai  |
| 11 | geetu | p     |   1211 |         20 | mumbai  |
+----+-------+-------+--------+------------+---------+
11 rows in set (0.01 sec)

mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

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
|  9 | Nina  | P     |   1200 |        100 | Pune    |
| 10 | gita  | T     |   1201 |         10 | mumbai  |
+----+-------+-------+--------+------------+---------+
10 rows in set (0.00 sec)

 
### Savepoint

The SAVEPOINT statement sets a named transaction savepoint with a name of identifier. If the current transaction has a savepoint with the same name, the old savepoint is deleted and a new one is set.

    
    
    
    
  
