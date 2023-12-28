# Bastion (Continue)
* Link: https://app.hackthebox.com/machines/Bastion
* Type: Windows
* Difficulty: Easy

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *smbclient -L //IPADDRESS* - Sorts the shares in a windows machine. (Just nothing for the password to continue as gues
* *sudo mount -t cifs //IPADDRESS/SHARENAME OUTPUTDIR* - Mounts the share in the directory provided
* *smbmap -u ANYUSERNAME -H IPADDRESS* - If gues login is allowed then type anything in the username field, automated mapping of smb but creates a file so maybe banned in oscp?
* *du -hs FILENAME* - tells you the size of the file.
* *7z l FILENAME.vhd* - Lists the contents of the file provided.
* *guestmount --add DISKNAME.vhd --inspector --ro -v DIRECTORY* - Mounts the virtual disk
* *find DIR1 DIR2 DIR3 -ls* - Ls for multiple directories.
* *impacket -secretdump -sam SAMFILENAME -system SYSTEMFILENAME* dumbs the hashes from the SAM and SYSTEM files.
* *hashes.org* - to decrypt hashes.
* *net user USERNAME* - information about the user in windows.
* *impacket-psexec USERNAME@IPADDRESS* opens a powershell instance to a windows machine.
* *powershell* starts a powershell instance.

## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* There is ssh and smb but since ssh is more secure by default, then check the smb first.
* Check if eternal blue is applicable using nmap script.
* Check the shares.
* Access the share.
* Find a backup, download and examine it.
* Search for the SAM and SYSTEM files.
* Extract the hashes from the SAM and SYSTEM files.
* Decrypt the hashes.
* SSH using the password.
* Examine the logs, nothing there.
* Examine the applications, find *mremoteng*.
* Search online for the password. (In the config file in AppData/Roaming)
* Extract the encrypted password, find a tool to decrypt.
* Decrypt the password then login as admin.

## Notes
* *.vhd* files can be extracted using 7zip.
* In windows, SAM and SYSTEM in the directory *Windows/System32/config/* contains the hashes of the passwords of the users.
* *aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0* is the empty hash meaning that the account doesn't exit/password doesn't exist.
* C:\Logs\ is an important directory because it shows you the logs
* Check for C:\Program Files\ and C:\Program Files (x86)\ for programs in windows.
