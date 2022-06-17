In this lab, you are given a list of username and a list of password.To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.


1. Turn on the Burp in FireFox, open the webiste and click on the _My_account_, try to input a random ussername and password to login.  

2. In Burp Suite Procy, under HTTP history, found the /login entry.

3. Send it to Intruder, try username field and password field corresponding to the given list.

4. Found the one that has different length.
