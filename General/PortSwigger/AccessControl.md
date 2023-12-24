# Access Control
* Access control is the application of constraints on who or what is authorized to perform actions or access resources.
* Access Control can be any of:
  - Authentication confirms that the user is who they say they are.
  - Session management identifies which subsequent HTTP requests are being made by that same user.
  - Access control determines whether the user is allowed to carry out the action that they are attempting to perform.
* Vertical access controls are mechanisms that restrict access to sensitive functionality to specific types of users (For example, an administrator might be able to modify or delete any user's account, while an ordinary user has no access to these actions.)
* Horizontal access controls are mechanisms that restrict access to resources to specific users (For example, a banking application will allow a user to view transactions and make payments from their own accounts, but not the accounts of any other user.)
* Context-dependent access controls restrict access to functionality and resources based upon the state of the application or the user's interaction with it (For example, a retail website might prevent users from modifying the contents of their shopping cart after they have made payment.)
* Often, a horizontal privilege escalation attack can be turned into a vertical privilege escalation, by compromising a more privileged user.
* Access Control can be detected using IDORs.

## Testing Access Control:
* Unprotected Functionality:
  - At its most basic, vertical privilege escalation arises where an application does not enforce any protection for sensitive functionality.
  - For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might be able to access the administrative functions by browsing to the relevant admin URL.

* Parameter-based access control methods 
  - Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could be:
    1. A hidden field.
    2. A cookie.
    3. A preset query string parameter.

* Broken access control resulting from platform misconfiguration
  - Some applications enforce access controls at the platform layer. they do this by restricting access to specific URLs and HTTP methods based on the user's role.
  - Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as X-Original-URL and X-Rewrite-URL.
  - Some websites tolerate different HTTP request methods when performing an action. If an attacker can use the GET (or another) method to perform actions on a restricted URL.

* Broken access control resulting from URL-matching discrepancies
  - Websites can vary in how strictly they match the path of an incoming request to a defined endpoint. For example, they may tolerate inconsistent capitalization, so a request to /ADMIN/DELETEUSER may still be mapped to the /admin/deleteUser endpoint.
  - Similar discrepancies can arise if developers using the Spring framework have enabled the useSuffixPatternMatch option. This allows paths with an arbitrary file extension to be mapped to an equivalent endpoint with no file extension. In other words, a request to /admin/deleteUser.anything would still match the /admin/deleteUser pattern. Prior to Spring 5.3, this option is enabled by default.
  - On other systems, you may encounter discrepancies in whether /admin/deleteUser and /admin/deleteUser/ are treated as distinct endpoints.

* Access control vulnerabilities in multi-step processes
  - Many websites implement important functions over a series of steps.
  - Sometimes, a website will implement rigorous access controls over some of these steps, but ignore others.
  - Imagine a website where access controls are correctly applied to the first and second steps, but not to the third step.
  - An attacker can gain unauthorized access to the function by skipping the first two steps and directly submitting the request for the third step with the required parameters.

* Referer-based access control
  - Some websites base access controls on the Referer header submitted in the HTTP request.
  - The Referer header can be added to requests by browsers to indicate which page initiated a request.

* Location-based access control
  - Some websites enforce access controls based on the user's geographical location.
  - These access controls can often be circumvented by the use of web proxies, VPNs, or manipulation of client-side geolocation mechanisms.


## How to Prevent
* Never rely on obfuscation alone for access control.
* Unless a resource is intended to be publicly accessible, deny access by default.
* Wherever possible, use a single application-wide mechanism for enforcing access controls.
* At the code level, make it mandatory for developers to declare the access that is allowed for each resource, and deny access by default.
* Thoroughly audit and test access controls to ensure they work as designed.
