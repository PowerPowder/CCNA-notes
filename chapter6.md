# Chapter 6

## Terms
* **Telnet**: protocol used to remote into systems with a CLI without encryption
* **SSH**: remote into systems with a CLI using encryption and keys
* **Local username**: username (with password) configured locally on a router or switch
* **AAA**:
    * **A**uthentication - confirms identity of user/device
    * **A**uthorisation - what user/device is allowed to do
    * **A**ccounting - records user/device access attempts
* **AAA server**: contains security info and provides user login services
* **Enable mode**: enable settings to switches/routers (user EXEC, password, reload)
* **Default gateway**: IP address of a router, a host sends packets to this IP when sending outside of subnet.
* **VLAN interface**: interface between IOS and VLAN supported inside switch
* **History buffer**: list of commands in IOS that a user has entered in their session
* **DNS**: protocol that translates hostnames into IP addresses and vice versa
* **Name resolution**: IP host discovers IP address associated with a hostname
* **Log message**:

Work performed by networking devices:
1. Data plane - switches forwarding frames
2. Configuration and processes - control and change choices made by data plane
3. Management plane - security, remoting into device

## Securing the Switch CLI

Switch needs to be configured an IP address to support Telnet and SSH.

### Securing User Mode and Privileged Mode with Simple Passwords

Accessing user mode - console users supply console password, Telnet users supply vty password.

Accessing enable mode - both users supply the enable password

<div style="text-align: center">
    <br>
    <img src="images/console-telnet-enable-passwords.png" width="500px" alt="Simple Password Security Configuration">
    <p>Simple Password Security Configuration - set enable mode password first</p>
</div>

`login` tells IOS t enable a password (no username) on this line.

`password` is the password used.

`enable secret` is the enable mode password.

Virtual terminal (VTY) lines are the amount of possible connections allowed to a router/switch, numbered 0-15.

### Securing User Mode Access with Local Usernames and Passwords

<div style="text-align: center">
    <br>
    <img src="images/local-user-pass.png" width="500px" alt="Configuring switches to use local username login authentication">
    <p>Configuring switches to use local username login authentication</p>
</div>

`no password` can be used to remove existing shared passwords.

### Securing User Mode Access with External Authentication Servers