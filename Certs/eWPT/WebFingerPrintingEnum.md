# Web Fingerprinting and Enumeration 

## Passive Information Gathering

* *host URL* - Provides the IP Address of the website. (If you see 2 IP addresses you can assume that the website is hosted behind a proxy/firewall)
* *URL/robots.txt* - Provides a list of the sites that aren't indexed.
* *URL/sitemap.xml* or *WEBADDRESS/sitemaps.xml* or *WEBADDRESS/sitemap_index.xml* - An XML file that's used to provide search engines of an organized way to present the website
* [BuiltWith](https://builtwith.com/) - A tool that tells you what technologies the site is built with.
* [Wappalyzer](https://www.wappalyzer.com/) - A tool that tells you what technologies the site is built with.
* *whatweb URL* - Provides an overview of the technologies on the URL.
* [Httrack](https://www.httrack.com/) - A tool that's available for both Linux and Windows that allows you to copy a whole website (Can be useful when you want to analyze the source code).
* *whois URL* - Provides information about the registry of the URL. (Sometimes you can find email addresses or names of the registerer)
* [WhoIs](https://who.is/) - Provides information about the registry of the URL. (Sometimes you can find email addresses or names of the registerer)
* [Netcraft](https://sitereport.netcraft.com/) - Find out the infrastructure and technologies used by any site.
* *dnsrecon URL* - Provides data about the URL. (i.e. nameserver, A records, AAAA records, Email server)
* [DNSdumpster](https://dnsdumpster.com/) - Similar to *dnsrecon* but in a more organized way.
* *wafw00f URL -a* - Checks if the site is behind a WAF or not and if it's behind a WAF it provides you with the type of WAF. (-a to test for all types)
* [Sublist3r](https://github.com/aboul3la/Sublist3r) - Finds the subdomains of a specific domain. (*sublist3r -d URL/DOMAIN*)
* [Wayback Machine](https://archive.org/web/) - Provides snapshots of websites.
* Metasploit auxiliary *scanner/http/http_version* - Provides the version of the system

* Google Dorks
  - *site:URL* - Limits the results to the specified URL.
  - *inurl:admin* - Limits the results to sites with *admin* in the URL.
  - *site:\*.URL* - Show subdomains of the specified URL.
  - *intitle:admin* - Shows results with admin in the title.
  - *filetype:pdf - Shows results with pdf file type.
  - intitle:index of - Shows results with directory listing.
  - *cache:URL* - Shows cached versions of the specified URL.
  - *inurl:auth_user_file.txt* - Usually a file that contains a list of authorized users.
  - *inurl:passwd.txt* - Usually a file that contains a list of passwords.

* [Google Hacking Database](https://www.exploit-db.com/google-hacking-database) - List of improtant Google Dorks.
* *theHarvester -d URL* - Finds email addresses & subdomains & IP addresses.
* [Have I Been Pwned](https://haveibeenpwned.com/) - Contains Information about data breaches 


## Active Information Gathering
* *dnsenum URL* - Perform DNS transfer & DNS bruteforce.
* *dnsrecon -d URL* - General Enumration of the DNS records.
* *dig axfr @NAMESERVER DOMAIN* - Perform DNS transfer & DNS bruteforce.
* *fierce -dns DOMAIN - Perform DNS transfer & DNS bruteforce.
* *sudo netdiscover -i INTERFACE -r NETWORK ADDRESS/NETMASK* - Ping sweep to check for active hosts in the network.
* *fierce --domain URL --subdomain-file WORDLIST* - Does subdomain enumration.
* *nikto -h URL* - Scans a URL and provides some insights
* *nikto -h URL -Tuning # -Display V* - Tries some exploits based on the number given.
* *nikto -h URL -Tuning # -Display V -o FILENAME.html -Format html* - Saves the output to FILENAME.
* *dirb URL/IPADDRESS* - Finds directories for the provided URL/IP Address (Make sure to add http(s):// to the URL)
* *gobuster dir -u URL -w WORDLIST -b 403,404 -r* - Perform directory scanning (-b to hide 404 and 403) (-r to follow redirects) (Make sure to add http(s) to the url)
* *gobuster dir -u URL -w WORDLIST -b 403,404 -x .php,.xml,.txt -r* - Perform directory scanning (-x to specify the file type)
* You can perform directory scanning using burpsuite intruder by requesting a variable and utilizing a wordlist.
* You can also use ZAProxy by doing manual/active scanning.
* Burpsuite live passive crawl (Dashboard) can be used to have a good image of the website and the URLs it contains.

### Amass
[Amass](https://github.com/owasp-amass/amass) - Tool to automate the enumrating process.

* *amass enum -d URL* - Finds subdomains.
* *amass enum -brute -d URL* - Do a bruteforce to find the subdomains.
* *amass enum -o FILENAME -d URL* - Saves the output to the file specified.
  
### Nmap
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

### Curl Commands
* *curl -X GET URL* - Gets the specified URL.
* *curl -I URL* - Gets the header of the specified URL.
* *curl -X OPTIONS URL* - Tells you what methods are allowed for the specific URL.
* *curl -X POST URL -d "VARIABLE=VALUE&VARIABLE2=VALUE -v* - Sends a post request that takes 2 variables.
* *curl URL --upload-file FILENAME* - Uploads file to the specified path.
