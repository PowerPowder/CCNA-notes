# Chapter 5

## Terms
* **Broadcast frame**: frame sent to FFFF.FFFF.FFFF, deliver to all hosts on LAN
* **Known unicast frame**: frame's dest MAC address is listed in a switch and sent out of it's corresponding port
* **Spanning Tree Protocol**: protocol that dynamically blocks ports for traffic on switches/bridges to prevent loops
* **Unknown unicast frame**: frame not in a switch's MAC address table, switch must flood to learn that device's MAC
* **MAC address table**: dynamic list of MACs on switch that listens and decides destination of incoming frames
* **Forward**: receive a frame from one port and send it to another port.
* **Flood**: forwards frames out all interfaces except receiving interface for broadcast, unknown unicast and multicast frames

## Features of Switches

Primary features of LAN switches:
* make decisions to forward or filter frames
* learn mac addresses
* implement and maintain STP

Ports are named based on their fasted speed and are autonegotiated, i.e. 10/100/1000Mbps is Gigabit Ethernet.

Switches forward frames within VLANs, frame received from a port in VLAN 1 only is forwarded to ports on VLAN 1.

Switches act like a host for IP, they need a defalt gateway.

Reset config of switch:
```
erase startup-config
delete vlan.dat
reload
hostname SW1
```

## Switch Concepts - Forwarding, Learning, Flooding

**Campus-lan**: end-user devices connect to lan switches

**Data center**: servers and switches in a closed room that connect to the campus-lan

Actions performed by switches:
1. Decide when to forward or filter a frame based of destination MAC address.
2. Prepare to forward by examining the source mac address of each frame received (learning).
3. Only forward one copy of the frame to the destination by using Spanning Tree Protocol (STP) to prevent loops.

If a switch receives a known unicast frame and is meant to be sent from the same interface it was received from, then the switch ignores the frame.

<!-- <div style="text-align: center">
    <img src="images/switch-forwarding.png" width="500px" alt="Sample switch forwarding and filtering decision">
    <p>Sample switch forwarding and filtering decision</p>
</div> -->

<div style="text-align: center">
    <br>
    <img src="images/switch-forwarding-2.png" width="500px" alt="Forwarding decision with two switches">
    <p>Forwarding known unicast frames between two switches</p>
</div>

<div style="text-align: center">
    <br>
    <img src="images/empty-address-table.png" width="500px" alt="Switch learning: empty table and adding two entries">
    <p>Switch learning MAC addresses from frames sent between Fred and Barney (learns from source MAC)</p>
</div>

<div style="text-align: center">
    <br>
    <img src="images/switch-flooding.png" width="500px" alt="Switch flooding: unknown unicast arrives, floods out other ports">
    <p>Switch flooding LAN - unknown unicast arrives, floods out other ports</p>
</div>

Switch floods all ports except for receiving port, the device with the requested MAC replies, the switch learns the device's MAC address. This applies to unknown unicast and broadcast frames.

## Spanning Tree Protocol (STP)

Without STP, flooded frames would loop infinitely in Ethernet networks with redundant links.

STP causes each port on a switch to be in blocking (can't forward) or forwarding (can forward) states, so **only one active logical path exists between any device**.

<div style="text-align: center">
    <img src="images/stp-example.png" width="500px" alt="Network with redundant links but without STP (frame loops forever)">
    <p>Network with redundant links, no STP (frame loops forever both directions)</p>
</div>

## MAC Address Tables

`show mac address-table dynamic` lists the MAC address table of a switch.

`show interfaces status` lists all ports and their connection status.

`show interfaces f0/1 counters` lists total amount of incoming and outgoing frames.

Filter entres in the MAC address table by:
* MAC address - `show mac address-table dynamic address 0200.1111.1111`
* Switch port - `show mac address-table dynamic interface fastEthernet 0/1`
* VLAN - `show mac-address table dynamic vlan 1`

## Aging Time and Clearing MAC Address Table

Entries are removed if not used for 'x' number of seconds (default is 300 seconds), oldest entries are removed when switch runs out of memory.

Aging time can be overridden by assigning a port to a specific VLAN.

`show mac address-table aging-time` lists the global and each per-VLAN override aging time.

`show mac address-table count` lists the amount of dynamic and static MAC address entries.

**CAM (Content-addressable memory)**: fast table lookup capabilities, where MAC table entries are stored.

`clear mac address-table dynamic` - enable mode command, can add `vlan x`, `interface x` or `address x`