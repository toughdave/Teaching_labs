# Cisco 3850 Switch Lab Exercises - 3 Simple Projects

## Prerequisites - Disconnect from Wi-Fi - no internet for this exercise
## Prerequisites - Software to Install on Laptops

Before starting any exercise, ensure you have these programs installed:

1. **Cisco Packet Tracer** (Latest version from Cisco Networking Academy)
2. **PuTTY** (SSH/Telnet client for Windows) or Terminal (for Mac/Linux)
3. **Command Prompt/Terminal** access

## Equipment Setup Overview

- **Physical Setup**: 1 Cisco 3850-48U-POE-S switch, 2 student laptops
- **Connections**: 
  - Laptop 1 (Primary): Console cable + Ethernet cable to switch
  - Laptop 2 (Secondary): Ethernet cable to switch
- **Switch Ports**: Use ports GigabitEthernet3/0/1 and GigabitEthernet3/0/2 for Ethernet connections

---


## Exercise 1: Basic Switch Configuration and Interface Status

**Learning Objective**: Configure basic switch settings and check interface status

### Packet Tracer Simulation:
1. Drag a 2960 switch and 2 PCs onto workspace
2. Connect PC0 to Gig0/1 and PC1 to Gig0/2 using straight-through cables
3. Connect PC0 to switch console port using console cable
4. Click on PC0 → Desktop → Terminal
5. Configure terminal settings: 9600 baud rate, 8 data bits, no parity, 1 stop bit
6. Press Enter to access switch CLI
   
```
Switch> enable
Switch# configure terminal
Switch(config)# hostname StudentSwitch
StudentSwitch(config)# exit
StudentSwitch# show interfaces status
StudentSwitch# show version
```


### Physical Lab Steps:
1. Connect console cable from Laptop 1 to switch console port
2. Connect Ethernet cables from both laptops to switch ports GigabitEthernet3/0/1 and GigabitEthernet3/0/2
3. Open PuTTY on Laptop 1
4. Configure Serial connection: COM port (check Device Manager), Speed: 9600
5. Click "Open" to connect to switch
6. Execute these commands:

```
Switch> enable
Switch# configure terminal
Switch(config)# hostname StudentSwitch
StudentSwitch(config)# exit
StudentSwitch# show interfaces status
StudentSwitch# show version
```

**Expected Result**: Switch hostname changes, interface status displayed


---

## Exercise 2: Interface Configuration and Port Management

**Learning Objective**: Configure switch interfaces and understand port status

### Packet Tracer Simulation:
1. Use same setup from Exercise 1
2. Access switch CLI through PC0 terminal
3. Configure interface descriptions and settings

```
Switch> enable
Switch# configure terminal
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# description Laptop-1-Connection
Switch(config-if)# no shutdown
Switch(config-if)# exit
Switch(config)# interface GigabitEthernet0/2
Switch(config-if)# description Laptop-2-Connection
Switch(config-if)# no shutdown
Switch(config-if)# exit
Switch(config)# exit
Switch# show interfaces status
Switch# show running-config
```


### Physical Lab Steps:
1. Use console connection established in Exercise 1
2. Execute these commands on the switch:

```
Switch> enable
Switch# configure terminal
Switch(config)# interface GigabitEthernet3/0/1
Switch(config-if)# description Laptop-1-Connection
Switch(config-if)# no shutdown
Switch(config-if)# exit
Switch(config)# interface GigabitEthernet3/0/2
Switch(config-if)# description Laptop-2-Connection
Switch(config-if)# no shutdown
Switch(config-if)# exit
Switch(config)# exit
Switch# show interfaces status
Switch# show running-config
```

**Expected Result**: Interface descriptions configured and visible in running-config, ports are active


---

## Exercise 3: Basic IP Configuration and Connectivity Testing

**Learning Objective**: Configure IP addresses on devices and test connectivity

### Packet Tracer Simulation:
1. Use setup from previous exercises
2. Click PC0 → Desktop → IP Configuration
3. Set Static IP: 192.168.1.10, Subnet: 255.255.255.0, Gateway: 192.168.1.1, DNS: 8.8.8.8
4. Click PC1 → Desktop → IP Configuration  
5. Set Static IP: 192.168.1.11, Subnet: 255.255.255.0, Gateway: 192.168.1.1, DNS: 8.8.8.8
6. Test connectivity using Command Prompt → ping

### Physical Lab Steps:
1. On Laptop 1, configure network adapter:
   - IP Address: 192.168.1.10
   - Subnet Mask: 255.255.255.0
   - Default Gateway: 192.168.1.1
   - DNS Server: 8.8.8.8
2. On Laptop 2, configure network adapter:
   - IP Address: 192.168.1.11
   - Subnet Mask: 255.255.255.0
   - Default Gateway: 192.168.1.1
   - DNS Server: 8.8.8.8
3. Test connectivity from Laptop 1:

```
ping 192.168.1.11
```

4. Test connectivity from Laptop 2:

```
ping 192.168.1.10
```

5. Both pings should be successful since both laptops are on the same network

**Expected Result**: Successful ping between both laptops showing network connectivity


---

## Quick Reference Commands

### Essential Switch Commands:
- `enable` - Enter privileged mode
- `configure terminal` - Enter global configuration
- `show interfaces status` - View interface status
- `show running-config` - View current configuration
- `copy running-config startup-config` - Save configuration

### Useful Troubleshooting Commands:
- `show mac address-table` - View MAC address table
- `show version` - View switch information
- `show interfaces [interface-id]` - Detailed interface info

## Safety Notes:
- Always save configurations before making major changes by using `write memory` or `wr` or `copy running-config startup-config`
- Use `show running-config` to verify changes before saving
- Keep a record of original settings before modifications
- Never disconnect console cable during configuration updates
