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

1. Simple ACL Configuration
   ![simple_acl](https://github.com/user-attachments/assets/5af9f46b-7f8b-4d40-af33-35713df76324)
```cisco
<!-- STUB (to insert correct configurations) -->
```

2. Blocking HTTP traffic by using Extended ACLs
    ![http_acl_filtering](https://github.com/user-attachments/assets/7dcfbd47-2764-4cac-b80a-3686399f0005)
```cisco
<!-- STUB (to insert correct configurations)-->
```

## Conclusion
  By implementing ACLs, network administrators can enforce security policies, optimize traffic flow, and manage access effectively.
