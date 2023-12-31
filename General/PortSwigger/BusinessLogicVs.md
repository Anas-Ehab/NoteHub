# Business Logic Vulnerabilities
* Business logic vulnerabilities are flaws in the design and implementation of an application that allow an attacker to elicit unintended behavior.
* In this context, the term "business logic" simply refers to the set of rules that define how the application operates. As these rules aren't always directly related to a business, the associated vulnerabilities are also known as "application logic vulnerabilities" or simply "logic flaws".
* Logic-based vulnerabilities can be extremely diverse and are often unique to the application and its specific functionality.
* Business logic vulnerabilities often arise because the design and development teams make flawed assumptions about how users will interact with the application.
* The impact of business logic vulnerabilities can, at times, be fairly trivial. It is a broad category and the impact is highly variable. However, any unintended behavior can potentially lead to high-severity attacks if an attacker is able to manipulate the application in the right way.


## Examples of Business Logic Vulnerabilities:
* Excessive trust in client-side controls:
  - A fundamentally flawed assumption is that users will only interact with the application via the provided web interface.
  - This is especially dangerous because it leads to the further assumption that client-side validation will prevent users from supplying malicious input. However, an attacker can simply use tools such as Burp Proxy to tamper with the data after it has been sent by the browser but before it is passed into the server-side logic.
  - This effectively renders the client-side controls useless.
    
* Failing to handle unconventional input:
  - One aim of the application logic is to restrict user input to values that adhere to the business rules.
  - 
* Making flawed assumptions about user behavior
* Domain-specific flaws
* Providing an encryption oracle


## How to Prevent
* Make sure developers and testers understand the domain that the application serves.
* Avoid making implicit assumptions about user behavior or the behavior of other parts of the application.
* Best practices for the development team:
  - Maintain clear design documents and data flows for all transactions and workflows, noting any assumptions that are made at each stage.
  - Write code as clearly as possible. If it's difficult to understand what is supposed to happen, it will be difficult to spot any logic flaws. Ideally, well-written code shouldn't need documentation to understand it. In unavoidably complex cases, producing clear documentation is crucial to ensure that other developers and testers know what assumptions are being made and exactly what the expected behavior is.
  - Note any references to other code that uses each component. Think about any side-effects of these dependencies if a malicious party were to manipulate them in an unusual way.
