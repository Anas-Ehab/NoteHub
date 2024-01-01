# Solidstate
* Link: https://app.hackthebox.com/machines/solidstate
* Type: Linux
* Difficulty: Medium

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *searchsploit Apache James Server 2.3.2* - Search for CVEs for adobe coldfusion.
* *nc -nlvp 4444* - Starts a listener.
* *searchsploit -m NUMBER* - Gets the PoC of a CVE.
* *LinPEAS* - Gets an updated xls file with vulnerabilities.
* *pspy* - Provides a list of running processes without having to be root.
* *python -m SimpleHTTPServer PORTNUMBER* - Starts a simple HTTP server using python (Can be used to upload files to target system)
* *nc 10.10.10.51 4555* - connects to the provided IP address through the provided port number.
* *telnet 10.10.10.51 110* - Connect to the provided IP address through the provided port nubmer.
  - USER USERNAME
  - PASS PASSWORD
  - LIST
  - RETR EMAILID
  
## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* There is ssh which is safe by default
* http which we do further enumration (dir busting,etc..) on but we find nothing
* a port for *James server* and specifically for administration.
* Search for exploits for the James server.
* Find an exploit that gives us RCE but it's authenticated so we need to find a user.
* Try default username and password for the James server admin.
* Logged in using default password (*root/root*) (*nc 10.10.10.51 4555*)
* Find list of users.
* Change the password of the users and login to their email accounts try to find senstive information.
* Found the SSH password for one of the users
* Login using the SSH credentials found get RCE through the previous exploit (*telnet 10.10.10.51 110*).
* Run LinEnum to find exploits to get priv esc.
* Nothing on LinEnum, run pspy to know the running processes (Check if the system is x64 or x32 first and run the appropirate exe)
* Find a process that's run by root but has read and write access for all users.
* Add the reverse shell into the file being ran by root.
* Wait a minute for the file to run again by root.
* Get back a reverse shell.

## Why is the machine vulnerable
* The Machine is not patched/updated.
* There is security misconfiguration such that, root is running a script that's read/write by all users.
