To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

It is a bit different compared to the first one as we need to find out the one of which the result is slight different.


## For username:  

On the **Payloads** tab, using **Simple list** payload type.  

On the **Option** tab, under **Grep-Extract**, click **Add**. Find the response of error message and highlight the part. The rest will be adjusted automatically.  

This time, the Intruder attack will return one more column name **Error**, and the one who is slight different from other results will be ticked.

## For password:  

On the **Payloads** tab, using **Simple list** payload type. And follow the rest of the step as last lab.

The one with a 302 response will be the password.

