# Cisco 3850 Switch Lab Exercises - 6 Simple Projects

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
2. Connect PC0 to Fa0/1 and PC1 to Fa0/2 using straight-through cables
3. Connect PC0 to switch console port using console cable
4. Click on PC0 → Desktop → Terminal
5. Configure terminal settings: 9600 baud rate, 8 data bits, no parity, 1 stop bit
6. Press Enter to access switch CLI

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
**Time**: 5-7 minutes

---

## Exercise 2: VLAN Creation and Port Assignment

**Learning Objective**: Create VLANs and assign ports to different VLANs

### Packet Tracer Simulation:
1. Use same setup from Exercise 1
2. Access switch CLI through PC0 terminal
3. Create VLANs in global configuration mode

### Physical Lab Steps:
1. Use console connection established in Exercise 1
2. Execute these commands on the switch:

```
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Students
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name Teachers
Switch(config-vlan)# exit
Switch(config)# interface GigabitEthernet3/0/1
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
Switch(config)# interface GigabitEthernet3/0/2
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit
Switch(config)# exit
Switch# show vlan brief
```

**Expected Result**: VLANs created and ports assigned to different VLANs
**Time**: 6-8 minutes

---

## Exercise 3: Basic IP Configuration and Connectivity Testing

**Learning Objective**: Configure IP addresses on devices and test connectivity

### Packet Tracer Simulation:
1. Use setup from previous exercises
2. Click PC0 → Desktop → IP Configuration
3. Set Static IP: 192.168.10.10, Subnet: 255.255.255.0
4. Click PC1 → Desktop → IP Configuration  
5. Set Static IP: 192.168.20.10, Subnet: 255.255.255.0
6. Test connectivity using Command Prompt → ping

### Physical Lab Steps:
1. On Laptop 1, configure network adapter:
   - IP Address: 192.168.10.10
   - Subnet Mask: 255.255.255.0
2. On Laptop 2, configure network adapter:
   - IP Address: 192.168.20.10
   - Subnet Mask: 255.255.255.0
3. Test connectivity from Laptop 1:

```
ping 192.168.20.10
```

4. Observe that ping fails (different VLANs)
5. Move both ports to same VLAN via switch console:

```
Switch# configure terminal
Switch(config)# interface GigabitEthernet3/0/2
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

6. Test ping again - should now succeed

**Expected Result**: Understanding of VLAN isolation and connectivity
**Time**: 8-10 minutes

---

## Exercise 4: Switch Port Security Configuration

**Learning Objective**: Configure basic port security to control access

### Packet Tracer Simulation:
1. Use existing setup
2. Access switch CLI and configure port security on interface
3. Test with different MAC addresses

### Physical Lab Steps:
1. Using switch console connection, configure port security:

```
Switch# configure terminal
Switch(config)# interface GigabitEthernet3/0/1
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 1
Switch(config-if)# switchport port-security violation shutdown
Switch(config-if)# switchport port-security mac-address sticky
Switch(config-if)# exit
Switch(config)# exit
Switch# show port-security interface GigabitEthernet3/0/1
```

2. Check current MAC address learning:
```
Switch# show port-security address
```

3. Generate traffic from Laptop 1 (ping any IP)
4. Verify MAC address has been learned and secured

**Expected Result**: Port security configured and MAC address learned
**Time**: 6-8 minutes

---

## Exercise 5: Basic Switch Management - Save Configuration

**Learning Objective**: Learn to save and manage switch configurations

### Packet Tracer Simulation:
1. Make configuration changes in previous exercises
2. Use CLI to save configuration
3. Simulate power cycle and verify settings persist

### Physical Lab Steps:
1. View current configuration:
```
Switch# show running-config
```

2. Save configuration to NVRAM:
```
Switch# copy running-config startup-config
```
or simply:
```
Switch# write memory
```

3. Verify saved configuration:
```
Switch# show startup-config
```

4. View configuration file details:
```
Switch# dir flash:
Switch# show version
```

5. Create a backup description:
```
Switch# configure terminal
Switch(config)# banner motd #
Welcome to StudentSwitch - Lab Exercise Configuration
Authorized Access Only
#
Switch(config)# exit
Switch# copy running-config startup-config
```

**Expected Result**: Configuration saved and banner displayed on login
**Time**: 5-7 minutes

---

## Exercise 6: Basic Troubleshooting and Show Commands

**Learning Objective**: Use common troubleshooting commands to diagnose network issues

### Packet Tracer Simulation:
1. Intentionally create a problem (wrong VLAN assignment)
2. Use show commands to identify and fix the issue
3. Verify resolution

### Physical Lab Steps:
1. Create an intentional problem by moving one port to wrong VLAN:
```
Switch# configure terminal
Switch(config)# interface GigabitEthernet3/0/1
Switch(config-if)# switchport access vlan 99
Switch(config-if)# exit
```

2. Test connectivity between laptops (should fail)

3. Use troubleshooting commands to identify the issue:
```
Switch# show interfaces status
Switch# show vlan brief
Switch# show interfaces GigabitEthernet3/0/1 switchport
Switch# show mac address-table
```

4. Analyze output and identify the problem

5. Fix the issue:
```
Switch# configure terminal
Switch(config)# interface GigabitEthernet3/0/1
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

6. Verify fix:
```
Switch# show vlan brief
```

7. Test connectivity again (should work)

**Expected Result**: Students learn systematic troubleshooting approach
**Time**: 8-10 minutes

---

## Quick Reference Commands

### Essential Switch Commands:
- `enable` - Enter privileged mode
- `configure terminal` - Enter global configuration
- `show interfaces status` - View interface status
- `show vlan brief` - View VLAN information
- `show running-config` - View current configuration
- `copy running-config startup-config` - Save configuration

### Useful Troubleshooting Commands:
- `show mac address-table` - View MAC address table
- `show port-security` - View port security status
- `show version` - View switch information
- `show interfaces [interface-id]` - Detailed interface info

## Safety Notes:
- Always save configurations before making major changes
- Use `show running-config` to verify changes before saving
- Keep a record of original settings before modifications
- Never disconnect console cable during configuration updates
