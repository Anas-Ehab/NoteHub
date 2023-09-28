**It's a free course on YouTube that covers Bug Bounty from Zero to Hero**
https://www.youtube.com/watch?v=Rp69edBmFFo

# General Tips

## Choosing a Program
* Check the programs by newest first as the newer the program the less tested it is.
* Before going through a program, make sure that its scope is large enough.
* Try to focus on things that are familiar to you because you will konw how things work.
* Pick a program that you are interested in to make you more motivated and interested in the program.
* It's easier to find bugs in unpaid programs as most hackers go for paid programs so as a beginner it might be a good start to focus on unpaid programs

# Recon

## Tools
* Nmap - a tool that's used to discover hosts and services on a network - https://nmap.org/ - Really Useful
* Fuff - a tool that's used to fuzz websites - https://github.com/ffuf/ffuf - Really Useful
* Dirb - a tool that's used to fuzz websites - similar to fuff but more basic
* Shodan - a tool/website that scans all the devices that are connected to the internet and save data about them - https://www.shodan.io/ - Most featuers are paid and the data provided can be accquired using other free tools (Good for when scanning is not allowed as it doesn't actually scan it just retrieves data)
* Hurricane Electric BGP Toolkit - a website that's similar to Shodan but slower - https://bgp.he.net/
* Wappalyzer - a plugin that shows you the technologies used by a specific website - https://www.wappalyzer.com/
 


## Commands Cheatsheet

## Tips
* Try to find the developers of the program you are testing and follow them on social media and github as they usually would post their about what they are working on and they even might post the code into GitHub
* After each recon session make sure to document what you did (ie the tools and commands used) this will ensure that you have a reference to look back into and know where you stopped
* There are many bug bounty checklists which are files that include steps to go through when doing bug bounty an example: https://github.com/sehno/Bug-bounty/blob/master/bugbounty_checklist.md
* Make sure that the subdomains are under scope before trying to breach them
* When searching for subdomains check for dev subdomains these usually include useful information about the application and sometimes code updates are published there before being published to the public
* If you find a URL as a parameter check for CSRF
* If you find an id then try to perform session hijacking by changing the number of the id/session

## Extra

