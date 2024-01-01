# Linux Privilege Escalation (Free Course)

## Linux Enumeration

### System Enumeration
* *hostname* - Provides the hostname of the device.
* *uname -a* - Provides you with the kernel and version (Useful to look for exploits)
* *cat /proc/version* - Provides you with the kernel and version (Similar to uname)
* *cat /etc/issue* - Provides you with the distribution.
* *lscpu* - Provides you with the architecture of the machine.
* *ps aux* - Provides the list of services running

* *Most important information is what kernel are we on, does it has any vulnerabilities, and what architecture is the machine to know what exploits we can run.*

### Username Enumeration
* *whoami* - Shows you what user you are.
* *id* - Shows you what your id is.
* *sudo -l* - Shows you what commands you can run as *sudo* with no password.
* 
