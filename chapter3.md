# Chapter 3

### Terms

**Leased line**: company using line does not own it, they pay a monthly lease fee to use it (level 1 service)

**Wide-Area Network (WAN)**: communicate over a long distance, router to router

**Telco**: telephone company

**Serial interface**: used by routers to connect to serial lines

**HDLC**

**Ethernet over MPLS (Multiprotocol Label Switching)**: technology used to create Ethernet service for customer

**Ethernet Line Service (E-Line)**: term from the Metro Ethernet Forum for point-to-point Ethernet WAN

**Default router (Default Gateway)**: The nearest router on a LAN to a host ()

**Routing table**

**IP network**

**IP subnet**

**IP packet**

**Routing protocol**

**Dotted-Decimal Notation (DDN)**

**IPv4 address**

**Unicast address**

**Subnetting**

**Hostname**

**DNS**

**ARP**

**Ping**

Two WAN links: Serial links and Ethernet WAN links

Data link protocols control the correct delivery of data over a physical link of a certain type.

## Leased-Line WANs
* Routers connect LAN to the WAN and have a WAN link to other routers.
* Leased-line WAN links are full duplex crossover links (eg. pins 1,2 -> 3,6) and installed in most buildings
* Managed by telcos - large network of cables and specialised switching devices
* Leased-lines are old, slower and take longer to install than Ethernet WAN links, Ethernet WAN links have been replacing them
* Protocols - HDLC & Point-to-Point (PPP)
* **High-level Data Link Control (HDLC)**: proprietary Cisco HDLC (adds type field), like Ethernet, creates WAN link
    * Fields:
        * Flag - pattern to signify new frame incoming
        * Address - destination device
        * Control (not used anymore)
        * Type - type of L3 packet in frame
        * FCS - used for error detection

<div style="text-align: center">
    <br>
    <img src="images/routers-encap-decap.png" width="600px" alt="Routers encapsulating and decapsulating IP packets">
    <p>Routers encapsulating and decapsulating IP packets</p>
    <br>
</div>

## Ethernet WANs

Ethernet WAN links use the same data-link protocols as ethernet LANs but add additional features to make them work over longer distances.

<div style="text-align: center">
    <br>
    <img src="images/sp-wan.png" width="500px" alt="Fibre Ethernet link to connect a CPE router to a SP's WAN">
    <p>Fibre Ethernet link to connect a CPE router to a SP's WAN</p>
    <p>CPE is Customer Premises Equipment, PoP is point of presence</p>
    <br>
</div>

**Ethernet emulation**: link is not a literal Ethernet link from one end to the other

Ethernet WAN links use the same protocols as Ethernet LAN links.

**EoMPLS WAN allows routers to send Ethernet frames over link and look like an ethernet link to the customer?**

## IP

### Routing

Routers & end-user computers are known as **hosts** in TCP/IP.

Every router has an **IP routing table**, these tables list IP address groupings (IP networks and IP subnets).

**ARP (Address Resolution Protocol)**: dynamically learns the data-link address of an IP host connected to a LAN.

<div style="text-align: center">
    <br>
    <img src="images/ip-routing.png" width="500px" alt="Network layer and Data-link layer encapsulation">
    <p>Network layer and Data-link layer encapsulation (the cloud signifies Ethernet WAN link)</p>
    <br>
</div>

Routing steps:
1. Check FCS to ensure frame has no errors, discard frame if there are errors.
2. Discard old data-link header and trailer.
3. Compare IP packet's destination IP address to routing table, find route to hop to next.
4. Encapsulate IP packet inside new data-link header and trailer, add destination MAC address of next hop host or router in frame header, then forward the frame.

### Addressing

Any interface that expects to receive IP packets needs an IP address.

**IP subnet (or IP network)**: groups of IP addresses used on the same physical network.

IP addresses not separated by a router are in same subnet, separated by a router then they are in different subnets.

<div style="text-align: center">
    <br>
    <img src="images/ipv4-header.png" width="500px" alt="IPv4 Header, 20 bytes in total">
    <p>IPv4 Header, 20 bytes in total</p>
    <br>
</div>

### Routing Protocols

Routers learn routes for each subnet it connects to and adds it to it's routing table.

How routers learn routes (using routing protocol):
1. Each router adds a route to its IP routing table for each subnet it connects to.
2. Each router tells its neighbours about routes in its IP routing table, including learned routes from other routers.
3. After learning a new route from a neighbour, it adds route to its IP routing table, typically the next hop on that route is that neighbour.

When a router is connected to a subnet, it adds that subnet into it's IP routing table without using routing protocol.

**Routing update**: a routing protocol message sent to another router to learn about a subnet.

## Other Protocols