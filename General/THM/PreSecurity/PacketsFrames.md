# Packets and Frames
* Packets and frames are small pieces of data that, when forming together, make a larger piece of information or message. However, they are two different things in the OSI model.
* A frame is at layer 2 - the data link layer, meaning there is no such information as IP addresses.
* Packets are an efficient way of communicating data across networked devices.
* Because this data is exchanged in small pieces, there is less chance of bottlenecking occurring across a network than large messages being sent at once.
* Packets have different structures that are dependant upon the type of packet that is being sent.
* For example a packet using the internet protocol will have the following headers:
  - Time to Live: This field sets an expiry timer for the packet to not clog up your network if it never manages to reach a host or escape!
  - Checksum: This field provides integrity checking for protocols such as TCP/IP. If any data is changed, this value will be different from what was expected and therefore corrupt.
  - Source Address: The IP address of the device that the packet is being sent from so that data knows where to return to.
  - Destination Address: The device's IP address the packet is being sent to so that data knows where to travel next.

# TCP/IP Protocol
