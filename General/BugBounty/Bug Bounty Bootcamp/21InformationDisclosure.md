# Information Disclosure

### Explanation
* Information disclosure occurs when an application fails to properly protect sensitive information, giving users access to information they shouldn’t have available to them.
* This sensitive information can include technical details that aid an attack, like software version numbers, internal IP addresses, sensitive filenames, and file paths.
* It could also include source code that allows attackers to conduct a source code review on the application.
* Most systems aim to hide development information, including software version numbers and configuration files, from the outside world, because it allows attackers to gather information about an application and strategize about how to most effectively attack it.
* Typically, applications leak version numbers in HTTP response headers, HTTP response bodies, or other server responses.

### Prevention
* The most important measure you should take is to avoid hardcoding credentials and other sensitive information into executable code (Instead, you can place sensitive information in separate configuration files or a secret storage system like Vault)
* Remove data from services and server responses that reveal technical details about the backend server setup and software versions.
* Handle all exceptions by returning a generic error page to the user, instead of a technical page that reveals details about the error.

### Hunting for Information Disclosure
* A good starting point is to look for software version numbers and configuration information by using the recon techniques

1- Attempt a Path Traversal Attack
  * Start by trying a path traversal attack to read the server’s sensitive files
    
2- Search the Wayback Machine
  * Another way to find exposed files is by using the Wayback Machine.
  * To search for a domain’s files, visit *https://web.archive.org/web/*/DOMAIN*
  * Add a /* to this URL to get the archived URLs related to the domain as a list. For example, *https://web.archive.org/web/*/example.com/** will return a list of URLs related to *example.com*.
  * You can then use the search function to see whether any sensitive pages have been archived. For example, to look for admin pages, search for the term /admin in the found URLs
  * You can also search for backup files and configuration files by using common file extensions like .conf and .env, or look for source code, like JavaScript or PHP files, by using the file extensions .js and .php.
  * Download interesting archived pages and look for any sensitive info. For example, are there any hardcoded credentials that are still in use, or does the page leak any hidden endpoints

3- Search Paste Dump Sites
  * look into paste dump sites like Pastebin and GitHub gists
  * Pastebin has an API that allows users to search for public paste files by using a keyword, email, or domain name.
  * Tools like PasteHunter or pastebin-scraper can also automate the process. Pastebin-scraper (https://github.com/streaak/pastebin-scraper/) uses the Pastebin API to help you search for paste files.

    *./scrape.sh -g KEYWORD* - Will return a list of Pastebin file IDs associated with the specified KEYWORD.

    *pastebin.com/ID* - To access these Pastebins

4- Reconstruct Source Code from an Exposed .git Directory
  * Another way of finding sensitive files is to reconstruct source code from an exposed .git directory.
  * When a developer uses Git to version-control a project’s source code, Git will store all of the project’s version-control information, including the commit history of project files, in a Git directory
  * Normally, this .git folder shouldn’t be accessible to the public, but sometimes it’s accidentally made available. This is when information leaks happen.
  * Secret scanning tools like truffleHog (https://github.com/dxa4481/truffleHog/) or Gitleaks (https://github.com/zricethezav/gitleaks/) can be used to find sensitive data in the leak
  * To check if a .git folder is public:

    *https://example.com/.git*
    
  Three things could happen when you browse to the /.git directory. 
  
    - If you get a 404 error, this means the application’s .git directory isn’t made available to the public, and you won’t be able to leak information this way. 
    - If you get a403 error, the .git directory is available on the server, but you won’t be able to directly access the folder’s root
    - If you don’t get an error and the server responds with the directory listing of the .git directory, you can directly browse the folder’s contents and retrieve any information contained in it.

  If directory listing is enabled, you can browse through the files and retrieve the leaked information. Using *$ wget -r example.com/.git* you can download all the files

  If directory listing isn't enabled, first make sure the directory is available to the public by trying to access the config file  using *$ curl https://example.com/.git/config*

  If this file is accessible then you can reconstruct the .git folder
  
