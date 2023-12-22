# Details
* Name: Popcorn
* Difficulity: Medium
* Category: Linux

* *sudo nmap -sV -sC -oA nmap IPADDRESS*
* Add to hosts file.
* *dirb http://popcorn.htb -r -o FILENAME* - Check for files/links related to the link provided.
* Check the subdomains/output from dirb 
* searchsploit "APPNAME" - Finds exploits for the application name provided.
* searchsploit -x *EXPLOITNUMBER.txt* - Loads the exploit with the number provided.
* Run SqlMap in the background while working - sqlmap -r RESPONSEFILENAME --level 5 --risk 3
* Some systems validates file types using what's called magic bytes, which are the first few bytes used to identify a file type.
* Search for uploaded files directory using subdomains like, upload/uploads/etc..
* 
