# ACLs

## What are ACLs
  ACLs (Access Control Lists) are sets of rules defined by system administrators and network engineers to permit or deny incoming and outgoing traffic at key network points, such as routers, firewalls, and Layer 3 switches.

  Several types of ACLs exist, including Standard, Extended, Named, Dynamic, Reflexive, and Time-Based ACLs. However, this repository primarily focuses on Standard and Extended ACLs, as they are the most commonly used.

### Why Standard and Extended ACLs Are Popular
  - Standard ACLs
    - Simple and lightweight, primarily used for basic filtering based on source IP
    - Typically applied near the destination to prevent unnecessary overblocking
    - Commonly used for basic network segmentation and restricting access to subnets
  - Extended ACLs
    - More flexible, allowing filtering based on source, destination, protocol, and ports
    - Ideal for firewall-like filtering, VPN traffic control, and QoS (Quality of Service) policies
    - Usually applied near the source to filter unwanted traffic before it enters the network
      
## Use cases
  - Network Security
  - Restrict access to sensitive internal resources by blocking unauthorized IPs
  - Prevent specific protocols (e.g., Telnet, FTP) from being used on certain network segments
  - Control access to network devices by allowing only trusted hosts to connect via SSH
  - Traffic Control and Optimization
  - Prioritize certain types of traffic by allowing only specific applications or services
  - Block unnecessary or harmful traffic, reducing network congestion and enhancing performance
  - Apply QoS rules by filtering packets based on protocol and port numbers
  - User and Device Access Management
  - Enforce role-based access by allowing different departments access to specific network areas
  - Restrict guest network access to certain internet services while blocking access to internal systems
  - Allow VPN users to access only specific resources based on predefined rules
    
## Examples

1. Standard ACL Example (Blocking a Specific Source IP)
```cisco
access-list 10 deny 192.168.1.100
access-list 10 permit any
interface GigabitEthernet0/1
ip access-group 10 in
```
Explanation: This ACL denies traffic from 192.168.1.100 while allowing all other traffic.
2. Extended ACL Example (Allowing Web Traffic and Blocking FTP)
```cisco
access-list 100 permit tcp any any eq 80
access-list 100 deny tcp any any eq 21
access-list 100 permit ip any any
interface GigabitEthernet0/1
ip access-group 100 in
```
Explanation:
Allows HTTP (port 80) traffic.
Blocks FTP (port 21) traffic.
Permits all other traffic.

## Conclusion
  By implementing ACLs, network administrators can enforce security policies, optimize traffic flow, and manage access effectively.
