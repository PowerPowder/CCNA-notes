# Chapter 8

## Terms

* **802.1Q**: 
* **Trunk**: 
* **Trunking Administrative Mode**: 
* **Trunking Operational Mode**: 
* **VLAN**: 
* **VTP**: 
* **VTP Transparent Mode**: 
* **Layer 3 Switch**: 
* **Access Interface**: 
* **Trunk Interface**: 
* **Data VLAN**: 
* **Voice VLAN**: 
* **Native VLAN**: 
* **Default VLAN**: 
* **Static Access Interface**: 

## VLAN Concepts

* **A LAN includes all devices in the same broadcast domain**

<div style="text-align: center">
    <img src="images/vlan.png" width="500px" alt="Creating two broadcast domains using one switch and vlans">
    <p>Creating two broadcast domains using one switch and vlans</p>
</div>

* Reasons to create smaller broadcast domains:
    * reduce CPU usage - less broadcast frames
    * improves security - less hosts flooded
    * specify security for different vlans
    * groups users/devices
    * easier to troubleshoot with less devices
    * reduce STP workload
* VLAN tagging - switch adds header (802.1q) to frame before sending over VLAN trunk (vlan id)

### Creating Multiswitch VLANs Using Trunking

#### VLAN Tagging Concepts

* VLAN trunking combines all vlans through one link

<div style="text-align: center">
    <img src="images/vlan-trunking.png" width="500px" alt="">
    <p>VLAN trunking between two switches</p>
</div>

#### 802.1Q and ISL VLAN Trunking Protocols

* 4 byte header is added to frame, VLAN ID is 12 bits, supports values 1 to 4094
* VLAN IDs 1 to 1005 are normal-range, 1006 to 4094 are extended-range
* VLAN 1 is default VLAN aka native VLAN, no header is added to frames for this VLAN

### Forwarding Data Between VLANs

#### The Need for Routing Between VLANs

#### Routing Packets Between VLANs with a Router

* Devices in different VLANs need to be in different subnets
* Only L3 switches and routers can connect different VLANs/subnets together

## VLAN and VLAN Trunking Configuration and Verification

### Creating VLANs and Assigning Access VLANs to an Interface

#### VLAN Configuration Example 1: Full VLAN Configuration

#### VLAN Configuration Example 2: Shorter VLAN Configuration

### VLAN Trunking Protocol

### VLAN Trunking Configuration

### Implementing Interfaces Connected to Phones

#### Data and Voice VLAN Concepts

#### Data and Voice VLAN Configuration and Verification

#### Summary: IP Telephony Ports on Switches

## Troubleshooting VLANs and VLAN Trunks

### Access VLANs Undefined or Disabled

### Mismatched Trunking Operational States

### The Supported VLAN List on Trunks

### Mismatched Native VLAN on a Trunk