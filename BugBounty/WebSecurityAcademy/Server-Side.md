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
