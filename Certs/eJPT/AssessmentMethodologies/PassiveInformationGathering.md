# Passive Information Gathering

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
