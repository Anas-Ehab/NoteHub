# OS Command Injection
* It's a vulnerability that allows an attacker to execute operating system (OS) commands on the server that is running an application.
* Many instances of OS command injection are blind vulnerabilities. This means that the application does not return the output from the command within its HTTP response.
  - Detecting can occur through time delays, for example: *\& ping -c 10 127.0.0.1 \&*
  - Detecting through redirecting output, for example: *\& whoami \> \/var\/www\/static\/whoami.txt \&* and then trying to access the text file *https://vulnerable-website.com/whoami.txt*
  - Detecting through out-of-band (OAST) techniques, for example: *\& nslookup kgji2ohoyw.web-attacker.com \&* this command is used to send a DNS query to the *web-attacker.com* monitor the *web-attack.com* DNS server to see if a query reached.
* The different shell metacharacters have subtly different behaviours that might change whether they work in certain situations.
* The following command separators work on both Windows and Unix-based systems:
  - \&
  - \&&
  - \|
  - \|\|
  - \* 

## Example: 
* A shopping application lets the user view whether an item is in stock in a particular store. This information is accessed via a URL: *https://insecure-website.com/stockStatus?productID=381&storeID=29*
* To provide the stock information, the application must query various legacy systems. For historical reasons, the functionality is implemented by calling out to a shell command with the product and store IDs as arguments.

## How to prevent
* The most effective way to prevent OS command injection vulnerabilities is to never call out to OS commands from application-layer code. In almost all cases, there are different ways to implement the required functionality using safer platform APIs.
* Validating against a whitelist of permitted values.
* Validating that the input is a number.
* Validating that the input contains only alphanumeric characters, no other syntax or whitespace.
