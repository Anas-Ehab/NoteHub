# File Upload Vulnerability
* File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size.
* There are 3 ways a server handles file uploads:
  - If this file type is non-executable, such as an image or a static HTML page, the server may just send the file's contents to the client in an HTTP response.
  - If the file type is executable, such as a PHP file, and the server is configured to execute files of this type, it will assign variables based on the headers and parameters in the HTTP request before running the script. The resulting output may then be sent to the client in an HTTP response.
  - If the file type is executable, but the server is not configured to execute files of this type, it will generally respond with an error. However, in some cases, the contents of the file may still be served to the client as plain text.
* The Content-Type response header may provide clues as to what kind of file the server thinks it has served.
* A web shell is a malicious script that enables an attacker to execute arbitrary commands on a remote web server simply by sending HTTP requests to the right endpoint.
* From a security perspective, the worst possible scenario is when a website allows you to upload server-side scripts, such as PHP, Java, or Python files, and is also configured to execute them as code.



## Testing File Upload:
* 

## How to Prevent
* 
