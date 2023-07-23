# Chapter 3

### Terms

**Leased line**: company using line does not own it, they pay a monthly lease fee to use it (level 1 service)

**Wide-Area Network (WAN)**: communicate over a long distance, router to router

**Telco**: telephone company

**Serial interface**: used by routers to connect to serial lines

**HDLC**

**Ethernet over MPLS**

**Ethernet Line Service (E-Line)**

**Default router (Default Gateway)**

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
* Leased-line WAN links are full duplex crossover links (eg. pins 1,2 -> 3,6)
* Managed by telcos - large network of cables and specialised switching devices
* Leased-lines are old, slower and take longer to install than Ethernet WAN links, Ethernet WAN links have been replacing them
* Protocols - HDLC & Point-to-Point (PPP)
* **High-level Data Link Control (HDLC)**: proprietary Cisco HDLC (adds type field), like Ethernet, creates WAN link
    * Fields:
        * Flag - pattern to signify new frame incoming
        * Address - destination device
        * Control - not used anymore
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

## IP

### Routing

### Addressing

### Routing Protocols

### Other Protocols