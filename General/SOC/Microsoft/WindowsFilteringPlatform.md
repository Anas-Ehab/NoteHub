# Windows Filtering Platform
* https://learn.microsoft.com/en-us/windows/win32/fwp/windows-filtering-platform-start-page

## Introduction
* Windows Filtering Platform (WFP) is a set of API and system services that provide a platform for creating network filtering applications.
* The WFP API allows developers to write code that interacts with the packet processing that takes place at several layers in the networking stack of the operating system.
* Network data can be filtered and modified before it reaches its destination.
* With the WFP API, developers can implement firewalls, intrusion detection systems, antivirus programs, network monitoring tools, and parental controls.
* Windows Filtering Platform is a development platform and not a firewall itself.

### Objects

#### Filter 
* A rule that governs classification. If the conditions are met, the action is invoked.
* This is the most complex object exposed by WFP since it ties together all the other object types.

* Properties:
  - Array of conditions
  - Action (Permit, Block, Callout)
  - Weight
  - Context

* Examples
  -  "Block traffic with a TCP port greater than 1024."
  -  "Callout to IDS for all traffic that is not secured."

#### Callout	
* A set of functions that participate in the classification process.
* It allows for custom packet processing to be done when certain conditions are met.

* Properties:
  - ID
  - Applicable layer

* Example: The NAT driver

#### Layer	
* A filter container in the filter engine.
* Represents a specific point in network traffic processing where the filter engine is invoked.
* Properties:
  - Schema for filters that can be added to the layer
* Example: The Inbound Transport Layer
  
#### Sub-layer	
* A sub-component of a layer, used in filter arbitration.
* Properties:
  - Weight
* Example: The IPsec Tunnel sub-layer
  
#### Provider
* A policy provider that has built a solution on WFP.
* It is used solely for management; it does not affect run-time packet processing.
* Properties:
  - ID
  - Service name
* Examples:
  - Windows Firewall with Advanced Security
  - A 3rd-party URL filtering application

#### Provider Context
* A data blob used by a policy provider to store arbitrary context information.
* It is used to pass custom configuration information to a callout.
* The most common way to use the context information is to have filters reference a provider context.
* Properties:
  - ID
  - Data blob
* Example:
  - IPsec stores authentication settings in the Base Filtering Engine ( BFE). The "Context" property of a filter indicates the authentication settings to use for the traffic that the filter describes.
  - The SSL certification selection shim will store certification information in a provider context.

## Logs 
### Auditing
* Success Audit: The Windows Filtering Platform has allowed a connection
* Success Audit: The Windows Filtering Platform has permitted a bind to a local port
* Success Audit: The Windows Filtering Platform has permitted an application or service to listen on a port for incoming connections
* Failure Audit: The Windows Filtering Platform has blocked a connection
* Failure Audit: The Windows Filtering Platform blocked a packet

### Configuration
* Success Audit: A Windows Filtering Platform filter has been changed
* Success Audit: A Windows Filtering Platform callout has been changed
* Success Audit: A Windows Filtering Platform provider has been changed
* Success Audit: A Windows Filtering Platform sub-layer has been changed
* Success Audit: A Windows Filtering Platform provider context has been changed

### Misc.
* Success Audit: The following sub-layer was present when the Windows Filtering Platform Base Filtering Engine started
* Success Audit: The following provider was present when the Windows Filtering Platform Base Filtering Engine started
* Success Audit: The following filter was present when the Windows Filtering Platform Base Filtering Engine started
