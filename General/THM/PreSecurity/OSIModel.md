# OSI Model
* The OSI model (or Open Systems Interconnection Model) is a fundamental model used in networking.
* This critical model provides a framework dictating how all networked devices will send, receive and interpret data.
* The OSI model consists of seven layers. Each layer has a different set of responsibilities and is arranged from Layer 7 to Layer 1.
* (P)lease (D)o (N)to (T)hrow (S)ausage (P)izza (A)way
  
# Application Layer (Layer 7)
* It's the layer that users interact with the most.
* Everyday applications such as email clients, browsers, or file server browsing software such as FileZilla provide a friendly, Graphical User Interface (GUI) for users to interact with data sent or received.

# Presentation Layer (Layer 6)
* This layer acts as a translator for data to and from the application layer (layer 7).
* The receiving computer will also understand data sent to a computer in one format destined for in another format.
* Security features such as data encryption/decryption (like HTTPS when visiting a secure site) occur at this layer.

# Session Layer (Layer 5)
* Once data has been correctly translated or formatted from the presentation layer (layer 6), the session layer (layer 5) will begin to create a connection to the other computer that the data is destined for.
* The session layer (layer 5) synchronises the two computers to ensure that they are on the same page before data is sent and received.
* Once these checks are in place, the session layer will begin to divide up the data sent into smaller chunks of data and begin to send these chunks (packets) one at a time.
* Sessions are unique — meaning that data cannot travel over different sessions, but in fact, only across each session instead.

# Transport Layer (Layer 4)
* Layer 4 of the OSI model plays a vital part in transmitting data across a network.
* It follows one of two different protocols that are decided based upon several factors:
  - TCP
  - UDP

## Transmission Control Protocol (TCP)
* This protocol is designed with reliability and guarantee in mind.
* This protocol reserves a constant connection between the two devices for the amount of time it takes for the data to be sent and received.
* Not only this, but TCP incorporates error checking into its design. Error checking is how TCP can guarantee that data sent from the small chunks in the session layer (layer 5) has then been received and reassembled in the same order.
* TCP is used for situations such as file sharing, internet browsing or sending an email. This usage is because these services require the data to be accurate and complete.
  
### Advantages:
* Guarantees the accuracy of data.
* Capable of synchronising two devices to prevent each other from being flooded with data.
* Performs a lot more processes for reliability.

### Disadvantages:
* Requires a reliable connection between the two devices. If one small chunk of data is not received, then the entire chunk of data cannot be used.
* A slow connection can bottleneck another device as the connection will be reserved on the receiving computer the whole time.
* TCP is significantly slower than UDP because more work has to be done by the devices using this protocol.

## User Datagram Protocol (UDP)
* Any data that gets sent via UDP is sent to the computer whether it gets there or not.
* There is no synchronisation between the two devices or guarantee.

### Advantages:
* UDP is much faster than TCP.
* UDP leaves the application layer (user software) to decide if there is any control over how quickly packets are sent.
* UDP does not reserve a continuous connection on a device as TCP does.
* UDP is useful in situations where there are small pieces of data being sent. For example, protocols used for discovering devices or larger files such as video streaming (where it is okay if some part of the video is pixelated)
  
### Disadvantages:
* UDP doesn't care if the data is received.
* Unstable connections result in a terrible experience for the user.

# Network Layer (Layer 3)
* The third layer of the OSI model (network layer) is where the magic of routing & re-assembly of data takes place (from these small chunks to the larger chunk).
* Firstly, routing simply determines the most optimal path in which these chunks of data should be sent.
* Some routing protocols are,
  - Open Shortest Path First (OSPF)
  - Routing Information Protocol (RIP)
* The factors that decide what route is taken is decided by the following:
  - What path is the shortest? I.e. has the least amount of devices that the packet needs to travel across.
  - What path is the most reliable? I.e. have packets been lost on that path before?
  - Which path has the faster physical connection? I.e. is one path using a copper connection (slower) or a fibre (considerably faster)?
* At this layer, everything is dealt with via IP addresses such as 192.168.1.100.
* Devices such as routers capable of delivering packets using IP addresses are known as Layer 3 devices.

# Data Link Layer (Layer 2)
* The data link layer focuses on the physical addressing of the transmission. It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical MAC (Media Access Control) address of the receiving endpoint.
* MAC addresses are set by the manufacturer and literally burnt into the card; they can't be changed -- although they can be spoofed.
* When information is sent across a network, it's actually the physical address that is used to identify where exactly to send the information.
* Additionally, it's also the job of the data link layer to present the data in a format suitable for transmission.

# Physical Layer (Layer 1)
* Put simply, this layer references the physical components of the hardware used in networking and is the lowest layer that you will find.
* Devices use electrical signals to transfer data between each other in a binary numbering system (1's and 0's).
