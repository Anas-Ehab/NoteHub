# Starting Point
## Commands
* *sudo nmap -sV IPADDRESS*: Scans the IP address for open ports and gives information about the version.
* *sudo nmap -p- -sV*: Scans the IP address for *all* open ports and gives information about the version.
* *sudo nmap -p- --min-rate=1000 -sV IPADDRESS*: *min-rate* is used to speed up the scan as the number goes higher the faster it works.
* *https://www.speedguide.net/port.php?port=#*: A website that provides information about the provided port.
* *gobuster dir -w /usr/share/wordlists/dirb/common.txt -u IPADDRESS/URL*: Used to enumrate directories and files.
* *telnet IPADDRESS* is used to connect through telnet.
* *ftp IPADDRESS* is used to connect through ftp.
* *smbclient -L IPADDRESS* can be used to list the shares that exist on the provided IP address.
* *redis-cli -h IPADDRESS* is the command used to connect to a redis db.
* *xfreerdp /v:IPADDRESS* is the command to open a RDP session.
* *gobuster dir -x EXTENSION -w WORDLIST -u IPADDRESS/URL* is used to enumrate dirs and files extension is optional.
* *mongo mongodb://IPADDRESS:PORT* is the command used to connect to a mongodb.
* *rsync --list-only IPADDRESS::* is used to show the list of shares avaliable.


  
## Appointment
* Telnet (TCP Port 23): it is a client/server application protocol that provides access to virtual terminals of remote systems on local area networks or the Internet.
* Sometimes, due to configuration mistakes, some important accounts can be left with blank passwords for the sake of accessibility (i.e. root/admin/etc..)
* *telnet IPADDRESS* is the command used to connect through telnet.

## Sequel
* File Transfer Protocol (FTP) (TCP Port 21 & 22): it is a network protocol for transmitting files between computers over Transmission Control Protocol/Internet Protocol (TCP/IP)
* *anonymous* user can be used to log in to FTP when you don't have an account.
* *ftp IPADDRESS* is the command used to connect through ftp.
* 230 Code is received when the login is successful.
* *dir* / *ls* are 2 commands that can be used to list files when connected to an ftp session.
* *get FILENAME* is the command used to download files when connected to an ftp session.

## Crocodile
* Server Message Block (SMB) (TCP Port 445: it is a network file sharing protocol that allows applications on a computer to read and write to files and to request services from server programs in a computer network.
* *smbclient* can be used to create a SMB session.
* *smbclient -L IPADDRESS* can be used to list the shares that exist on the provided IP address.
* *smbclient \\\\IPADDRESS\\SHARENAME* is used to connect to a share.
* *get FILENAME* is the command used to download files when connected to a SMB session.

## Responder
* Redis (TCP Port 6379) is an open-source in-memory storage, used as a distributed, in-memory key–value database.
* *redis-cli -h IPADDRESS* is the command used to connect to a redis db.
* Once connected to the session *info* command is used to obtain the information and statistics about the Redis server.
* *Keyspace* section provides information about the databases.
* *SELECT #* is used to select a specific database.
* *keys\** can be used to get all the keys in the database.
* *get KEY* is used to get the value.

## Three
* Remote Desktop Protocol (RDP) (TCP Port 3389): it is a protocol, or technical standard, for using a desktop computer remotely.
* *xfreerdp2-x11* is a free tool that allows RDP sessions.
* *xfreerdp /v:IPADDRESS* is the command to open a RDP session.
* *xfreerdp /v:IPADDRESS /cert:ignore /u:USERNAME*

## Ignition
* Hyper Text Transfer Protocol (HTTP) (TCP 80): it is a protocol for fetching resources such as HTML documents. It is the foundation of any data exchange on the Web
* Nginx: it is a web server that can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache.
* *gobuster* is a tool that's used to enumrate directories and endpoints.
* *gobuster dir -x EXTENSION -w WORDLIST -u IPADDRESS/URL*

## Bike
* MongoDB (TCP 27017): it is a source-available cross-platform document-oriented database program. Classified as a NoSQL database program.
* *mongo mongodb://IPADDRESS:PORT* is the command used to connect to a mongodb.
* *show* is used to list items (i.e. *show dbs* or *show collections*)
* *use DB* is used to choose a DB.
* *db.COLLECTION.find().pretty()* is used to show the item in a pretty mode.

## Funnel
* Rsync (TCP 873): it is a fast and extraordinarily versatile file copying tool. It can copy locally, to/from another host over any remote shell, or to/from a remote rsync daemon.
* *rsync --list-only IPADDRESS::* is used to show the list of shares avaliable.
* *rsync --list-only IPADDRESS::SHARENAME* is used to list files in the share.

## Pennyworth
* Rsync (TCP 873): it is a fast and extraordinarily versatile file copying tool. It can copy locally, to/from another host over any remote shell, or to/from a remote rsync daemon.
* *rsync --list-only IPADDRESS::* is used to show the list of shares avaliable.
* *rsync --list-only IPADDRESS::SHARENAME* is used to list files in the share.
* *rsync IPADDRESS::SHARENAME/FILENAME DEST* is used to get a file.

## Tactics
* Rsync (TCP 873): it is a fast and extraordinarily versatile file copying tool. It can copy locally, to/from another host over any remote shell, or to/from a remote rsync daemon.
* *rsync --list-only IPADDRESS::* is used to show the list of shares avaliable.
* *rsync --list-only IPADDRESS::SHARENAME* is used to list files in the share.
* *rsync IPADDRESS::SHARENAME/FILENAME DEST* is used to get a file.
