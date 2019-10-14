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
            | Before : X = 500  | Y = 200       |
            | ----------------- | ------------- |
            |   T1              |   T2          |
            |  Read X           |   Read Y      |
            |  X= X-100         |   Y=Y+100     |
            |  Write X          |   Write Y     |
            |  After: X = 400   |    Y = 300    |
                  
        
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
  
