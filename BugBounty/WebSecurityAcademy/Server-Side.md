# Server Side Vulnerabilities

## Path Traversal

* Path traversal is also known as directory traversal. These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application.
* In some cases, an attacker might be able to write to arbitrary files on the server, allowing them to modify application data or behavior, and ultimately take full control of the server.
* Imagine a shopping application that displays images of items for sale. This might load an image using the following HTML: *<img src="/loadImage?filename=218.png">*
* The loadImage URL takes a filename parameter and returns the contents of the specified file. This application implements no defenses against path traversal attacks. As a result, an attacker can request the following URL to retrieve the /etc/passwd file from the server's filesystem: *https://insecure-website.com/loadImage?filename=../../../etc/passwd*
* On Windows, both ../ and ..\ are valid directory traversal sequences. The following is an example of an equivalent attack against a Windows-based server: *https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini*



## Access Control

#### Introduction
* Access control is the application of constraints on who or what is authorized to perform actions or access resources.
* In the context of web applications, access control is dependent on authentication and session management:
  - Authentication confirms that the user is who they say they are.
  - Session management identifies which subsequent HTTP requests are being made by that same user.
  - Access control determines whether the user is allowed to carry out the action that they are attempting to perform.
* Broken access controls are common and often present a critical security vulnerability.
* Access control design decisions have to be made by humans so the potential for errors is high.


#### Vertical Privilege Escalation
* If a user can gain access to functionality that they are not permitted to access then this is vertical privilege escalation. For example, if a non-administrative user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation.


#### Unprotected functionality
* At its most basic, vertical privilege escalation arises where an application does not enforce any protection for sensitive functionality. For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might be able to access the administrative functions by browsing to the relevant admin URL.
* In some cases, the administrative URL might be disclosed in other locations, such as the robots.txt file
* Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality.
* In some cases, sensitive functionality is concealed by giving it a less predictable URL. This is an example of so-called "security by obscurity". However, hiding sensitive functionality does not provide effective access control because users might discover the obfuscated URL in a number of ways.
* The URL might be disclosed in JavaScript that constructs the user interface based on the user's role


#### Parameter-based access control methods
*  Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could be:
    - A hidden field.
    - A cookie.
    - A preset query string parameter.
* This approach is insecure because a user can modify the value and access functionality they're not authorized to, such as administrative functions.


#### Horizontal privilege escalation
* Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of that type.
* For example, if an employee can access the records of other employees as well as their own, then this is horizontal privilege escalation.
* Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. For example, a user might access their own account page using the following URL: *https://insecure-website.com/myaccount?id=123* If an attacker modifies the id parameter value to that of another user, they might gain access to another user's account page, and the associated data and functions.
* In some applications, the exploitable parameter does not have a predictable value. For example, instead of an incrementing number, an application might use globally unique identifiers (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.
* Often, a horizontal privilege escalation attack can be turned into a vertical privilege escalation, by compromising a more privileged user. 


## Authentication
* Conceptually, authentication vulnerabilities are easy to understand. However, they are usually critical because of the clear relationship between authentication and security. 
* Authentication vulnerabilities can allow attackers to gain access to sensitive data and functionality. They also expose additional attack surface for further exploits.

#### Authentication vs Authorization
*  Authentication is the process of verifying that a user is who they claim to be. Authorization involves verifying whether a user is allowed to do something.

#### Brute-force Attacks
* A brute-force attack is when an attacker uses a system of trial and error to guess valid user credentials.
* These attacks are typically automated using wordlists of usernames and passwords.
* Brute-forcing is not always just a case of making completely random guesses at usernames and passwords. By also using basic logic or publicly available knowledge, attackers can fine-tune brute-force attacks to make much more educated guesses.

##### Brute-forcing usernames
* Usernames are especially easy to guess if they conform to a recognizable pattern, such as an email address. For example, it is very common to see business logins in the format *firstname.lastname@somecompany.com*
* However, even if there is no obvious pattern, sometimes even high-privileged accounts are created using predictable usernames, such as *admin* or *administrator*
* During auditing, check whether the website discloses potential usernames publicly. For example, are you able to access user profiles without logging in? Even if the actual content of the profiles is hidden, the name used in the profile is sometimes the same as the login username.
* You should also check HTTP responses to see if any email addresses are disclosed. Occasionally, responses contain email addresses of high-privileged users, such as administrators or IT support.

##### Brute-forcing passwords
* Passwords can similarly be brute-forced, with the difficulty varying based on the strength of the password.
* Many websites adopt some form of password policy, which forces users to create high-entropy passwords that are, theoretically at least, harder to crack using brute-force alone. Examples of these:
  - A minimum number of characters
  - A mixture of lower and uppercase letters
  - At least one special character

* Rather than creating a strong password with a random combination of characters, users often take a password that they can remember and try to crowbar it into fitting the password policy. For example, if *mypassword* is not allowed, users may try something like *Mypassword1!* or *Myp4$$w0rd* instead.
* In cases where the policy requires users to change their passwords on a regular basis, it is also common for users to just make minor, predictable changes to their preferred password. For example, *Mypassword1!* becomes *Mypassword1?* or *Mypassword2!*
* This knowledge of likely credentials and predictable patterns means that brute-force attacks can often be much more sophisticated, and therefore effective, than simply iterating through every possible combination of characters.

##### Username enumeration
* Username enumeration is when an attacker is able to observe changes in the website's behavior in order to identify whether a given username is valid.
* Username enumeration typically occurs either on the login page, for example, when you enter a valid username but an incorrect password, or on registration forms when you enter a username that is already taken.
* While attempting to brute-force a login page, you should pay particular attention to any differences in:
  - Status codes: During a brute-force attack, the returned HTTP status code is likely to be the same for the vast majority of guesses because most of them will be wrong. If a guess returns a different status code, this is a strong indication that the username was correct. It is best practice for websites to always return the same status code regardless of the outcome, but this practice is not always followed.
  - Error messages: Sometimes the returned error message is different depending on whether both the username AND password are incorrect or only the password was incorrect. It is best practice for websites to use identical, generic messages in both cases, but small typing errors sometimes creep in. Just one character out of place makes the two messages distinct, even in cases where the character is not visible on the rendered page.
  - Response times: If most of the requests were handled with a similar response time, any that deviate from this suggest that something different was happening behind the scenes. This is another indication that the guessed username might be correct. For example, a website might only check whether the password is correct if the username is valid. This extra step might cause a slight increase in the response time. This may be subtle, but an attacker can make this delay more obvious by entering an excessively long password that the website takes noticeably longer to handle.

#### Bypassing two-factor authentication
* At times, the implementation of two-factor authentication is flawed to the point where it can be bypassed entirely.
* If the user is first prompted to enter a password, and then prompted to enter a verification code on a separate page, the user is effectively in a "logged in" state before they have entered the verification code. In this case, it is worth testing to see if you can directly skip to "logged-in only" pages after completing the first authentication step. Occasionally, you will find that a website doesn't actually check whether or not you completed the second step before loading the page.

## Server-side request forgery (SSRF)
* Server-side request forgery is a web security vulnerability that allows an attacker to cause the server-side application to make requests to an unintended location.
* In a typical SSRF attack, the attacker might cause the server to make a connection to internal-only services within the organization's infrastructure. In other cases, they may be able to force the server to connect to arbitrary external systems. This could leak sensitive data, such as authorization credentials.
* In an SSRF attack against the server, the attacker causes the application to make an HTTP request back to the server that is hosting the application, via its loopback network interface.
* This typically involves supplying a URL with a hostname like *127.0.0.1* (a reserved IP address that points to the loopback adapter) or *localhost* (a commonly used name for the same adapter).
* For example, imagine a shopping application that lets the user view whether an item is in stock in a particular store. To provide the stock information, the application must query various back-end REST APIs. It does this by passing the URL to the relevant back-end API endpoint via a front-end HTTP request. When a user views the stock status for an item, their browser makes the following request:

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```

 This causes the server to make a request to the specified URL, retrieve the stock status, and return this to the user.
 In this example, an attacker can modify the request to specify a URL local to the server: 

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```

The server fetches the contents of the */admin* URL and returns it to the user. 

* An attacker can visit the */admin* URL, but the administrative functionality is normally only accessible to authenticated users. This means an attacker won't see anything of interest. However, if the request to the */admin* URL comes from the local machine, the normal access controls are bypassed. The application grants full access to the administrative functionality, because the request appears to originate from a trusted location.

* Why do applications behave in this way, and implicitly trust requests that come from the local machine? This can arise for various reasons:

    - The access control check might be implemented in a different component that sits in front of the application server. When a connection is made back to the server, the check is bypassed.
    - For disaster recovery purposes, the application might allow administrative access without logging in, to any user coming from the local machine. This provides a way for an administrator to recover the system if they lose their credentials. This assumes that only a fully trusted user would come directly from the server.
    - The administrative interface might listen on a different port number to the main application, and might not be reachable directly by users.

* These kind of trust relationships, where requests originating from the local machine are handled differently than ordinary requests, often make SSRF into a critical vulnerability.

#### SSRF attacks against other back-end systems
* In some cases, the application server is able to interact with back-end systems that are not directly reachable by users. These systems often have non-routable private IP addresses. The back-end systems are normally protected by the network topology, so they often have a weaker security posture. In many cases, internal back-end systems contain sensitive functionality that can be accessed without authentication by anyone who is able to interact with the systems.



## OS command injection
* OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data.
* Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure, and exploit trust relationships to pivot the attack to other systems within the organization.
*  After you identify an OS command injection vulnerability, it's useful to execute some initial commands to obtain information about the system. Below is a summary of some commands that are useful on Linux and Windows platforms:

  ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/294b27e3-6aac-4ae8-ad8e-68af5772658c)

* Placing the additional command separator & after the injected command is useful because it separates the injected command from whatever follows the injection point. This reduces the chance that what follows will prevent the injected command from executing.

