# Chapter 4

## Accessing the Cisco Switch CLI

### Terms
* **command-line interface (CLI)**: interface to interact with the operating system 
* **Telnet**: protocol used to remote into systems with a CLI without encryption
* **Secure Shell**: remote into systems with a CLI with encryption and keys
* **enable mode**: enable settings to switches/routers (user EXEC, password, reload)
* **user mode**: used for nondisruptive EXEC commands, like looking at current status
* **configuration mode**: used for config commands that are added to running config file
* **startup-config file**: sits in NVRAM, holds config file that's loaded into RAM on reload or power on
* **running-config file**: sits in RAM, holds currently used config, updates dynaically


### Cisco Catalyst Switches

Interface type are things like Ethernet, Fast Ethernet, Gigabit Ethernet.

Interfaces that run at multiple speeds are referred to as the highest speed, eg. 10/100/1000Mbps interface is called Gigabit Ethernet.

Interfaces are numbered 0/0, 0/1, ... on older switches or 1/0/1, 1/0/2, ... on newer switches.

### Cisco IOS CLI

Switch CLI can be accessed via:
* Console (Physical port) - serial (DB-9 connector), rollover cable (for RJ-45 console), USB
* Telnet (IP network)
* SSH (IP network)

<!-- Default console port settings (last 3 settings are **8N1**):
* 9600 bits/second
* No hardware flow control
* **8**-bit ASCII
* **N**o parity bits
* **1** stop bit -->

`?` lists all commands or parameters depending on context, `<TAB>` is used to autocomplete.

`show` lists the switch's operational status, eg: `show mac address-table dynamic` lists table used for making forwarding decisions.

`debug` records all output from commands entered after this command.

### User and Enable (Privileged) Modes

**user EXEC mode (user mode)** - allows user to type harmless exec commands, '>' at end of command prompt

`enable` changes the mode to enable mode, `disable` goes to user mode.

`reload` tells the switch reinitialize/reboot, only used in enable mode.

Commands used in user mode and enable mode are EXEC commands.

**Setting passwords**:
* Enable mode - `enable secret password123` 
* User mode:
    1. `line console 0` - identifies the console, next commands apply to the console only.
    2. `login` - perform simple password checking at login.
    3. `password password123` - the password the user must enter to gain access.

## Configuration Mode

Commands entered in config mode update the running config file.

<div style="text-align: center">
    <br>
    <img src="images/ios-modes.png" width="600px" alt="Escalating/de-escalating different modes in IOS CLI">
    <p>Escalating/de-escalating different modes in IOS CLI</p>
    <br>
</div>

## Configuring Cisco IOS Software

Global config mode is the initial config mode, you move into subcommand modes (context).

**Common switch configuration modes**:
| Prompt | Name of mode | Context-setting commands to reach mode |
| --- | --- | --- |
| `hostname(config)#` | Global | None |
| `hostname(config-line)#` | Line | `line console 0`<br>`line vty 0 15` |
| `hostname(config-if)#` | Interface | `interface` *type* *number* |
| `hostname(config-vlan)#` | VLAN | `vlan` *number* |

### Switch Configuration Files

Four types of memory in Cisco switches:
* **RAM**: current running config (active)
* **Flash memory**: stores Cisco IOS images, boot config and backups of config files
* **ROM**: stores bootstrap program - finds Cisco IOS image and loads it into RAM.
* **NVRAM (Nonvolatile RAM)**: stores initial config or startup config

`copy running-config startup-config` copies running config to startup config.

**Create fresh config**:

```
write erase
erase startup-config
erase nvram:
reload
```

<!--
Modes:
* User Mode 'hostname>'
* Enable Mode 'hostname#'
* Config Mode 'hostname(config)#'

<div style="text-align: center">
    <br>
    <img src="images/cisco-ios-command-hierarchy.png" width="" alt="Cisco IOS command hierarchy">
    <p>Cisco IOS command hierarchy</p>
    <br>
</div>
-->