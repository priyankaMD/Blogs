
## What exactly 'Parsing' in DB means :  
The database engine receives queries in the specified format. Once a query is received, it first needs to be parsed, which involves translating it from what is essentially a textual format into a combination of internal binary structures that can be easily manipulated by the optimizer.

## Parser role in parsing :
A parser is a compiler or interpreter component that breaks data into smaller elements for easy translation into another language. A parser takes input in the form of a sequence of tokens or program instructions and usually builds a data structure in the form of a parse tree or an abstract syntax tree.

## Parsing steps
Before the process of finding the best plan is started for the query, there are some tasks that are completed. These tasks are repeatedly executed even if the same query executes in the same session for N number of times:

## 1. Syntax Check : 
  The syntax is checked by comparing the entire text of the query against the supported keywords for the version of             the database currently in use
  For Example: <br/>
  SQL> select ENAME, EMPNO, DEPTNO<br/>
  2  fro SCOTT.EMP<br/>
  3  where deptno=10;<br/>
  fro SCOTT.EMP<br/>
    *<br/>
  ERROR at line 2:<br/>
  ORA-00923: FROM keyword not found where expected<br/>

## 2. Semantics Check : 
  The semantics check to confirm that the correct object name is used and also whether the user has the proper privileges       to execute the query on the object(s) used in the statement.
  For Example: <br/>
  SQL> SELECT * FROM HR.EMPLOYEES;<br/>
  SELECT * FROM EMPLOYEES<br/>
              *<br/>
  ERROR at line 1:<br/>
  ORA-00942: table or view does not exist<br/>
  
## 3. Hashing the query text and generating a hash key-value pair : 
  If the query passes both of the above steps, the next and the most important task is to search for it in the                   SGA(System global Area), part of RAM, more precisely within the Library Cache. Since it’s going to be a memory                 structure,the best way to search within the memory would be via the Hashing mechanism.
  
## Note :  
The previously-mentioned three tasks (syntax check, semantics check and the generation of the hash value for the query) are performed every single time, even when the query is executed in the same session N number of times.

If the given hash value and the statement text exactly match a similar statement in the library cache, the statement is termed to be executed already. This statement can now be executed as a Soft Parsed statement. But if it isn’t, the query must be Hard Parsed.


  


