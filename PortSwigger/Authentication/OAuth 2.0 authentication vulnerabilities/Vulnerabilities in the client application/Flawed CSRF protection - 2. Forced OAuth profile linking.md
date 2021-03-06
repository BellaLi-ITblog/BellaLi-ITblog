## Background  
Due to the insecure implementation of the OAuth flow by the client application, an attacker can manipulate this functionality to obtain access to other users' accounts.  

To solve the lab, use a CSRF attack to attach your own social media profile to the admin user's account on the blog website, then access the admin panel and delete Carlos.  

The admin user will open anything you send from the exploit server and they always have an active session on the blog website.  
 
Blog website account: wiener:peter  
Social media profile: peter.wiener:hotdog  

## Steps  
1. With Burp is on, login with our own credentials and then link the social media account.  

2. In Burp HTTP history, find the record GET /auth?client_id[...]. There is **no** state parameter to protect against CSRF attacks.    
![image](https://user-images.githubusercontent.com/106157137/176172625-c95c6302-edf2-4293-983f-b4e159b9e2c9.png)  

3. Turn on Intercept in Burp, and click on "attach socail media" in browser.  

4. In Intercept find the intercepted one for GET /oauth-linking?code=[...]. Right click on this request and select "copy URL". Drop this request.  
> This is **important** to ensure that the code is not used and, therefore, remains valid.  

![image](https://user-images.githubusercontent.com/106157137/176173586-122bd780-51ed-4350-9159-2b8f0010ba75.png)

5. Turn off the intercept and log out of the blog website.  

6. Go to the exploit server and create an iframe. The src attribute points to the URL we just copied.  
![image](https://user-images.githubusercontent.com/106157137/176175084-a1adc440-5e14-4b8f-9400-c46c350a40b5.png)  
> <iframe> is to load another HTML page within the document. It essentially puts another webpage withnin the parent page.  

7. Deliver exploit to the victim. When their browser loads the iframe, it will complete the OAuth flow using your social media profile, attaching it to the admin account on the blog website.  

8. In browser, select the "log in with social media" option. And you will be logged in as the admin user. Go to the admin panel and delete Carlos's account.  
