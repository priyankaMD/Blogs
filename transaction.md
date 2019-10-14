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
        —Abort: If a transaction aborts, changes made to database are not visible.
        —Commit: If a transaction commits, changes made are visible.
  

  
