# Active Information Gathering
* *dnsenum URL* - Perform DNS transfer & DNS bruteforce.
* *dig axfr @NAMESERVER DOMAIN* - Perform DNS transfer & DNS bruteforce.
* *fierce -dns DOMAIN - Perform DNS transfer & DNS bruteforce.
* *sudo netdiscover -i INTERFACE -r NETWORK ADDRESS/NETMASK* - Ping sweep to check for active hosts in the network.

## Nmap
* *sudo nmap OPTIONS NETWORKADDRESS/NETMASK OR IP*
* Options:
  - *-Pn* Assumes the target is up already and skips the ping packets (Use most of the time).
  - *-sn* Performs a ping sweep to check for the active hosts.
  - *-p-* Scans the entire range of ports.
  - *-sU* Scans UDP ports.
  - *-F*  Fast scan on the most popular 100 ports.
  - *-sV* Scan with version detection.
  - *-O*  Scan with OS detection.
  - *-sC* Runs various scripts to find extra information.
  - *-T* Controls the speed of the scan 0 and 1 are for IDS evasion, default mode is 3, 4 and 5 sacrifice accuracy for speed.
  - *-oN FILENAME* Save the output into a file.
  - *-oX FILENAME* Save the output into an XML file.
