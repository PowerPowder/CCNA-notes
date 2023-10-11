# Chapter 7

## Terms

* **Port security**: 
* **Autonegotiation**: two nodes exchange messages to agree on using the same Ethernet standards (aka IEEE 802.3u)
* **Full duplex**: send and receive data at the same time.
* **half duplex**: send or receive data at a given time, requires CSMA/CD.
* **10/100**: Ethernet NIC tha supports 10/100Mbs.
* **10/100/1000**: Ethernet NIC that supports 10/100/1000Mbps.

## Configuring Switch Interfaces

### Configuring Speed, Duplex, Description

Autonegotiation is set by default, changing duplex or speed disables autonegotiation. `a-full` is full duplex, `a-100` is 100Mbps both autonegotiated on a connected port.

`duplex {auto | full | half}`

`speed {auto | 10 | 100 | 1000}`

`description <text>`

`show interfaces status` - list all interfaces, sow status, vlan, duplex, speed and type

`interface range FastEthernet 0/11 - 20` - configure Fa0/11 to Fa0/20, each port in the range is manually configured in IOS.

### Administratively Controlling Interface State with shutdown

`shutdown` disables ports (makes a port administratively down), `no shutdown` enables ports.

### Removing Configuration with the no Command

Using `no` on commands like speed, duplex, description, resets those commands to their default setting.

### Autonegotiation

#### Autonegotiation Under Working Conditions - On Both Ends

Ethernet devices on the ends of a link must use the same standard, otherwise they cannot send data. 100BASE-T cannot communicate with 1000BASE-T.

Autonegotiation opts for the highest speed and duplex supported between devices on ends of a link.

#### Autonegotiation Results When Only One Node Uses Autonegotiation

Sometimess autonegotiation is disabled on links to configure desired speed and duplex settings.

When autonegotiation is enabled on one side and speed/duplex is set on the other, the link may not work or work poorly.

If no response is sent after trying to autonegotiate, switches do (IEEE):
* Speed - sense the speed (without autonegotiation, cisco switch feature), otherwise use slowest speed (usually 10Mpbs)
* Duplex - if speed is 10Mbps or 100Mpbs use half duplex otherwise use full duplex.

<div style="text-align: center">
    <br>
    <img src="images/autonegotiation-failed.png" width="500px" alt="IEEE autonegotiation results with autonegotiation disabled on one side">
    <p>IEEE autonegotiation results with autonegotiation disabled on one side</p>
</div>

duplex mismatch: two nodes have different duplex modes configured, will be still listed as up/up.

#### Autonegotiation and LAN Hubs

hubs do not react to autonegotiation messages and don't forward them.

devices connected to hubs must use IEEE rules, leads to devices use 10Mbps half duplex and devices connected to the hub need to use CSMA/CD.

## Analysing Switch Interface Staus and Statistics

### Interface Status Codes and Reasons for Nonworking States

| Line Status (L1) | Protocol<br>Status (L2) | Interface<br>Status | Typical Root Cause |
| :-: | :-: | :-: | :-: |
| administratively down | down | disabled | The `shutdown` command is configured on the interface. |
| down | down | notconnect | No cable; bad cable; wrong cable pinouts, speed<br> mismatch, neighbouring device is (a) powered off, <br>(b), shutdown, or (c) error disabled. |
| up | down | notconnect | Not expected on LAN swich physical interfaces. |
| down | down (err-disabled) | err-disabled | Port security has disabled the interface. |
| up | up | connected | The interface is working. |

### Interface Speed and Duplex Issues

n/a

### Common Layer 1 Problems on Working Interfaces

Interface counters from `show interfaces <x>`:
* **Runts** - frame smaller than minimum size ( < 64 bytes)
* **Giants** - frames bigger than maximum size ( > 1518 bytes)
* **Input Errors** - total including runts, giants, no buffer, CRC, frame, overrun, ignored counts
* **CRC** - frames not passing FCS math
* **Frame** - frame has illegal format
* **Packet Output** - total packets sent out of interface
* **Output Errors** - total packets failed after trying to transmit
* **Collisions** - count of collisions caused when transmitting from this interface
* **Late Collisions** - collisions that occurred after a frame's 64th byte (possible duplex mismatch)