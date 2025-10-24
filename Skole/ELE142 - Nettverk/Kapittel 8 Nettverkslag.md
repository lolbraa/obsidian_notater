#Nettverk 

| #**Topic Title**                  | **Topic Objective**                                                                        |
| --------------------------------- | ------------------------------------------------------------------------------------------ |
| **Network Layer Characteristics** | Explain how the network layer uses IP protocols for reliable communications.               |
| **IPv4 Packet**                   | Explain the role of the major header fields in the IPv4 packet.                            |
| **IPv6 Packet**                   | Explain the role of the major header fields in the IPv6 packet.                            |
| **How a Host Routes**             | Explain how network devices use routing tables to direct packets to a destination network. |
| **Router Routing Tables**         | Explain the function of fields in the routing table of a router.                           |

# Network Layer Protocol, OSI Layer 3
![[Kapittel 8 Nettverkslag-1.jpg]]
![[Kapittel 8 Nettverkslag-1.png|500]]
> To accomplish end-to-end communications across network boundaries, network layer protocols perform four basic operations:
> - **Addressing end devices** - End devices must be configured with a unique IP address for identification on the network.
> - **Encapsulation -** The network layer encapsulates the protocol data unit (PDU) from the transport layer into a packet. The encapsulation process adds IP header information, such as the IP address of the source (sending) and destination (receiving) hosts. The encapsulation process is performed by the source of the IP packet.
> - **Routing -** The network layer provides services to direct the packets to a destination host on another network. To travel to other networks, the packet must be processed by a router. The role of the router is to select the best path and direct packets toward the destination host in a process known as routing. A packet may cross many routers before reaching the destination host. Each router a packet crosses to reach the destination host is called a hop.
> - **De-encapsulation -** When the packet arrives at the network layer of the destination host, the host checks the IP header of the packet. If the destination IP address within the header matches its own IP address, the IP header is removed from the packet. After the packet is de-encapsulated by the network layer, the resulting Layer 4 PDU is passed up to the appropriate service at the transport layer. The de-encapsulation process is performed by the destination host of the IP packet.
## Characteristics of IP
IP was designed as a protocol with low overhead. It provides only the functions that are necessary to deliver a packet from a source to a destination over an interconnected system of networks. The protocol was not designed to track and manage the flow of packets. These functions, if required, are performed by other protocols at other layers, primarily TCP at Layer 4.

These are the basic characteristics of IP:
- **Connectionless** - There is no connection with the destination established before sending data packets.
- **Best Effort** - IP is inherently unreliable because packet delivery is not guaranteed.
- **Media Independent** - Operation is independent of the medium (i.e., copper, fiber-optic, or wireless) carrying the data.


# IPv4
![[Kapittel 8 Nettverkslag-2.png]]
> Significant fields in the IPv4 header include the following:
> - **Version -** Contains a 4-bit binary value set to 0100 that identifies this as an IPv4 packet.
> - **Differentiated Services or DiffServ (DS) -** Formerly called the type of service (ToS) field, the DS field is an 8-bit field used to determine the priority of each packet. The six most significant bits of the DiffServ field are the differentiated services code point (DSCP) bits and the last two bits are the explicit congestion notification (ECN) bits.
> - **Time to Live (TTL) –** TTL contains an 8-bit binary value that is used to limit the lifetime of a packet. The source device of the IPv4 packet sets the initial TTL value. It is decreased by one each time the packet is processed by a router. If the TTL field decrements to zero, the router discards the packet and sends an Internet Control Message Protocol (ICMP) Time Exceeded message to the source IP address. Because the router decrements the TTL of each packet, the router must also recalculate the Header Checksum.
> - **Protocol –** This field is used to identify the next level protocol. This 8-bit binary value indicates the data payload type that the packet is carrying, which enables the network layer to pass the data to the appropriate upper-layer protocol. Common values include ICMP (1), TCP (6), and UDP (17).
> - **Header Checksum –** This is used to detect corruption in the IPv4 header.
> - **Source IPv4 Address –** This contains a 32-bit binary value that represents the source IPv4 address of the packet. The source IPv4 address is always a unicast address.
> - **Destination IPv4 Address –** This contains a 32-bit binary value that represents the destination IPv4 address of the packet. The destination IPv4 address is a unicast, multicast, or broadcast address.
The two most commonly referenced fields are the source and destination IP addresses. 


# IPv6
Improvements that IPv6 provides include the following:
- **Increased address space** - IPv6 addresses are based on 128-bit hierarchical addressing as opposed to IPv4 with 32 bits.
- **Improved packet handling** - The IPv6 header has been simplified with fewer fields.
- **Eliminates the need for NAT** - With such a large number of public IPv6 addresses, NAT between a private IPv4 address and a public IPv4 is not needed. This avoids some of the NAT-induced problems experienced by applications that require end-to-end connectivity.

![[Kapittel 8 Nettverkslag-3.png]]
>The fields in the IPv6 packet header include the following:
> - **Version -** This field contains a 4-bit binary value set to 0110 that identifies this as an IP version 6 packet.
> - **Traffic Class -** This 8-bit field is equivalent to the IPv4 Differentiated Services (DS) field.
> - **Flow Label -** This 20-bit field suggests that all packets with the same flow label receive the same type of handling by routers.
> - **Payload Length -** This 16-bit field indicates the length of the data portion or payload of the IPv6 packet. This does not include the length of the IPv6 header, which is a fixed 40-byte header.
> - **Next Header -** This 8-bit field is equivalent to the IPv4 Protocol field. It indicates the data payload type that the packet is carrying, enabling the network layer to pass the data to the appropriate upper-layer protocol.
> - **Hop Limit** - This 8-bit field replaces the IPv4 TTL field. This value is decremented by a value of 1 by each router that forwards the packet. When the counter reaches 0, the packet is discarded, and an ICMPv6 Time Exceeded message is forwarded to the sending host,. This indicates that the packet did not reach its destination because the hop limit was exceeded. Unlike IPv4, IPv6 does not include an IPv6 Header Checksum, because this function is performed at both the lower and upper layers. This means the checksum does not need to be recalculated by each router when it decrements the Hop Limit field, which also improves network performance.
> - **Source IPv6 Address -** This 128-bit field identifies the IPv6 address of the sending host.
> - **Destination IPv6 Address -** This 128-bit field identifies the IPv6 address of the receiving host.


# Routing
Alle enheter har en (host) Routing Table for hvor pakker skal sendes.

Another role of the network layer is to direct packets between hosts. A host can send a packet to the following:
- **Itself** - A host can ping itself by sending a packet to a special IPv4 address of 127.0.0.1 or an IPv6 address ::1, which is referred to as the loopback interface. Pinging the loopback interface tests the TCP/IP protocol stack on the host.
- **Local host** - This is a destination host that is on the same local network as the sending host. The source and destination hosts share the same network address.
- **Remote host** - This is a destination host on a remote network. The source and destination hosts do not share the same network address.

## Default gateway
Having a default gateway configured creates a default route in the routing table of the PC. A default route is the route or pathway your computer will take when it tries to contact a remote network.

### IP Router Routing Table
The routing table of the router contains network route entries listing all the possible known network destinations.

The routing table stores three types of route entries:
- **Directly-connected networks -** These network route entries are active router interfaces. Routers add a directly connected route when an interface is configured with an IP address and is activated. Each router interface is connected to a different network segment. In the figure, the directly-connected networks in the R1 IPv4 routing table would be 192.168.10.0/24 and 209.165.200.224/30.
- **Remote networks -** These network route entries are connected to other routers. Routers learn about remote networks either by being explicitly configured by an administrator or by exchanging route information using a dynamic routing protocol. In the figure, the remote network in the R1 IPv4 routing table would be 10.1.1.0/24.
- **Default route** – Like a host, most routers also include a default route entry, a gateway of last resort. The default route is used when there is no better (longer) match in the IP routing table. In the figure, the R1 IPv4 routing table would most likely include a default route to forward all packets to router R2.

### Static Routing
Static routes are route entries that are manually configured. The figure shows an example of a static route that was manually configured on router R1. The static route includes the remote network address and the IP address of the next hop router.
![[Kapittel 8 Nettverkslag-4.png]]

### Dynamic Routing
A dynamic routing protocol allows the routers to automatically learn about remote networks, including a default route, from other routers. Routers that use dynamic routing protocols automatically share routing information with other routers and compensate for any topology changes without involving the network administrator. If there is a change in the network topology, routers share this information using the dynamic routing protocol and automatically update their routing tables.

Dynamic routing protocols include OSPF and Enhanced Interior Gateway Routing Protocol (EIGRP). The figure shows an example of routers R1 and R2 automatically sharing network information using the routing protocol OSPF.