### Transaction
  A transaction is a single logical unit of work which accesses and possibly modifies the contents of a database.
  
  Transactions access data using: 
    1. Read Operation
    2. Write Operation
  In order to maintain consistency in a database, before and after transaction, certain properties are followed. 
  These are called ACID properties.
  1. Atomicity : (All or nothing rule)
      Each transaction is considered as one unit and either runs to completion or is not executed at all. 
      It involves following two operations.
        —Abort: If a transaction aborts, changes made to database are not visible.
        —Commit: If a transaction commits, changes made are visible.
  2. 

  