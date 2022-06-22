Sometimes, the brute-force protection is broken, which gives the atttacker some space to attack.  

Observe that your IP is temporarily blocked if you submit 3 incorrect logins in a row. However, notice that you can reset the counter for the number of failed login attempts by logging in to your own account before this limit is reached.  

To avoid IP blocking, we set two lists for username and password respectively.

The username list is a repeat of 'carlos' and 'winer'. Among them, 'winer' is the given credential username. 'carlos' is the victim's username.

The password list is a given password list, inserted the correct password 'peter' once in each line.

In this way, we will get a lot of status 302 with payload1=wiener and payload2=peter, and the entry payload1=carlos and payload2=123123 is within it.
