# Linux Privilege Escalation (Free Course)

## Linux Enumeration

### Automated Tools
* [LinPeas](https://github.com/carlospolop/PEASS-ng/)
* [LinEnum](https://github.com/rebootuser/LinEnum)
* [Linux Exploit Suggester](https://github.com/The-Z-Labs/linux-exploit-suggester)
* [Linux Priv Checker](https://github.com/sleventyeleven/linuxprivchecker)

* Run more than one tool, start with *LinPeas* then run the others as sometimes one tool might miss something but the other will get it.

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
* *cat /etc/passwd* - Display the list of users. (Not all of them are real users)
* *cat /etc/passwd | cut -d : -f 1* - Shows the users only (Enhanced view over the above one)
* *cat /etc/shadow* - Important file that contains the passwords of the users.
* *cat /etc/group* - Shows the groups in the system.
* *history* - Check for the command history of the user.
* *sudo su -* - Tries to switch to a superuser.

* *Most important information is, what can you run as sudo, what are your commands history, and if you can switch into root.*

### Network Enumeration
* *ifconfig* - Shows your network interfaces and your IP address.
* *ip a* - Shows your network interfaces and your IP address.
* *ip route* - Shows the network routes.
* *arp -a* - Shows you the arp entities.
* *ip neigh* - Shows you the arp entities.
* *netstat -ano* - Shows you the open ports and the established connections.

### Password Hunting
* *grep --color=auto -rnw '/' -ie "PASSWORD=" --color=always 2> /dev/null* - Searches for "password" with colors.
* *locate password | more* - Searches for files named password. (Use *passwd*/*pass*/etc..)
* *find / -name id_rsa 2> /dev/null* - Searches for SSH keys.
