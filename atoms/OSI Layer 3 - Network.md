### OSI Layer 3 - Network
**Routers | IP | Packets**
Routers move packets across networks. Defines the physical path.

#Q What is the responsibility of Layer 3?
It is responsible for the end-to-end delivery of data between devices on different network segments. This layer defines protocols for logical addressing, routing, and fragmentation of data packets to ensure that they are delivered to the correct destination across different networks

#Q What is the IP Packet Structure components?
![[Pasted image 20240217125807.png]]
- Source IP Address
- Destination IP Address
- Protocol => 
	- ICMP (Internet Control Message Protocol), 
	- TCP (Transmission Control Protocol), 
	- UDP (User Datagram Protocol) => Connectionless communication models used for performance sensitive applications such as VoIP, streaming media, online games etc. 
	- IGMP (Internet Group Management Protocol) => IP hosts report their multicast group memberships to any immediately neighboring multicast routers.
	- SCTP(Stream Control Transmission Protocol) => Transports PSTN (Public Switched Telephone Network) over IP networks. 
	- GRE (Generic Routing Encapsulation) => tunneling inside virtual point-to-point links 
	- ESP (Encapsulating Security Payload) and AH (Authentication Header) => IPsec for authentication, integrity, and confidentiality.
- TTL: Time-to-Live - max number of hops before it should be discarded.

#Q How do routers route?
A router has multiple interfaces. A route table contains a mapping of destination and next hops (target). When a packet arrives, the route table is used to send the packet to the mapped target.
The more specific prefixes are preferred e.g. 0.0.0.0/0 is least preferred and a /32 is most preferred.

![[Pasted image 20240217131754.png]]
In this example, the home router sends all it's routes to the ISP. The ISP has a router with a route table, the sends the packets to the next hop.
#Q How are encapsulated packets reach MAC addressable router?

Routing is a hop-by-hop protocol. 
Routers use [[BGP]] routes to learn about network info. When ISP router is forwarding at Layer 2. Destination [[MAC]] address of destination router is known via [[ARP]] - or Address Resolution Protocol.

#Q What are the limitation of Layer 3?
Layer 3 does not support channels, it is source to destination IP only.
Packets can be delivered out of order.
Packets can be dropped e.g. number of hops exceeded ([[TTL]])
No flow control - packets can be dropped if destination is over-whelmed