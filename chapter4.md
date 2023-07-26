# Chapter 4

## Accessing the Cisco Switch CLI

### Cisco Catalyst Switches

This all refers to Cisco Catalyst enterprise-class switches.

RJ-45 UTP 10/100/1000 ports on a Cisco switch can auto-negotiate 10BASE-T, 100BASE-T, 1000BASE-T speeds.

**interfaces** and **ports** are a switch's physical connector.

Interface type are things like Ethernet, Fast Ethernet, Gigabit Ethernet.

Interfaces that run at multiple speeds are referred to as the highest speed, eg. 10/100/1000Mbps interface is called Gigabit Ethernet.

Interfaces are numbered 0/0, 0/1, ... on older switches or 1/0/1, 1/0/2 on newer switches.

### Accessing the Cisco IOS CLI

#### Cabling the Console Connection

Switch CLI can be accessed via:
* Console (Physical port) - use serial/USB from PC to RJ-45/USB switch console port, requires driver on pc
* Telnet (IP network) - communicate via IP to switch, unsecure method as it sends all data including username and password in clear-text
* SSH (IP network) - communicate vai IP to switch, secure as it encrypts all messages including passwords

<div style="text-align: center">
    <img src="images/connect-to-console.png" width="500px" alt="Console connection to a switch">
    <p>Console connection to a switch</p>
</div>

PC serial port has a D-shell connector with nine pines (DB-9).

Rollover cable is like ethernet but with different pinouts, eg pin 1 -> 8, pin 2 -> 7, pin 3 -> 6, ...

Default console port settings (last 3 settings are **8N1**):
* 9600 bits/second
* No hardware flow control
* **8**-bit ASCII
* **N**o parity bits
* **1** stop bit

#### User and Enable (Privileged) Modes

**user EXEC mode (user mode)** - allows user to type harmless exec commands, '>' at end of command prompt

Modes:
* User Mode
* Enable Mode
* Config Mode