# Cobalt Co - Network Design
Multi-floor office network design (subnetting, DHCP, RIP) for a fictional small business, built and tested in Cisco Packet Tracer.
## Overview 
This project simulates a network design engagement for a fictional small consulting firm, Cobalt Co., as it moves into a new 3 floor office building. The design supports approximately 50 emplyees across Sales, Accounting, HR, and IT/Management, with a dedicated guest wireless network for visitors. Built and tested in Cicso Packet Tracer, this project demonstrates subnetting, DHCP, configuration, and dynamic routing in a realistic small-business network topology. 

## Network Requirements

## Topology

## IP Addressing Scheme 

## Design Decisions 

## Configuration Highlighs 

## Testing & Verification 
### Problem
DHCP clients not receiving IP Addresses

### Symptom
PCs on Sales/Reception, Accounting/HR, and Guest Wireless were not pulling IP addresses via DHCP. The IT/Management PC did not fail to obtain an address.

### Root Cause 1 - IP misconfiguraiton 
The core switch's routed interfaces had been assigned incorrect IPs, off by one from the documented gateway address. 

### Root Cause 2 - Duplicate Address Conflict 
After ensuring that IT/Management was receiving the correct IP addresses, the switch logged "%IP-4-DUPADDR: Duplicate address 192.168.10.65 on FastEthernet0/4, sourced by 0090.0cdb.dee5". 
Traced via "show mac address-table" to identify what it turned out to be, the IT/Management PC had been statically configured to 192.168.10.65 instead of set to DHCP. 

### Resolution 
1. Corrected all three routed intereface IPs to match the IP addressing table. 
2. Reconfigured the conflicting end device to use DHCP. 
3. Verified the server's Default Gateway field was set to "192.168.10.65" (not .66), since these had been mixed in the intial configuration. 
4. Re-tested DHCP on all four subnet and confirmed each PC pulled an addres from the correct pool with the correct gateway. 

### Verification Commands Used: 
show ip interface brief 
show mac address-table 
show run 

## SKills Demonstrated 

## Tools Used 
