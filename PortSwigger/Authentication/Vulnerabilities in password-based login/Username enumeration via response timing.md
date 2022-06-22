This lab is vulnerable to username enumeration using its response times. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

If you try invalid username and password for too many times, your IP might be blocked. To solve this problem, `X-Forwarded-For: how many times` can be used.  

Make sure the testing password is **long enough**, because:  
 
> Invalid username - > response time is roughly the same  
> Valid useranme   - > response time is increasing depend on the length of password  


Using pitchfork as the attack type.  
Here is an explanation of the difference between pitchfork and cluster bomb.  
> Pitchfork:  
> ![image](https://user-images.githubusercontent.com/106157137/174254867-edfd5e77-91e8-4d1e-a1a9-cf627d9c2b84.png)

> Cluster bomb
> ![image](https://user-images.githubusercontent.com/106157137/174255228-11d5d3a9-1b09-49f8-a3f6-5c99a599e799.png)

According to the result of response time, we can the username, which takes the longest processing time.  

Then we go back to the intruder, change the position to `X-Forwarded-For` and `password`, and follow the rest of the steps as we have done in previous labs.
