

A tracking cookie was used for analytics, and some SQL querys with value will be followed to test.  
从tracking cookie入手进行分析，在其之后注入一些查询语句。

The querys will not return any result, and no error messages will be displayed. The only signal is if the returned page contains "Welcome Back" message.  
评价是否猜测成功的标准是查看返回信息是否包含“Welcome Back”  

The querys including:

`TrackingId=xyz' AND '1'='1 `  

`TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a `  

`TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a `  

A trick is that we can put the proxy from repeater to intruder, and then add positions and set payloads,
to help to crack the password we need.
