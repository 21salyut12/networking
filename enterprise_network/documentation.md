# Enterprise Network in Cisco Packet Tracer

## Overview
The main objective of the project was to build an enterprise network that offers a high level of redundancy, scalability and fundamental security.

---

To better organize the network and save up address space as well as minimizing the attack surface in case of a possible cyber attack, the following subnets and VLANs were implemented: Wireless Guests, IT, HR, Sales and Server Room.

Regarding IP addressing, DHCP was implemented to handle dynamic IPv4 addressing for hosts across VLANs/subnets.

## Subnetting
The following section contains details regarding each subnet such as the maximum number of hosts, the network address and ACL rules that strengthen the overall network security.

### 1. Wireless Guests
- **Subnet:** 192.168.4.0/27
- **Hosts:** 20
- **Wireless Security:**
  - Configured PSK (Personal Shared Key) for guests to connect to the network
- **ACL Rules:**
  - Allow access only to the servers

### 2. IT Department
- **Subnet:** 192.168.1.0/26
- **Hosts:** 50
- **ACL Rules:**
  - Allow all outgoing traffic
  - Deny incoming traffic from other subnets except ICMP packets or other network traffic used for troubleshooting

### 3. Sales Department
- **Subnet:** 192.168.3.0/27
- **Hosts:** 16
- **ACL Rules:**
  - Allow access to servers
  - Allow incoming traffic only from IT & HR

### 4. HR Department
- **Subnet:** 192.168.2.0/27
- **Hosts:** 20
- **ACL Rules:**
  - Allow access to servers
  - Allow incoming traffic only from IT & Sales

### 5. Server Room
- **Subnet:** 192.168.5.0/28
- **Devices:** 6 servers (2 Web, 2 FTP, 2 Mail)
- **ACL Rules:**
  - **Web Servers:** Allow **HTTPS** and **ICMP** only
  - **FTP Servers:** Allow **FTP** and **ICMP** only
  - **Mail Servers:** Allow **Mail protocols** (SMTP and POP3) and **ICMP** only
- Configured NAT for public accessibility

### 6. Remote Worker
The idea here is to simulate a remote connection between a remote worker and the network.
- **Subnet:** 192.168.100.0/24
- **Connectivity:** Considering that the Internet relies on eBGP mostly, the remote worker's network will connect via eBGP to the office network.

---

## VLAN Configuration
The following is a list of VLANs implemented throughout the network. As mentioned in the beginning, the use of VLANs and subnetting facilitates in a better organization of the network as well as a better means to isolate certain parts of the network in case of a cyber attack. 

1. IT - VLAN 10
2. SALES - VLAN 20
3. HR - VLAN 30
4. WIRELESS_ACCESS - VLAN 40
5. SERVER_ROOM - VLAN 50

---

## Routing Protocols
To obtain high scalability, OSPF is the best solution for this as it offers high convergence through which the protocol maps out the entire network each time a topology change occurs

### OSPF
Below is a list of point-to-point connections between routers across the whole network:

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
  
---

## Device Hardening & Admin Settings

### SSH Configuration (L2 & L3 Devices)
For a more secured remote access to network devices SSHv2 was used because compared to Telnet, SSH encrypts session data.
The proccess to configure SSHv2 is showcased below:

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

### Interface Descriptions
All interfaces include descriptive labels to make it easy to identify to which network device they connect and to provide an easier way of troubleshooting issues at the Physical Layer.

---

## Redundancy
As mentioned before, the network design includes redundant routers, servers and links to ensure high availability and fault tolerance.

---

## PAT Configuration
To allow hosts outside the network access the servers, PAT was configured to forward all traffic intended for the server to one single public address.

## Servers
The network contains a total of six servers. For each configured service, that being mail, file transfer and web, 2 servers each were allocated for an improved redundancy and scalability.
