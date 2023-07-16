# Chapter 1

### Terms

* **Networking model**: define structure/categories (layers) of standards and protocols - OSI, TCP/IP
* **Same-layer Interaction**: protocol defines a header for two computers to communicate with each other
* **Adjacent-layer interaction**: the layer below provides a service to the layer above on a single computer
* **De-capsulation**: remove headers/trailers around data (go up layers)
* **Encapsulation**: add headers/trailers around data (go down layers)
* **Protocol Data Unit (PDU)**: name for any layer in the OSI model - L#PDU (L#H = header, L#T = trailer)

### TCP/IP Model
* Application (data) - HTTP, POP3, SMTP
* Transport (segment) - TCP, UDP
* Network (packet) - IP, ICMP
* Data Link (frame) - Ethernet (802.3), 802.11 (Wi-Fi)
* Physical (bits) - Electricity? lol

<div style="text-align: center">
    <br>
    <img src="images/osi-tcpip.png" alt="OSI compared to TCP/IP">
    <p>OSI compared to TCP/IP and term of each layer</p>
    <br>
</div>

### Application Layer
<div style="text-align: center">
    <br>
    <img src="images/http.png" alt="HTTP GET request, HTTP reply and data only messages">
    <p>HTTP GET request, HTTP reply and data only messages</p>
    <br>
</div>

### Transport Layer
Same layer interaction - using TCP headers when Larry and Bob are communicating

Adjacent layer interaction - TCP is providing error checking to HTTP through sequence numbers

<div style="text-align: center">
    <br>
    <img src="images/tcp-seq.png" alt="TCP providing error recovery for HTTP - adjacent layer interaction">
    <p>TCP providing error recovery for HTTP</p>
    <br>
</div>

### Network Layer
<div style="text-align: center">
    <br>
    <img src="images/basic-routing.png" width="500px" alt="Basic Routing Example">
    <p>Basic Routing Example</p>
    <br>
</div>

### Data-Link Layer
<div style="text-align: center">
    <br>
    <img src="images/encapsulation-decapsulation.png" width="500px" alt="Using ethernet to forward an IP packet to R1">
    <p>Using Ethernet to forward IP packets</p>
    <br>
</div>

NOTE: Ethernet is depicted as lines here to show that there are other devices connected but aren't important

### Data Encapsulation

<div style="text-align: center">
    <br>
    <img src="images/data-encapsulation.png" width="500px" alt="TCP/IP Layers showing encapsulation">
    <p>TCP/IP Layers showing encapsulation</p>
    <br>
</div>