# Authentication
* Authentication is the process of verifying the identity of a user or client.
* There are three main types of authentication:
  - Something you know, such as a password or the answer to a security question. These are sometimes called "knowledge factors".
  - Something you have, This is a physical object such as a mobile phone or security token. These are sometimes called "possession factors".
  - Something you are or do. For example, your biometrics or patterns of behaviour. These are sometimes called "inherence factors".

* Authentication is the process of verifying that a user is who they claim to be. Authorization involves verifying whether a user is allowed to do something.
* Most vulnerabilities in authentication mechanisms occur in one of two ways:
  - The authentication mechanisms are weak because they fail to adequately protect against brute-force attacks.
  - Logic flaws or poor coding in the implementation allow the authentication mechanisms to be bypassed entirely by an attacker. This is sometimes called "broken authentication".
* The impact of authentication vulnerabilities can be severe. If an attacker bypasses authentication or brute-forces their way into another user's account, they have access to all the data and functionality that the compromised account has.
  
## Testing Access Control:
* Password-based Login:
  - For websites that adopt a password-based login process, users either register for an account themselves or they are assigned an account by an administrator. This account is associated with a unique username and a secret password, which the user enters in a login form to authenticate themselves.
  - A major security issue with password-based login is brute-forcing attacks (A brute-force attack is when an attacker uses a system of trial and error to guess valid user credentials):
    1. Brute-forcing usernames:
       * Usernames are especially easy to guess if they conform to a recognizable pattern
       * Even if there is no obvious pattern, sometimes even high-privileged accounts are created using predictable usernames, such as admin or administrator.
       * Check whether the website discloses potential usernames publicly. For example, are you able to access user profiles without logging in? Even if the actual content of the profiles is hidden, the name used in the profile is sometimes the same as the login username.
       * Check HTTP responses to see if any email addresses are disclosed. Occasionally, responses contain email addresses of high-privileged users, such as administrators or IT support.
    2. Brute-forcing passwords:
       * While high-entropy passwords are difficult for computers alone to crack, we can use a basic knowledge of human behaviour to exploit the vulnerabilities that users unwittingly introduce to this system. Rather than creating a strong password with a random combination of characters, users often take a password that they can remember and try to crowbar it into fitting the password policy (i.e. Mypassword1! or Myp4$$w0rd)
       * In cases where the policy requires users to change their passwords on a regular basis, it is also common for users to just make minor, predictable changes to their preferred password. For example, *Mypassword1!* becomes *Mypassword2!*.
       * This knowledge of likely credentials and predictable patterns means that brute-force attacks can often be much more sophisticated, and therefore effective, than simply iterating through every possible combination of characters.
  - Username enumeration:
    * Username enumeration is when an attacker is able to observe changes in the website's behavior in order to identify whether a given username is valid.
    * Username enumeration typically occurs either on the login page, for example, when you enter a valid username but an incorrect password, or on registration forms when you enter a username that is already taken.
    * This greatly reduces the time and effort required to brute-force a login because the attacker is able to quickly generate a shortlist of valid usernames.
  - While attempting to brute-force a login page, you should pay particular attention to any differences in
    1. Status codes: During a brute-force attack, the returned HTTP status code is likely to be the same for the vast majority of guesses because most of them will be wrong. If a guess returns a different status code, this is a strong indication that the username was correct. It is best practice for websites to always return the same status code regardless of the outcome, but this practice is not always followed.
    2. Error messages: Sometimes the returned error message is different depending on whether both the username AND password are incorrect or only the password was incorrect. It is best practice for websites to use identical, generic messages in both cases, but small typing errors sometimes creep in. Just one character out of place makes the two messages distinct, even in cases where the character is not visible on the rendered page.
    3. Response times: If most of the requests were handled with a similar response time, any that deviate from this suggest that something different was happening behind the scenes. This is another indication that the guessed username might be correct. For example, a website might only check whether the password is correct if the username is valid. This extra step might cause a slight increase in the response time. This may be subtle, but an attacker can make this delay more obvious by entering an excessively long password that the website takes noticeably longer to handle.     
     
## How to Prevent
* Never rely on obfuscation alone for access control.
* Unless a resource is intended to be publicly accessible, deny access by default.
* Wherever possible, use a single application-wide mechanism for enforcing access controls.
* At the code level, make it mandatory for developers to declare the access that is allowed for each resource, and deny access by default.
* Thoroughly audit and test access controls to ensure they work as designed.
