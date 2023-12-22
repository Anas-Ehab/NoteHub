# Path Traversal (Directory Traversal)
* This vulnerability enables an attacker to read arbitrary files on the server that is running an application.
* The sequence ../ is valid within a file path, and means to step up one level in the directory structure.
* Files to check for in Linux: */etc/passwd*
* On Windows, both *../* and *..\* are valid directory traversal sequences.
* Files to check for in Windows: *\windows\win.ini*
  
## Example:
* Imagine a shopping application that displays images of items for sale. This might load an image using the following HTML: *img src="/loadImage?filename=218.png"*
* The loadImage URL takes a filename parameter and returns the contents of the specified file. The image files are stored on disk in the location /var/www/images/.
* Using *https://insecure-website.com/loadImage?filename=../../../etc/passwd* will provide an attacker with the passwd file.

## How to prevent
* The most effective way to prevent path traversal vulnerabilities is to avoid passing user-supplied input to filesystem APIs altogether.
* Validate the user input before processing it. Ideally, compare the user input with a whitelist of permitted values. If that isn't possible, verify that the input contains only permitted content, such as alphanumeric characters only.
* After validating the supplied input, append the input to the base directory and use a platform filesystem API to canonicalize the path. Verify that the canonicalized path starts with the expected base directory.
