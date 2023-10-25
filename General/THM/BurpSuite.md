# Burp Suite The Basics
* Burp Suite captures and enables manipulation of all the HTTP/HTTPS traffic between a browser and a web server.
* Features:
  - Proxy: It enables interception and modification of requests and responses while interacting with web applications.
  - Repeater: Allows for capturing, modifying, and resending the same request multiple times.
  - Intruder: Allows for spraying endpoints with requests. It is commonly utilized for brute-force attacks or fuzzing endpoints.
  - Decoder: It can decode captured information or encode payloads before sending them to the target.
  - Comparer: Enables the comparison of two pieces of data at either the word or byte level.
  - Sequencer: Employed when assessing the randomness of tokens, such as session cookie values or other supposedly randomly generated data.
* Shortcuts: ![image](https://github.com/Anas-Ehab/NotesHub/assets/55194408/5b7cdccd-aeb5-453f-95af-7bd312078f36)
* You can intercept the response that's coming back from the server.
* Target Tab:
  - Site map: Allows us to map out the web applications we are targeting in a tree structure. Every page that we visit while the proxy is active will be displayed on the site map. 
  - Issue definitions: An extensive list of web vulnerabilities, complete with descriptions and references.
  - Scope Settings: This setting allows us to control the target scope in Burp Suite.
* Scoping: By setting a scope for the project, we can define what gets proxied and logged in Burp Suite. We can restrict Burp Suite to target only the specific web application(s) we want to test. 
