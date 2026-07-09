# IP Addressing Table 
This document outlines the VLSM addressing scheme used for the fictional office netork. 

| Floor/Segment | Network | CIDR | Subnet Mask | Gateway | Useable Range | Broadcast |
|---------------|---------|------|-------------|---------|---------------|-----------|
| Accounting/HR | 192.168.10.0 | /27 | 255.255.255.224 | 192.168.10.1 | 192.168.10.2-192.168.10.31 | 192.168.10.31 |
| Sales/Reception | 192.168.10.32 | /27 | 255.255.255.224 | 192.168.10.33 | 192.168.10.34 - 192.168.10.62 | 192.168.10.63 |
|IT/Managmenet | 192.168.10.64 | /27 | 255.255.255.224 | 192.168.10.65 | 192.168.10.66 - 192.168.10.94 | 192.168.10.95 |
| Guest Wireless | 192.168.10.96 | /28 | 255.255.255.240 | 192.168.10.97 | 192.168.10.98 -192.168.10.111 |