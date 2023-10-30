# SQL Injection
* SQL injection (SQLi) is a web application injection vulnerability that occurs when an attacker injects malicious SQL statements into an application's input fields.
* Types:
  - In-Band SQLi (Most Popular)
    * In-band SQL injection is the most common type of SQL injection attack. It occurs when an attacker uses the same communication channel to send the attack and receive the results.
    * In other words, the attacker injects malicious SQL code into the web application and receives the results of the attack through the same channel used to submit the code.
    * There are 2 types
      * Error Based
        1. In error-based SQL injection, the attacker injects SQL code that causes the web application to generate an error message.
        2. The error message can contain valuable information about the database schema or the contents of the database itself, which the attacker can use to further exploit the vulnerability. 
         
      * Union Based SQLi
        1.  In union-based SQL injection, the attacker uses the UNION operator to combine the results of two or more SQL queries into a single result set.
        2.  By manipulating the injected SQL code, the attacker can extract data from the database that they are not authorized to access

  - Blind SQLi (Most Popular)
    * Blind SQL Injection is a type of SQL Injection attack where an attacker can exploit a vulnerability in a web application that does not directly reveal information about the database or the results of the injected SQL query.
    *  The attacker injects malicious SQL code into the application's input field, but the application does not return any useful information or error messages to the attacker in the response.
      
    * Boolean Based SQLi
        1.  In this type of attack, the attacker exploits the application's response to boolean conditions to infer information about the database.
        2.  The attacker sends a malicious SQL query to the application and evaluates the response based on whether the query executed successfully or failed. 

    * Time-Based SQLi
        1.  In this type of attack, the attacker exploits the application's response time to infer information about the database.
        2.  The attacker sends a malicious SQL query to the application and measures the time it takes for the application to respond. 

  - Out-of-Band SQLi
    * The least common type of SQL injection attack. It involves an attacker exploiting a vulnerability in a web application to extract data from a database using a different channel, other than the web application itself.

* Types of Databases:
  - Relational Databases - A database that organizes data into one or more tables or relations, where each table represents an entity or a concept, and the columns of the table represent the attributes of that entity or concept.
  - NoSQL Databases - A type of database that does not use the traditional tabular relations used in relational databases. Instead, NoSQL databases use a variety of data models to store and access data.
  - Object-oriented Databases - A database that stores data as objects rather than in tables, allowing for more complex data structures and relationships.

## Hunting for SQLi
* Identify an injection point that interacts with the database (i.e. login form & search boxes)
* Probe the input field with special characters.
* Input fields aren't just input forms, URL parameters, hidden fields, and cookies are all also injection points.
* For Manual testing try injecting a malicious code (i.e. special characters, *-- # ' "*) and look for unexpected behaviour or any indication (i.e. errors) that the input is being handled through the database.
* There are integer-based injection parameters and string-based injection parameters.
  - For integer-based, the expected data is of type integer.
  - As for string-based, the expected data is of type string.
  - Payloads for each is different. For example, for an integer-based parameter, the payload can be something like, *AND 1* or *1\*56*. As for string-based payloads, it will look something like, *' - False* or *`" - True*.

* Every DBMS responds to errors differently try to find out the DBMS based on the error received because every DBMS has its own payload lists.
* Try URL Encoding.
* To Check with OWASP ZAP
  - Add the link to your default context and then do a spider and then an active scan. (Can be also utilized in a general vulnerability scan)
  - Locate the request where injection can occur.
  - Locate the injection point.
  - Send the request to the fuzzer and add the injection point as a fuzz point.
  - Go to file fuzzers --> jbrofuzz --> SQL Injection and then select all the lists.
  - Check for reflected state. (It will contain lots of false positive but check them 1 by 1)

## Exploiting SQLi
* 
