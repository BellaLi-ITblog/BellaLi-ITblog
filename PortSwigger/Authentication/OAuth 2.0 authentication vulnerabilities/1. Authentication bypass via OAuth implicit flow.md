## Background  
This lab is designed based on a flawed validation by the client application. It makes it possible for an attacker to log in to other's account without knowing the password.  
To solve the lab, log in to Carlos's account. His email address is carlos@carlos-montoya.net.  
You own credentials: `wiener:peter`.  

## Steps  
1. In browser with Burp is on, complete the OAuth login process.  

2. In Burp HTTP history, find the record POST /authenticate and send to Repeater.  
![image](https://user-images.githubusercontent.com/106157137/176097030-8404add2-8819-44a3-b0b8-07a265ccd048.png)

3. Change the value of email to carlos@carlos-montoya.net, and send.  

4. Show response in browser.  
