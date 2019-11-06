
## What is key in DB:
- A key is an attribute or set of an attribute which helps you to identify a row(tuple) in a relation(table). 
- They allow you to find the relation between two tables. 
- Keys help you uniquely identify a row in a table by a combination of one or more columns in that table.
For example:

| Employee ID   | FirstName     | LastName      | 
| ------------- | ------------- | ------------- |
| 11  | Andrew  | Johnson  | 
| 22  | Tom  | wood | 
| 33  | Alex  | hale | 

In the above-given example, employee ID is a primary key because it uniquely identifies an employee record. In this table, no other employee can have the same employee ID.

## Why we need a Key?
- Keys help you to identify any row of data in a table. In a real-world application, a table could contain thousands of records. Moreover, the records could be duplicated. Keys ensure that you can uniquely identify a table record despite these challenges.
- Allows you to establish a relationship between and identify the relation between tables
- Help you to enforce identity and integrity in the relationship.

## Database has follwing types of Keys:
   - Super Key 
   - Primary Key
   - Candidate Key
   - Alternate Key
   - Foreign Key
   - Unique Key
   - Composite Key
   
## What is the Super key?
A superkey is a group of single or multiple keys which identifies rows in a table. A Super key may have additional attributes that are not needed for unique identification.
For Example,

| EmpSSN   | EmpNum  | Empname   | 
| ------------- | ------------- | ------------- |
| 9812345098 | AB05  | Shown  | 
| 9876512345  | AB06  | Roslyn | 
| 199937890  | AB07  | James | 

In the above-given example, EmpSSN and EmpNum name are superkeys.

## What is a Primary Key?
A column or group of columns in a table which helps us to uniquely identifies every row in that table is called a primary key. This DBMS can't be a duplicate. The same value can't appear more than once in the table.
For Example,


| StudID   | Roll No     | First Name      | LastName | Email |
| ------------- | ------------- | ------------- |------------- |------------- |
|1  | 11  | Tom  | Price|abc@gmail.com|
|2  | 22  | Nick | Wright | xyz@gmail.com|
| 3 | 33  |Alex  | hale | mno@yahoo.com|


In the above-given example, StudId is a primary key because it uniquely identifies an student record. In this table, no other student can have the same StudId.

## Rules for defining Primary key:
  - Two rows can't have the same primary key value
  - It must for every row to have a primary key value.
  - The primary key field cannot be null.
  - The value in a primary key column can never be modified or updated if any foreign key refers to that primary key.
  
## What is the Unique key?
A unique key is a set of one or more than one fields/columns of a table that uniquely identify a record in a database table.
You can say that it is little like primary key but it can accept only one null value and it cannot have duplicate values.

For Example: In above table, StudID, Roll No are qualified to become a primary key and Email becomes the unique key.

## What is the Alternate key?
All the keys which are not primary key are called an alternate key. It is a candidate key which is currently not the primary key. However, A table may have single or multiple choices for the primary key.

For Example: In above table, StudID, Roll No, Email are qualified to become a primary key. But since StudID is the primary key, Roll No, Email becomes the alternative key.


## What is a Candidate Key?
A super key with no repeated attribute is called candidate key.
The Primary key should be selected from the candidate keys. Every table must have at least a single candidate key.
Properties of Candidate key:
    • It must contain unique values
    • Candidate key may have multiple attributes
    • Must not contain null values
    • It should contain minimum fields to ensure uniqueness
    • Uniquely identify each record in a table
    
For Example: In above table,Stud ID, Roll No, and email are candidate keys which help us to uniquely identify the student record in the table.

## What is the Foreign key?
A foreign key is a column which is added to create a relationship with another table. Foreign keys help us to maintain data integrity and also allows navigation between two different instances of an entity. Every relationship in the model needs to be supported by a foreign key.
For Example:

| DeptCode   | DeptName  |
| ------------- | ------------- | 
| 001 | Science  |  
| 002  | English  |
| 005  | Computer  |


| Teacher ID   | Fname  | Lname   | DeptCode|
| ------------- | ------------- | ------------- | ------------- |
| B002 | David  | Warner  | 002|
| B017  | Sara  | Joseph | 002|
| B009  | Mike  | Brunton | 001|

In this example, we have two table, teacher and department in a school. However, there is no way to see which search work in which department.
In 2nd table, adding the foreign key in Deptcode to the Teacher name, we can create a relationship between the two tables.
This concept is also known as Referential Integrity.

## What is the Composite key?

A key which has multiple attributes to uniquely identify rows in a table is called a composite key.The composite key may or maybe not a part of the foreign key.















