# Cross Site Scripting (XSS)
* Cross site scripting (XSS) is a client-side web vulnerability that allows an attacker to inject malicious scripts into web pages.
* 2 Types
  - Stored/Persistent
    1. When an attacker can inject javascript code into the web application's database or the source code of the web page and anyone who visits the web page will be affected.
    2. Check any input field that's persistent (Comment/Post) and try to inject code into it.
    3. If you can inject code then it's vulnerable and everyone who visits the page will be affected by the code.

  - Reflected
    1. It's the tricking of a target into clicking a specially crafted link with an XSS payload.
    2. Check any input field and try to inject code into it.
    3. If the input is added to the URL then it's reflected not stored.
    4. If you can inject code then it's vulnerable.

  - DOM-Based XSS (Type 0 XSS)
    1. It is a type of XSS vulnerability that allows an attacker to inject malicious payloads into a webpage by exploiting a weakness in the DOM of the web application.

* XSSer
  - A tool that automates XSS injection
  - *xsser --url URL -p PAYLOADXSS --Fp "SCRIPT" --auto* (Add XSS to the part to be injected)
  - *xsser --gtk* (GUI of xsser)
