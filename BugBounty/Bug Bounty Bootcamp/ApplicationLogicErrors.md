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
