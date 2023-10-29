# Common Attacks

## HTTP Method Tempring
* It is a type of security vulnerability that can be exploited in web applications. It occurs when an attacker manipulates the HTTP request method used to interact with a web server.
* Test with options request to see what methods the request accepts.
* Try tampering the methods and test the results.

## Basic HTTP Authentication
* Basic HTTP authentication is a simple authentication mechanism used in web applications and services to restrict access to certain resources or functionalities.
* Credential Format: The client constructs a string in the format username:password and encodes it in Base64. It then includes this encoded string in an Authorization header in subsequent requests. ( Authorization: Basic dXNlcjpwYXNz)
* How to test in Burp
  - Capture the authorization payload
  - Add passwords payloads
  - In payload processing add 2 rules
    1. Add prefix USERNAME: (i.e. admin)
    2. encode as base64
  - Run the attack
 
