# Chapter 5

three primary features of LAN switches:
make decisins to forward/filter frames
learn mac addresses
STP

**switches act like a host in regards to IP - needs a default gateway**

do switches fload unknown multicast frames?

does the default gateway need to be manually configured on a switch?

does a switch send out the same unicast frame to all ports that have the same destination mac address?

## LAN Switching Concepts

campus-lan: end-user devices connect to lan switches
data center: servers and switches in a closed room that connect to the campus-lan

### Overview of switching logic

purpose of a lan switch - forward frames to the  correct destination (mac) address.

actions performed by switches:
1. decide when to forward or filter a frame based of destination MAC address.
2. prepare to forward by examining the source mac address of each frame received (learning).
3. only forward one copy of the frame to the destination by using Spanning Tree Protocol (STP) to prevent loops.

### Forwarding known unicast frames

<div style="text-align: center">
    <img src="images/switch-forwarding.png" width="500px" alt="Sample switch forwarding and filtering decision">
    <p>Sample switch forwarding and filtering decision</p>
</div>

<div style="text-align: center">
    <br>
    <img src="images/switch-forwarding-2.png" width="500px" alt="Forwarding decision with two switches">
    <p>Forwarding decision with two switches</p>
</div>

**Unicast frames (unicasts)**: frames that have a known destination (unicast) MAC address in a switch's MAC address table.

### Learning MAC Addresses

<div style="text-align: center">
    <img src="images/empty-address-table.png" width="500px" alt="Switch learning: empty table and adding two entries">
    <p>Switch learning: empty table and adding two entries (ignoring forwaring process)</p>
</div>

### Flooding unknown unicast and broadcast frames

**Unknown unicast frame (unknown unicast)**: an unknown unicast MAC address sent to a switch.

Switch forwards copies of the frame out all ports except for the incoming port.

The device with the requested MAC address will send a reply, the switch learns that device's MAC address.

<div style="text-align: center">
    <img src="images/switch-flooding.png" width="500px" alt="Switch flooding: unknown unicast arrives, floods out other ports">
    <p>Switch flooding: unknown unicast arrives, floods out other ports</p>
</div>

### Avoiding Loops Using Spanning Tree Protocol

without stp, flooded frames would loop infinitely in Ethernet networks with redundant links.

stp blocks some ports from sending frames, so only one active logical path exists between any device.

<div style="text-align: center">
    <img src="images/stp-example.png" width="500px" alt="Network with redundant links but without STP (frame loops forever)">
    <p>Network with redundant links, no STP (frame loops forever both directions)</p>
</div>

STP causes each port on a switch to be in blocking (can't forward) or forwarding (can forward) states.

### LAN Switching Summary