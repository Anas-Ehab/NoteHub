# Web Service Security Testing
* Web services are software components designed to facilitate communication and data exchange between different applications or systems over the internet.
* Web services are a broad category of technologies and protocols designed to facilitate communication and data exchange between different software systems over the internet. They are meant to provide a standardized way for various applications, often on different platforms and using different programming languages, to interact with each other.
* APIs (Application Programming Interfaces), on the other hand, refer to a set of rules, protocols, and tools that allow different software applications to communicate with each other. They provide access to the functionality or data of an application or service for developers to use in their own applications.

## Web Services Implementation
* SOAP (Simple Object Access Protocol):
  - SOAP is a protocol for exchanging structured information in the implementation of web services.
  - SOAP-based web services use XML as their message format.
* JSON-RPC and XML-RPC: JSON-RPC and XML-RPC:
  - Lightweight protocols for remote procedure calls (RPC) using JSON or XML, respectively (Simpler than SOAP)
* REST (Representational State Transfer):
  - REST is an architectural style for designing networked applications, and it uses HTTP as its communication protocol.

## Web Services Definition Language (WSDL)
* WSDL is an XML-based language used to describe the functionality and interface of a web service.
* WSDL documents serve as contracts between service providers and consumers, specifying how a web service can be used.
* WSDL is commonly used in conjunction with SOAP (Simple Object Access Protocol) to define and document SOAP-based web services.
* 2 main versions: 1.1 and 2.0
* 2 definitions:
  - Abstract: Describes what the service does, such as the operation provided, the input, the output and the fault messages used by each operation
  - Concrete: Adds information about how the web service communicates and where the functionality is offered

### Components:
* Types: The <types> section defines the data types used in the web service. It typically includes XML Schema Definitions (XSD) that specify the structure and constraints of input and output data.
* Message: The <message> element defines the data structures used in the messages exchanged between the client and the service. Messages can have multiple parts, each with a name and a type definition referencing the types defined in the <types> section.
* Port Type: The <portType> element describes the operations that the web service supports. Each operation corresponds to a method or function that a client can invoke. It specifies the input and output messages for each operation.
  - Instead of portType, WSDL v. 2.0 uses interface elements which define a set of operations representing an interaction between the client and the service. Each operation specifies the types of messages that the service can send or receive.
  - Unlike the old portType, interface elements do not point to messages anymore (it does not exist in v. 2.0). Instead, they point to the schema elements contained within the types element.

* Binding: The <binding> element specifies how the service operations are bound to a particular protocol, such as SOAP over HTTP. It defines details like the protocol, message encoding, and endpoint addresses.
* Service: The <service> element provides information about the service itself. It includes the service's name and its endpoint address, which is the URL where clients can access the service.

### Testing 
* Identify the web services.
* Try to find the WSDL file. (append *?wsdl* or *.wsdl* or *?disco* at the end of the endpoint)
* Invoke hidden methods.
* Try to bypass body restrictions.
* Test for injection vulnerabilities.
