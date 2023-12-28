# CronOS
* Link: https://app.hackthebox.com/machines/Cronos
* Type: Linux
* Difficulty: Medium

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *nslookup* then *server IPADDRESS* then *IPADDRESS* then Enter.
* *nc -nlvp 4444* - Starts a listener.
* *searchsploit -m 50057* - Gets the PoC of a CVE.
* *sudo nano /etc/hosts* - Add *IPADDRESS* of target then the *DOMAIN*
* *host -l DOMAINNAME DNSSERVERADDRESS* - Performs zone transfer attack. When you find the other domains add them next to the first domain in the hosts file to be able to reach them.
* *python -m http.server PORTNUMBER* - Starts a simple HTTP server using Python (Can be used to upload files to the target system)
* *admin' #* - Basic SQL Injection.
* *& COMMAND* - OS Command Injection.
  
## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* Check open ports.
* Port 80 directs us to the default Apache login page, which means that there is some misconfiguration. In this case, do nslookup and find the domain name and add it in the hosts file.
* Do zone transfer to get the other domains/subdomains.
* Admin login page, try default creds, then try to do SQL Injection.
* A page that runs commands, try command injection.
* Get initial access, run LinEnum.sh to enum the environment.
* Find a script that runs every minute and the owner is root.
* Inject the script with your reverse shell.
* Get Root.

## Why is the machine vulnerable
* A security misconfiguration that allows SQL injection.
* A security misconfiguration in cron that had a scheduled cron job to run a non-privileged user owned file as root.
