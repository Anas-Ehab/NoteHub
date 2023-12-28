# Enumuration

## nmap
* *sudo nmap -sC -sV -O -oA \<Output Directory\> \<IP Address\>* - Basic nmap scan for the top ports only. (-sC for default scripts, -sV for version enum, -O for OS enum)
* *sudo nmap -sC -sV -O -p- -oA \<Output Directory\> \<IP Address\>* - Scan for all the ports.
