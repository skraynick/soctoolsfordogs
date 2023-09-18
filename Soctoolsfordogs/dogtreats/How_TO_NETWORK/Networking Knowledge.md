
## Networking Basics ![[1.2_Bibliography#Networking Basics]]


### What do the different parts of an IP address mean?
[What is a Subnet](https://www.cloudflare.com/learning/network-layer/what-is-a-subnet/)
[Introduction to Subnetting](https://www.ittsystems.com/introduction-to-subnetting/)
Every IP address has two parts. The first part indicates which network the address belongs to. The second part specifies the device within that network. However, the length of the "first part" changes depending on the network's class.

Networks are categorized into different classes, labeled A through E. Class A networks can connect millions of devices. Class B networks and Class C networks are progressively smaller in size. (Class D and Class E networks are not commonly used.)

#### **Class A network:**
Everything before the first period indicates the network, and everything after it specifies the device within that network. Using 203.0.113.112 as an example, the network is indicated by "203" and the device by "0.113.112."

#### **Class B network:** 
Everything before the second period indicates the network. Again using 203.0.113.112 as an example, "203.0" indicates the network and "113.112" indicates the device within that network.

#### **Class C network:**
For Class C networks, everything before the third period indicates the network. Using the same example, "203.0.113" indicates the Class C network, and "112" indicates the device.

### Subnet Mask
A subnet mask is like an IP address, but for only internal usage within a network. Routers use subnet masks to route data packets to the right place. Subnet masks are not indicated within data packets traversing the Internet — those packets only indicate the destination IP address, which a router will match with a subnet.

#Networking 


## OSI Model ![[1.2_Bibliography#OSI_Model]]
#osi 
![[osi_model_7_layers.png]]

### The 7 layers of the OSI model
[7 Layers](https://www.networkworld.com/article/3239677/the-osi-model-explained-and-how-to-easily-remember-its-7-layers.html)

The layers are: Layer 1—Physical; Layer 2—Data Link; Layer 3—Network; Layer 4—Transport; Layer 5—Session; Layer 6—Presentation; Layer 7—Application.

It wasn’t always this way. Conceived in the 1970s when computer networking was taking off, two separate models were merged in 1983 and published in 1984 to create the OSI model that most people are familiar with today. Most descriptions of the OSI model go from top to bottom, with the numbers going from Layer 7 down to Layer 1. The layers, and what they represent, are as follows:

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAACXBIWXMAAA3XAAAN1wFCKJt4AAABWWlUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iWE1QIENvcmUgNS40LjAiPgogICA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPgogICAgICA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIgogICAgICAgICAgICB4bWxuczp0aWZmPSJodHRwOi8vbnMuYWRvYmUuY29tL3RpZmYvMS4wLyI+CiAgICAgICAgIDx0aWZmOk9yaWVudGF0aW9uPjE8L3RpZmY6T3JpZW50YXRpb24+CiAgICAgIDwvcmRmOkRlc2NyaXB0aW9uPgogICA8L3JkZjpSREY+CjwveDp4bXBtZXRhPgpMwidZAAABOklEQVQ4Ea2V3U7DMAxGV8QN3OyBB+oDdK/L75DKOV0cmdC0EizSp7iJfWwvbXaY5/mIJnUoA/s+7N6cfSKe+XgoD1/ML+gpANhdaN4zBr2iC5ruCuCT+RGdWHx2bRgGk/yCuuaePsX3hPmALq4tww1kFscbWqBuYldoYxujr8O5dpeh2eEHlIAMbmHVt62g77ikvbZZKmLqdLOTfSwsk49o96eJltuWItDTt3Kl7XCvtoldYyP5GnTEMQDv2MrhWq56HRZknKsDtlV9oBjam5XFexi8285kz9WNPP+95QaWXx+h7aF0X/61w8gwA/MBjDzH6a9DcchttrB6APHj4t/1yazlQ2fh/5+emQF5BXVhqbqtbq6XAyAv1zjN3S8A3wyNu5DlhTFZ3Rl59+3CNio1VsZZ4E3/Ar4BuSbVUBIuWisAAAAASUVORK5CYII=)

#### Layer 7 - Application

The Application Layer in the OSI model is the layer that is the “closest to the end user”. It receives information directly from users and displays incoming data to the user. Oddly enough, applications themselves do not reside at the application layer. Instead the layer facilitates communication through lower layers in order to establish connections with applications at the other end. Web browsers (Google Chrome, Firefox, Safari, etc.) TelNet, and FTP, are examples of communications  that rely  on Layer 7.

#### Layer 6 - Presentation

The Presentation Layer represents the area that is independent of data representation at the application layer. In general, it represents the preparation or translation of application format to network format, or from network formatting to application format. In other words, the layer “presents” data for the application or the network. A good example of this is encryption and decryption of data for secure transmission; this happens at Layer 6.

#### Layer 5 - Session

When two computers or other networked devices need to speak with one another, a session needs to be created, and this is done at the Session Layer**.** Functions at this layer involve setup, coordination (how long should a system wait for a response, for example) and termination between the applications at each end of the session.
#### Layer 4 – Transport

The Transport Layer deals with the coordination of the data transfer between end systems and hosts. How much data to send, at what rate, where it goes, etc. The best known example of the Transport Layer is the Transmission Control Protocol (TCP), which is built on top of the Internet Protocol (IP), commonly known as TCP/IP. TCP and UDP port numbers work at Layer 4, while IP addresses work at Layer 3, the Network Layer.

#### Layer 3 - Network

Here at the Network Layer is where you’ll find most of the router functionality that most networking professionals care about and love. In its most basic sense, this layer is responsible for packet forwarding, including routing through different routers. You might know that your Boston computer wants to connect to a server in California, but there are millions of different paths to take. Routers at this layer help do this efficiently.

#### Layer 2 – Data Link

The Data Link Layer provides node-to-node data transfer (between two directly connected nodes), and also handles error correction from the physical layer. Two sublayers exist here as well--the Media Access Control (MAC) layer and the Logical Link Control (LLC) layer. In the networking world, most switches operate at Layer 2. But it’s not that simple. Some switches also operate at Layer 3 in order to support virtual LANs that may span more than one switch subnet, which requires routing capabilities.

#### Layer 1 - Physical

At the bottom of our OSI model we have the Physical Layer, which represents the electrical and physical representation of the system. This can include everything from the cable type, radio frequency link (as in a Wi-Fi network), as well as the layout of pins, voltages, and other physical requirements. When a networking problem occurs, many networking pros go right to the physical layer to check that all of the cables are properly connected and that the power plug hasn’t been pulled from the router, switch or computer, for example.

## TCP 3-way Handshake Process
![[1.2_Bibliography#TCP 3-way Handshake]]
#3-way_handshake

![[TCP-connection-1.png]]

#### Step 1 (SYN):
In the first step, the client wants to establish a connection with a server, so it sends a segment with SYN(Synchronize Sequence Number) which informs the server that the client is likely to start communication and with what sequence number it starts segments with
#### Step 2 (SYN + ACK):
Server responds to the client request with SYN-ACK signal bits set. Acknowledgement(ACK) signifies the response of the segment it received and SYN signifies with what sequence number it is likely to start the segments with
#### Step 3 (ACK): 
In the final part client acknowledges the response of the server and they both establish a reliable connection with which they will start the actual data transfer