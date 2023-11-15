# Chapter 9

## Terms

* **blocking state**: 
* **BPDU guard**: 
* **bridge ID**: 
* **bridge protocol data unit (BPDU)**: 
* **designated port**: 
* **EtherChannel**: 
* **forward delay**: 
* **forwarding state**: 
* **Hello BPDU**: 
* **learning state**: 
* **listening state**: 
* **MaxAge**: 
* **PortFast**: 
* **root port**: 
* **root switch**: 
* **root cost**: 
* **Spanning Tree Protocol (STP)**: 
* **Rapid STP (RSTP)**: 
* **alternate port**: 
* **backup port**: 
* **disabled port**: 
* **discarding state**: 

## STP and RSTP Basics

* STP/RSTP prevents looping frames by adding an additional check on each interface before a switch uses it to send or receive user traffic.
    * Forwarding mode: use port in a VLAN as usual
    * Block mode: block all sending/receiving on the port
* Broadcast storm - any Ethernet frame loops around a LAN indefinitely, saturating the LAN with copies of itself

### The Need for Spanning Tree

### What Spanning Tree Does

* Problems caused if STP/RSTP is not used:
    1. Broadcast storms - frame forwarded repeatedly on same links
    2. MAC table instability - table is continuously updated with incorrect entries
    3. Multiple frame transmission - host receives multiple copies of a frame

<div style="text-align: center">
    <img src="images/stp.png" width="500px" alt="">
    <p>STP/RSTP blocking a port to stop networking loops</p>
</div>

### How Spanning Tree Works

* Putting interfaces in forwarding state:
    * Root port is selected
    * Ports on each switch have a root cost, lowest root cost is the root port
    * Switch and switch port with the lowest root cost is the designated switch/port
* Reasons for forwarding/blocking:
| Characterisation of Port | STP State | Description |
| --- | --- | --- |
| All the root switch's ports | Forwarding | Root switch is designated switch |
| Each nonroot switch's root port | Forwarding | Lowest root cost port to root switch |
| Each LAN's designated port | Forwarding | Switch forwarding the Hello with lowest root<br>cost is designated switch |
| All other working ports | Blocking | Port cannot forward/receive user frames |

#### The STP Bridge ID and Hello BPDU

* Hello BPDU (bridge protocol data unit) is used to exchange info with other switches and has fields:
    * Root bridge ID 
    * Sender's bridge ID 
    * Sender's root cost 
    * Timer values on root switch - Hello, MaxAge, forward delay timers

#### Electing the Root Switch

* Root selection:
    1. Lowest priority BID
    2. If that ties then lowest switch MAC address

#### Choosing Each Switch's Root Port

<div style="text-align: center">
    <img src="images/calculating-cost.png" width="600px" alt="">
    <p>Calculating total cost from SW3 to the root - smallest one is used</p>
</div>

* If a tie occurs then choose the lowest neighbour's: BID -> port priority -> port number

#### Choosing the Designated Port on Each LAN Segment

* Only SW3's Gi0/2 port is blocked, all other interfaces are forwarding
* Switch ports connected to endpoints are designated ports

### Configuring to Influence the STP Topology

* The priority can be changed per switch to influence the choices of STP/RSTP
* Port cost can be changed per port, per VLAN

| Ethernet Speed | IEEE Cost: 1998 & Before | IEEE Cost: 2004 & After |
| --- | --- | --- |
| 10 Mbps | 100 | 2,000,000 |
| 100 Mbps | 19 | 200,000 |
| 1 Gbps | 4 | 20,000 |
| 10 Gbps | 2 | 2,000 |
| 100 Gbps | N/A | 200 |
| 1 Tbps | N/A | 20 |

* Cost defaults is based on operating speed of link (**10**/100/1000 -> 100 cost)
* Use `spanning-tree pathcost method long` to use the right side of the table

## Details Specific to STP (not RSTP)

### STP Activity When the Network Remains Stable

1. Root switch sends a new Hello BDPU (root cost 0) out working interfaces every 2 seconds (by default)
2. Nonroot switch receives, adds it's BID as sender's BID and switch's root cost, forwards Hello out all designated ports
3. Repeat 1 & 2 until something changes

### STP Timers That Manage STP Convergence

| Timer | Default Value | Description |
| --- | --- | --- |
| Hello | 2 seconds | Time between Hellos created by root |
| MaxAge | 10 times Hello | Wait time after not hearing Hellos |
| Forward delay | 15 seconds | Time after changing from blocking to forwarding |

### Changing Interface States with STP

* roles: root port, designated port
* states: forwarding, blocking
* changing blocked to forwarding ports are put through two extra states (both timers are forward delay):
    1. Listening - does not forward, removes unused MAC table entries
    2. Learning - does not forward, learns MAC addresses received on interface
* blocking -> listening -> learning -> forwarding

| State | Forwards Frames | Learns MACs from frames | Transitory/Stable State |
| --- | --- | --- | --- |
| Blocking | No | No | Stable |
| Listening | No | No | Transitory |
| Learning | No | Yes | Transitory |
| Forwarding | Yes | Yes | Stable |
| Disabled | No | No | Stable |

## RSTP Concepts

### Comparing STP and RSTP

* RSTP and STP both:
    * elect root switch
    * select root ports
    * elect designated ports
    * place each port in forwarding/blocked states
* RSTP adds:
    * can replace root port without waiting
    * can replace designated port without waiting
    * lowers wait times when RSTP waits for timers

| Port Role | Function |
| --- | --- |
| Root port | Port that begins a nonroot switch's best path to the root |
| Alternate port | Port that replaces the root port when the root port fails |
| Designated port | Switch port designated to forward onto a collision domain |
| Backup port | Port that replaces a designated port when a designated port fails |
| Disabled port | Port that is administratively disabled |

### RSTP and the Alternate (Root) Port

### RSTP States and Processes

### RSTP and the Backup (Designated)

### RSTP Port Types

### Optional STP Features