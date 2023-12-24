# Insecure Direct Object Refernece
* Insecure direct object references (IDOR) are a type of access control vulnerability that arises when an application uses user-supplied input to access objects directly.

## Examples:
* Consider a website that uses the following URL to access the customer account page, by retrieving information from the back-end database: *https://insecure-website.com/customer_account?customer_number=132355*
* If no other controls are in place, an attacker can simply modify the customer_number value, bypassing access controls to view the records of other customers.
* IDOR vulnerabilities often arise when sensitive resources are located in static files on the server-side filesystem. For example, a website might save chat message transcripts to disk using an incrementing filename, and allow users to retrieve these by visiting a URL like the following: *https://insecure-website.com/static/12144.txt*
* In this situation, an attacker can simply modify the filename to retrieve a transcript created by another user and potentially obtain user credentials and other sensitive data.
