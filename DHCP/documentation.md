# DHCP

## What is DHCP

**Dynamic Host Configuration Protocol (DHCP)** is a network management protocol used on Internet Protocol (IP) networks to automatically assign IP addresses and other network configuration parameters to devices, enabling them to communicate efficiently. This automation reduces the need for manual configuration and helps prevent IP address conflicts.  
[Source: Wikipedia](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol?utm_source=chatgpt.com)

## How DHCP Works

DHCP operates on a client-server model and involves the following sequence:

1. **DHCP Discover**: The client broadcasts a DHCP Discover message to locate available DHCP servers.
2. **DHCP Offer**: DHCP servers respond with a DHCP Offer message, proposing an IP address and configuration parameters.
3. **DHCP Request**: The client replies with a DHCP Request message, accepting the offered parameters.
4. **DHCP Acknowledgment**: The server finalizes the process with a DHCP Acknowledgment message, confirming the lease and configuration details.

This process ensures that each device on the network receives a unique IP address and appropriate configuration settings.  
[Source: TechTarget](https://www.techtarget.com/searchnetworking/definition/DHCP?utm_source=chatgpt.com)

## Benefits of DHCP

- **Simplifies Network Administration**: Automates IP address assignment, reducing manual configuration errors.
- **Efficient IP Address Management**: Dynamically allocates IP addresses, optimizing address utilization.
- **Centralized Configuration**: Allows centralized management of network settings such as DNS servers and gateways.

[Source: GeeksforGeeks](https://www.geeksforgeeks.org/dynamic-host-configuration-protocol-dhcp/?utm_source=chatgpt.com)

## Use Cases

- **Enterprise Networks**: Automates IP configuration for devices, simplifying large-scale network management.
- **Home Networks**: Enables seamless connectivity for personal devices without manual setup.
- **Public Wi-Fi**: Provides temporary IP addresses to guests, ensuring secure and efficient network access.

[Source: EfficientIP](https://efficientip.com/glossary/what-is-dhcp-and-why-is-it-important/?utm_source=chatgpt.com)

## Examples

### Example 1: Configuring a DHCP Server on a Cisco Router

```cisco
! Exclude addresses from being assigned by DHCP
ip dhcp excluded-address 192.168.100.1

! Define a DHCP pool
ip dhcp pool LAN_POOL
   network 192.168.100.0 255.255.255.0
   default-router 192.168.100.1
   dns-server 8.8.8.8 8.8.4.4
   lease 7
