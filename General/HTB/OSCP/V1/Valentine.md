# Valentine
* Link: https://app.hackthebox.com/machines/Valentine
* Type: Linux
* Difficulty: Medium

## Commands Used
* *nmap -sC -sV -oA OUTPUTDIR IPADDRESS* - Nmap scan.
* *nmap --script vuln IPADDRESS* - Nmap scan that runs vulnerability scripts.
* *sslyize IPADDRESS* - analyze the SSL certificate of a website.
* *sslyize --heartbleed IPADDRESS* checks if the provided IP address is vulnerable to heartbleed or not.
* *chmod 600 KEYFILENAME* - Makes a SSH key useable.
* *ssh -i KEYFILENAME.KEY USERNAME@IPADDRESS* - SSH connection using the key and the username.
* *ssh -oPubkeyAcceptedAlgorithms=+ssh-rsa -i KEYFILENAME.KEY USERNAME@IPADDRESS* - 
* *ps -ef | grep ROOT* - shows the processes running by root.
* *groups* tells you what group your user has.
* *tmux -S TMUXSESSIONNAME* - hops into the tmux session specified.
* *grep gcc FILENAME.c* - display the compiling info for the C file.
* *echo BASE64ENCODEDSTRING | base64 --decode*
  
## Steps
* Start by checking the open ports using nmap (nmap -sC -sV -oA DIR IPADDRESS)
* Check open ports.
* Check the website
* There is a photo of a heart with blood (reference to Heartbleed bug)
* Get PoC.
* Check */dev/* directory.
* Find the key in hexadecimal, convert the hexadecimal to normal ASCII and save the key.
* *The naming convention of SSH keys is USERNAME_KEY* so we know the key belongs to which user.
* Use the hearbleed bug to get the base64 encoded password or the user.
* Using the key and password login to the user.
* Use LinPeas
* Provides 2 methods to privilege escalate. The first one is hijacking the Tmux session, the second one is using the dirty cow.

## Why is the machine vulnerable
* Unpatched/updated system
* Heartbleed
* Dirty Cow
* An open TMUX session that belongs to root.
