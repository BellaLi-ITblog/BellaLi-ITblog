## background  
Some websites use function that allows users to stay logged in, however, the cookie used to provide this function may be vulnerbale.  
For example, the attacker can study how their own cookie is generated to find a pattern, and use this pattern to brute force other people's cookie to log on their account.  

> 一个常见功能是即使在关闭浏览器会话后也可以保持登录状态。这通常是一个简单的复选框，标有“记住我”或“让我登录”之类的标签。  
> 但是，一些网站会根据可预测的静态值串联生成此 cookie，例如用户名和时间戳。有些甚至使用密码作为 cookie 的一部分。  
> 这非常危险，因为攻击者可以研究自己的 cookie 并可能推断出它是如何生成的。一旦他们制定出公式，他们就可以尝试暴力破解其他用户的 cookie 以访问他们的帐户。  

## lab instruction  
To solve the lab, brute-force Carlos's cookie to gain access to his "My account" page.  

- Your credentials: wiener:peter  
- Victim's username: carlos  
- You are given a candidate password list 

## steps  
1. Log in to your own account, don't forget to click the **stay logged in** option.  

2. Find out the pattern.  
  - Examine the cookie in Burp Inspector panel, and find it is encoded using base64.
  Decoding the cookie, we get _wiener:51dc30ddc473d43a6011e9ebba6ca770_.
  - Examine the length and character set of the decoded string, it could be an MD5 hash.  

    So the pattern could be:  
      `base64(username+":"+mad5hash(password))`  
    
3. Log out my account.  
4. Send the most recent GET /my-account to Intruder.  
5. Confirm whether my guess about the pattern is correct by using my own credentials to try.  
6. Set the payload position to the **stay_logged_in** cookie.  
7. Set the payload as my own password peter.  
8. Under **Payload processing**, add the following rules:  
    - hash: MD5  
    - Add prefix: wiener:  
    - Encode: Base64-encode  
9. Under **option** tab, add a **grep match** rule to flag any responses containing the string "Update email". As it is shown only when you access the /my-account page successfully.  
10. Start attack.  
11. We got the response with "Update email", which mean our guess of the pattern is correct.  
12. Make some adjustment and repeat the steps:  
    - change the single payload to the cadidate password list  
    - change the **add prefix** from wiener: to carlos:
13. The payload from the response with "update email" is the valid stay-logged-in cookie for Carlos's account.  
