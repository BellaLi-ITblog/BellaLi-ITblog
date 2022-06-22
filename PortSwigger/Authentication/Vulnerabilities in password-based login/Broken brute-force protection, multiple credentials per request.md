Firstly, we need to investigate the login page by observing the POST /login request.
<img width="1145" alt="1655789152(1)" src="https://user-images.githubusercontent.com/106157137/174722618-24383205-c004-4366-a0d6-5d6cf8559533.png">


The key point to solve the problem is to find the format that contains the login credentials is **JSON**.
<img width="316" alt="1655788179(1)" src="https://user-images.githubusercontent.com/106157137/174720712-8ab40193-06c3-49fe-91d4-2fea793b176b.png">

In BurpSuite, replace the single string value of username with the one provided, and replace the single string value of password with an array containing all of the candidate passwords.

Send the request, a 302 response should be returned.

Right-click on the request and select **Show response in browser**. Copy the URL and load it in the browser. You will be logged in.
