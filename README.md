# Cobalt Co - Network Design
Multi-floor office network design (subnetting, DHCP, RIP) for a fictional small business, built and tested in Cisco Packet Tracer.
## Overview 
This project simulates a network design engagement for a fictional small consulting firm, Cobalt Co., as it moves into a new 3 floor office building. The design supports approximately 50 emplyees across Sales, Accounting, HR, and IT/Management, with a dedicated guest wireless network for visitors. Built and tested in Cicso Packet Tracer, this project demonstrates subnetting, DHCP, configuration, and dynamic routing in a realistic small-business network topology. 

## Network Requirements

- Support ~50 employees across 3 floors: Sales/Reception, Accounting/HR, and IT/Management
- Provide a separate guest wireless network for customers/visitors for internet access 
- Use VLSM subnetting to size each subnet appropriately with minimal waste 
- Route between floor subnets using a Layer 3 core switch (no VLANs/trunking)
- Use RIP to advertise all internal subnets between the core switch and edge router 
- Provide DHCP for all end-user devices per floor, including a separate DHCP pool for guest wireless 
- Statically assign IPs to servers, the core switch's routed interfaces, and the core-to-edge router link 
- Centralize DNS, HTTP, and HTTP services on a single server in the IT/Management server room 
- Keep guest wireless traffice logically separate from internal department traffic (own subnet, own DNS, own swith uplink)
- Design with room for future growth

## Physical Layout

The Cobalt Co. Consulting network uses a single Layer 3 core switch as the distribution point for all floor subnets, with one edge router (Cobalt Router) handling the boundary to the ISP.

| Core Switch Port | Connects To |
|---|---|
| Gig1/0/1 | Cobalt Router (edge router / ISP boundary) |
| Gig1/0/2 | Floor 1 Sales/Reception switch |
| Gig1/0/3 | Floor 2 Accounting/HR switch |
| Gig1/0/4 | Floor 3 IT/Management switch (server room + IT PC) |
| Gig1/0/5 | Guest Access switch (isolated guest wireless subnet) |

Each floor swith is Layer 2 only (access switches simply forward frames to an end device). All inter-subnet routing happens at the core swith via routed interfaces (no VLANs or trunking required because each port is its subnet). The Cobalt Router connects the core switch to the ISP cloud and would handle NAT for internet-bound traffice. 

Guest Access is deliberately connected to its dedicated port (Gig1/0/5) rather than sharing a swith with Sales/Reception in order to keep guest traffic in its own broadcast domain. 

![Topology Diagram](docs/topology-diagram.jpg)

## IP Addressing Scheme 

| Floor/Segment | Network | CIDR | Subnet Mask | Gateway | Usable Range | Broadcast |
|---|---|---|---|---|---|---|
| Accounting/HR | 192.168.10.0 | /27 | 255.255.255.224 | 192.168.10.1 | 192.168.10.2 - 192.168.10.31 | 192.168.10.31 |
| Sales/Reception | 192.168.10.32 | /27 | 255.255.255.224 | 192.168.10.33 | 192.168.10.34 - 192.168.10.62 | 192.168.10.63 |
| IT/Management | 192.168.10.64 | /27 | 255.255.255.224 | 192.168.10.65 | 192.168.10.66 - 192.168.10.94 | 192.168.10.95 |
| Guest Wireless | 192.168.10.96 | /28 | 255.255.255.240 | 192.168.10.97 | 192.168.10.98 - 192.168.10.110 | 192.168.10.111 |
| Core-Edge Link | 192.168.10.112 | /30 | 255.255.255.252 | N/A (point-to-point) | 192.168.10.113 - 192.168.10.114 | 192.168.10.115 |
## Design Decisions 

### 1. IP Addressing & Subnetting 
 **Approach:** VLSM subnetting was used starting fromt 192.168.10.0/24

 - Accounting/HR, Sales/Reception, and IT/Management each received a /27 (30 useable addresses), sized to comfortably cover each floor's device count plus room for growth. 
 - Guest Wireless received a smaller /28 (14 useable addresses), since guest device counts may vary and are expected to be low and doesn't need the same available addresses as the staff subents. 
 - A /30 was reserved for the point-to-point link between the core switch and edge router, since only two devices (one interface on each side) occupy that link sizing it any larger would be a waste of address space. 
 - Remaining address space in the /24 (beyond .115) is left unused, available for future subnets if the office adds departments or device counts grow. 

 ### 2. Distribution Layer: Layer 3 Switch Vs Router-per-floor

 Rather than using a dedicated router for each floor, this design uses a single Layer 3 core switch with routed interfaces per floor subnet, connected to one edge router (Cobalt Router) for internet access. This mirrors typical small/mid-size business deployments where: 
    - Access switches (Floor 1, 2, 3, and Guest Wireless) forward frames within their segment.
    - The Layer 3 core switch handles inter-subnet routing, which is cheaper and faster than routing internal traffic through dedicated routers. 
    - A single edge router handles the boundary to the ISPm where routing between networks occur.

This reduces the cost and hardware count compared to router-per-floor design while still meeting all subnetting, DHCP, and routing requirements. 
## Configuration Highlighs 

## Testing & Verification 

## SKills Demonstrated 

## Tools Used 
