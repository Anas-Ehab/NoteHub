# Insecure Direct Object References

### Explanation

* IDORs happen when users can access resources that do not belong to them by directly referencing the object ID, object number, or filename.
* IDORs are not just limited to reading other users’ information, either. You can also use them to edit data on another user’s behalf.
* Finally, IDORs can affect resources other than database objects. Another type of IDOR happens when applications reference a system file directly. 
* For example, this request allows users to access a file they’ve uploaded: *https://example.com/uploads?file=user1234-01.jpeg.*
Since the value of the file parameter is *user1234–01.jpeg*, we can easily deduce that user-uploaded files follow the naming convention of *USER_ID-FILE_NUMBER.FILE_EXTENSION*.
Therefore, another user’s uploaded files might be named *user1233–01.jpeg* 
If the application doesn’t restrict users’ access to files that belong to others, an attacker could access anyone’s uploaded files by guessing the filenames, like this: 
*https://example.com/uploads?file=user1233-01.jpeg*

### Prevention
* IDORs happen when an application fails at two things. 
* First, it fails to implement access control based on user identity. 
* Second, it fails to randomize object IDs and instead keeps references to data objects, like a file or a database entry, predictable.

Applications can prevent IDORs in two ways:
* First, the application can check the user’s identity and permissions before granting access to a resource. For example, the application can check if the user’s session cookies correspond to the user_id whose messages the user is requesting.
* Second, the website can use a unique, unpredictable key or a hashed identifier to reference each user’s resources.

### Hunting For IDORs
* The best way to discover IDORs is through a source code review that checks if all direct object references are protected by access control.

If you can't access the source code:
1. Create 2 Accounts
- If users can have different permissions on the site, create two accounts for each permission level. For example, create two admin accounts and two regular user accounts.
- This will help you test for access control issues among similar user accounts, as well as across users with different privileges.
- One of the accounts would serve as your attacker account, used to carry out the IDOR attacks. The other would be the victim account used to observe the effects of the attack.
- If the application doesn’t allow you to create so many accounts, you could reach out to the company and ask for more accounts.
- Also, if the application has paid memberships, ask the company for a premium account or pay for one yourself. Quite often, paying for these memberships is worth it, because you gain access to new features to test.
- In addition to testing with two accounts, you should also repeat the testing procedure without signing in. See if you can use an unauthenticated session to access the information.
      
2. Discover Features
- Try to discover as many application features as possible
- Pay special attention to functionalities that return user information or modify user data.
   Examples:
       https://example.com/messages?user_id=1236
       https://example.com/uploads?file=user1236-01.jpeg
       https://example.com/group_files?group=group3
       message_id=user1236-0111
   
3. Capture Requests
- Browse through each application feature you mapped in the preceding step and capture all the requests going from your web client to the server.
- Inspect each request carefully and find the parameters that contain numbers, usernames, or IDs.
- Remember that you can trigger IDORs from different locations within a request, like URL parameters, form fields, file paths, headers, and cookies.
- To make testing more efficient, use two browsers, and log into a different account in each. Then manipulate the requests coming from one browser to see if the change is immediately reflected on the other account.
   
4. Change the IDs
- Switch the IDs in the sensitive requests and check if the information returned also changes.
- See if you can access the victim account’s information by using the attacker account.
- Check if you can modify the second user’s account from the first.
   

### Bypassing IDOR Protection
IDORs can manifest in applications in different ways. Here are a few places to pay attention to, beyond your plain old numeric IDs.

1. Encoded IDs and Hashed IDs
- When faced with a seemingly random string, always suspect that it is encoded and try to decode it.
- Learn to recognize the most common encoding schemes (ie. base64, URL encoding, base64url)
- Use tools to figure out encoding that you don't recognize
- If the application is using a hashed or randomized ID, see if the ID is predictable.
- Sometimes applications use algorithms that produce insufficient entropy (Entropy is the degree of randomness of the ID. The higher the entropy of a string, the harder it is to guess)
- Try creating a few accounts to analyze how these IDs are created. You might be able to find a pattern that will allow you to predict IDs belonging to other users.
   
2. Leaked IDs
- It might also be possible that the application leaks IDs via another API end-point or other public pages of the application.
- For example, *GET /messages?conversation_id=O1SUR7GJ43HS93VAR8xxxx* might seem secure but there might be another method to retrieve the messages using for example *GET /messages?user_id=1236*

3. Offer IDs Instead of Cookies
- In modern web applications, you’ll commonly encounter scenarios in which the application uses cookies instead of IDs to identify the resources a user can access.
- If no IDs exist in the application-generated request, try adding one to the request.
- For example, *GET /api_v1/messages* this request display your messages, try *GET /api_v1/messages?user_id=ANOTHER_USERS_ID*

4. Blind IDORs
- Sometimes endpoints susceptible to IDOR don’t respond with the leaked information directly.
- They might lead the application to leak information elsewhere, instead: in export files, email, and maybe even in text alerts.
- For example, *POST /get_receipt (POST request body) receipt_id=3001* Try changing the receipt_id and see if you receive the receipt of someone else.

5. Change Request Method
- Applications often enable multiple request methods on the same endpoint but fail to implement the same access control for each method.
- For example, *GET example.com/uploads/user1236-01.jpeg* might not be vulnerable but *DELETE example.com/uploads/user1236-01.jpeg* might be.
- If POST requests don’t work, you can also try to update another user’s resource by using the PUT method.
- Another trick that often works is switching between POST and GET requests. If there is a POST request like this *POST /get_receipt (POST request body) receipt_id=2983* *GET /get_receipt?receipt_id=2983*

6. Change Requested File Type
- Switching the file type of the requested file sometimes leads the server to process the authorization differently.
- For example, applications commonly store information in the JSON file type. Try adding the .json extension to the end of the request URL and see what happens.
- *GET /get_receipt?receipt_id=2983* to *GET /get_receipt?receipt_id=2983.json*

### Escalating the Attack
* The impact of an IDOR depends on the affected function, so to maximize the severity of your bugs, you should always look for IDORs in critical functionalities first.
* Both read-based IDORs (which leak information but do not alter the database) and write-based IDORs (which can alter the database in an unauthorized way) can be of high impact.
* In terms of the state-changing (write-based) IDORs, look for IDORs in password reset, password change, and account recovery features, as these often have the highest business impact.
* As for the non-state-changing (read-based) IDORs, look for functionalities that handle the sensitive information in the application. For example, look for functionalities that handle direct messages, personal information, and private content.

### Automating the Attack
* Burp intruder to iterate through IDs to find valid ones.
* Burp extension Autorize (https://github.com/Quitten/Autorize/) scans for authorization issues by accessing higher-privileged accounts with lower-privileged accounts
* Burp extensions Auto Repeater (https://github.com/nccgroup/AutoRepeater/) and AuthMatrix (https://github.com/SecurityInnovation/AuthMatrix/) allow you to automate the process of switching out cookies, headers, and parameters.
