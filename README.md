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

## Design Decisions 

## Configuration Highlighs 

## Testing & Verification 

## SKills Demonstrated 

## Tools Used 
