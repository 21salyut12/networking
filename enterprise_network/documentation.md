# Network Design Documentation

## Overview
This documentation describes the current state of the configured network.
It includes subnetting, security configurations, dynamic routing, redundancy and administrative settings.

---

To separate traffic throughout the network, provide better security, and save up address space,
subnets and VLANs have been configured for the following segments: Wireless Guests, IT, HR, Sales and Server Room.
Hosts on each VLAN/subnet are dynamically assigned IPv4 addresses via DHCP.

## Subnetting

### 1. Wireless Guests
- **Subnet:** 192.168.4.0/27
- **Hosts:** 20
- **Security:**
  - Configured Wi-Fi password
  - Changed the default SSID 
  - SSID is not being broadcasted
- **Firewall Rules:**
  - Allow hosts on this subnet only servers access

### 2. IT Department
- **Subnet:** 192.168.1.0/26
- **Hosts:** 50
- **Firewall Rules:**
  - Allow all outgoing traffic
  - Deny incoming traffic from other subnets except for traffic used in basic network troubleshooting

### 3. Sales Department
- **Subnet:** 192.168.3.0/27
- **Hosts:** 16
- **Firewall Rules:**
  - Allow access to servers
  - Allow incoming traffic only from IT & HR

### 4. HR Department
- **Subnet:** 192.168.2.0/27
- **Hosts:** 20
- **Firewall Rules:**
  - Allow access to servers
  - Allow incoming traffic only from IT & Sales

### 5. Server Room
- **Subnet:** 192.168.5.0/28
- **Devices:** 6 servers (2 Web, 2 FTP, 2 Mail)
- **Firewall Rules:**
  - Configure NAT for public accessibility
  - **Web Servers:** Allow **HTTPS** and **ICMP** only
  - **FTP Servers:** Allow **FTP** and **ICMP** only
  - **Mail Servers:** Allow **Mail protocols** (SMTP and POP3) and **ICMP** only

### 6. Remote Worker
This is a remote subnet which is meant to simulate a WAN connection to the rest of the network.
- **Subnet:** 192.168.100.0/24
- **Connectivity:** Connects via eBGP to internal network

---

## VLAN Configuration

1. IT - VLAN 10
2. SALES - VLAN 20
3. HR - VLAN 30
4. WIRELESS_ACCESS - VLAN 40
5. SERVER_ROOM - VLAN 50

---

## Routing Protocols

### OSPF
Used for internal routing across the entire network. Subnets include:
- 10.0.0.0/30 IT-HR
- 10.0.1.0/30 IT-SALES
- 10.0.2.0/30 SALES-WIRELESS
- 10.0.3.0/30 WIRELESS-REDUNDANT1
- 10.0.4.0/30 REDUNDANT1-SERVERS
- 10.0.5.0/30 SERVERS-REDUNDANT2
- 10.0.6.0/30 REDUNDANT2-REMOTE_ACCESS_ROUTER
- 10.0.7.0/30 REMOTE_ACCESS_ROUTER-HR
- 10.0.8.0/30 HR-REDUNDANT2
- 10.0.9.0/30 HR-REDUNDANT1
- 10.0.10.0/30 IT-REDUNDANT2
- 10.0.11.0/30 IT-REDUNDANT1
- 10.0.12.0/30 SALES-REDUNDANT2
- 10.0.13.0/30 SALES-REDUNDANT1
- 10.0.14.0/30 WIRELESS-REDUNDANT2
- 10.0.15.0/30 REDUNDANT1-REDUNDANT2

### eBGP
Used to connect the Remote Worker network (192.168.100.0/24) to the main enterprise network via the REMOTE_ACCESS_ROUTER.
The network hosting the remote worker is using NAT to assign the user's PC a static public IPv4 address in order to simulate a real-life connection to the internet.

---

## Device Hardening & Admin Settings

### SSH Configuration (L2 & L3 Devices)
```cisco
ip domain-name admin.com
crypto key generate rsa
username admin privilege 15 secret Adm1nP455
line vty 0 4
 transport input ssh
 login local
exit
ip ssh version 2
```

### Banner of the Day
Set a login banner warning unauthorized users:
```cisco
banner motd #Authorized Access Only#
```

### Interface Descriptions
All interfaces include descriptive labels to reflect their function or link.

---

## Redundancy
The network design includes redundant routers, servers and links to ensure high availability and fault tolerance.

---

## Security Policies
- VLAN segmentation ensures traffic isolation
- Strict firewall rules per subnet
- PAT configured for server access
- SSH restricted and encrypted for secure remote management
- Hidden SSID for wireless guest access
