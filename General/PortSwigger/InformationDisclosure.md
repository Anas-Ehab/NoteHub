# Information Disclosure
* Information disclosure, also known as information leakage, is when a website unintentionally reveals sensitive information to its users.
* Although some of this information will be of limited use, it can potentially be a starting point for exposing an additional attack surface, which may contain other interesting vulnerabilities.

## Examples
* Revealing the names of hidden directories, their structure, and their contents via a robots.txt file or directory listing.
* Providing access to source code files via temporary backups.
* Explicitly mentioning database table or column names in error messages.
* Unnecessarily exposing highly sensitive information, such as credit card details.
* Hard-coding API keys, IP addresses, database credentials, and so on in the source code.
* Hinting at the existence or absence of resources, usernames, and so on via subtle differences in application behavior.

## How to Prevent
* Audit any code for potential information disclosure as part of your QA or build processes.
* Use generic error messages as much as possible. Don't provide attackers with clues about application behavior unnecessarily.
* Double-check that any debugging or diagnostic features are disabled in the production environment.
