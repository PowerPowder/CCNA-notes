# Chapter 2

### Terms

* **Ethernet**
* **IEEE**
* **WLAN**
* **Ethernet frame**
* **10BASE-T**
* **100BASE-T**
* **1000BASE-T**
* **Fast Ethernet**
* **Gigabit Ethernet**
* **Ethernet link**
* **RJ-45**
* **Ethernet port**
* **NIC**
* **Straight-through cable**
* **Crossover cable**
* **Ethernet address**
* **MAC address**
* **Unicast address**
* **Broadcast address**
* **Frame Check Sequence**
* **Transceiver**
* **Multimode (MM)**
* **Single-mode (SM)**
* **Electromagnetic Interference (EMI)**
* **Core**
* **Cladding**
* **Fibre-optic cable**

<div style="text-align: center">
    <br>
    <img src="images/enterprise-lan.png" width="500px" alt="Single-building enterprise wired and wireless LAN">
    <p>Single-building enterprise wired and wireless LAN</p>
    <br>
</div>

| Speed | Common Name | Informal IEEE<br>Standard Name | Formal IEEE<br>Standard Name | Cable Type,<br>Maximum Length |
| --- | --- | --- | --- | --- |
| 10 Mbps | Ethernet | 10BASE-T | 802.3 | Copper, 100m |
| 100 Mbps | Fast Ethernet | 100BASE-T | 802.3u | Copper, 100m |
| 1000 Mbps | Gigabit Ethernet | 1000BASE-LX | 802.3z | Fibre, 5000m |
| 1000 Mbps | Gigabit Ethernet | 1000BASE-T | 802.3ab | Copper, 100m |
| 10 Gbps | 10 Gig Ethernet | 10GBASE-T | 802.3an | Copper, 100m |

Ethernet frames use the same format for the header and trailer no matter the speed or type of cable (UTP/fibre optic).

**Ethernet is a standard not a specific cable**

UTP cables are twisted to prevent EMI (crosstalk - EMI from a wire to another wire in the same cable).

SFP (Small Form Factor Pluggable): on switch ports where you decide what interface you want - SFP is like USB-C and the SFP modules are the adapters/dongles.

<div style="text-align: center">
    <br>
    <img src="images/straight-through-cable.png" width="500px" alt="10BASE-T and 100BASE-T Straight-Through Cable Pinout">
    <p>10BASE-T/100BASE-T Straight-Through Cable Pinout - 1 & 2 Transmit, 3 & 6 Receive</p>
    <br>
</div>

<div style="text-align: center">
    <br>
    <img src="images/crossover-cable.png" width="450px" alt="Crossover Ethernet Cable">
    <p>Crossover Ethernet Cable</p>
    <br>
</div>

| Transmits on Pins 1 & 2 | Transmits on Pins 3 & 6 |
| --- | --- |
| PC NICs | Hubs |
| Routers | Switches |
| Wireless access point | - |

1000BASE-T uses 1,2 & 3,6 and 4,5 & 7,8 - with a crossover cable 1,2 and 3,6 are swapped, 4,5 and 7,8 are swapped.

Cisco switches have *auto-mdix* which if the wrong cable is used, it changes it's logic to make the link work.