# Application Logic Errors & Broken Access Control

### Explanation
* Application logic errors are logic flaws in an application.
* Application logic errors and broken access control issues are often triggered by perfectly valid HTTP requests containing no illegal or malformed character sequences.
* These requests are crafted intentionally to misuse the application’s logic for malicious purposes or circumvent the application’s access control.
* To find these vulnerabilities, you cannot simply rely on your technical knowledge. Instead, you need to use your creativity and intuition to bypass restrictions set by the developers.
* Application logic errors like these are prevalent because these flaws cannot be scanned for automatically. They can manifest in too many ways, and most current vulnerability scanners don’t have the intelligence to understand application logic or business requirements.

### Application Logic Errors (Business Logic Vulnerabilities)
* Ways of using the legitimate logic flow of an application that result in a negative consequence to the organization.
* For example, let’s say an application implements a three-step login process. First, the application checks the user’s password. Then, it sends an MFA code to the user and verifies it. Finally, the application asks a security question before logging in the user:

Step 1 (Password Check) --> Step 2 (MFA) --> Step 3 (Security Questions)

Sometimes, though, users can reach step 3 in the authentication process without clearing steps 1 and 2. While the vulnerable application redirects users to step 3 after the completion of step 2, it doesn’t verify that step 2 is completed before users are allowed to advance to step 3.
In this case, all the attacker has to do is to manipulate the site’s URL and directly request the page of a later stage.

* Another example is during multi­-step checkout processes. Let’s say an online shop allows users to pay via a saved payment method. 

  When users save a new payment method, the site will verify whether the credit card is valid and current. That way, when the user submits an order via a saved payment method, the application won’t have to verify it again.
  Let's take this request for example (payment_id refers to the user's saved credit card): 

    *POST /new_order
    Host: shop.example.com
    (POST request body)
    item_id=123
    &quantity=1
    &saved_card=1
    &payment_id=1*

  The request for payment using a new credit card:

    *POST /new_order
    Host: shop.example.com
    (POST request body)
    item_id=123
    &quantity=1
    &card_number=1234-1234-1234-1234*

  The application also determines whether the payment method is new by the existence of the saved_card parameter in the HTTP request. 

  So a malicious user can submit a request with a saved_card parameter and a fake credit card number. Because of this error in payment verification, they could order unlimited items for free with the unverified card using this query:

    *POST /new_order
    Host: shop.example.com
    (POST request body)
    item_id=123
    &quantity=1
    &saved_card=1
    &card_number=0000-0000-0000-0000*


### Broken Access Control
* Broken access control occurs when access control in an application is improperly implemented and can be bypassed by an attacker.
* Exposed Admin Panels
  - Applications sometimes neglect or forget to lock up sensitive functionalities such as the admin panels used to monitor the application.
  - Developers may mistakenly assume that users can’t access these functionalities because they aren’t linked from the main application, or because they’re hidden behind an obscure URL or port.
  - Attackers can often access these admin panels without authentication, if they can locate them.
  
    let’s say the usual way of accessing example.com’s admin panel is via the URL *https://example.com/YWRtaW4/admin.php*.

    If you browse to that URL, you’ll be prompted to log in with your credentials.

    After that, you’ll be redirected to https://example.com/YWRtaW4/dashboard.php, which is where the admin panel resides.

    Users might be able to browse to *https://example.com/YWRtaW4/dashboard.php* and directly access the admin panel, without providing credentials, if the application doesn’t implement access          control at the dashboard page.

    
* Directory Traversal Vulnerabilities
  - They happen when attackers can view, modify, or execute files they shouldn’t have access to by manipulating file paths in user-input fields.
  - Let’s say example.com has a functionality that lets users access their uploaded files. Browsing to the URL *http://example.com/uploads?file=example.jpeg* will cause the application to display   the file named *example.jpeg* in the user’s uploads folder located at */var/www/html/uploads/USERNAME/*.

    If the application doesn’t implement input sanitization on the file parameter, a malicious user could use the sequence *../* to escape out of the uploads folder and read arbitrary files on the system.


### Prevention
* You can prevent application logic errors by performing tests to verify that the application’s logic is working as intended.
* Carefully review each process for any logical flaws that might lead to a security issue.
* Implement granular access control policies on all files and actions on a system.


### Hunting for Application Logic Errors and Broken Access Control
1- Learn About Your Target
* Start by learning about your target application. Browse the application as a regular user to uncover functionalities and interesting features.
* You can also read the application’s engineering blogs and documentation.
* Test newer features first, since new features are often the least tested by other hackers.
* If you find out that the application uses WordPress, you should try to access */wp-admin/admin.php*, the default path for WordPress admin portals.

2- Intercept Requests While Browsing
* Intercept requests while browsing the site and pay attention to sensitive functionalities.
* Take note of how sensitive functionalities and access control are implemented, and how they interact with client requests.

3- Think Outside The Box
* Use your creativity to think of ways to bypass access control or otherwise interfere with application logic.


### Escalating the Attack
* Escalating application logic errors and broken access control depends entirely on the nature of the flaw you find.
* A general rule of thumb is that you can try to combine the application logic error or broken access control with other vulnerabilities to increase their impact.
* Think of ways malicious users can exploit these vulnerabilities to the fullest extent, and communicate their impact in detail in your report.
