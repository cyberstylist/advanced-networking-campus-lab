# IPv4 Addressing and VLSM Plan

## 1. Addressing Overview

The Campus Area Network uses the private IPv4 address block 10.50.0.0/16. Variable Length Subnet Masking (VLSM) is used to allocate subnets based on the estimated host requirements of each VLAN while allowing for 25% future growth.

The first usable IP address in each VLAN subnet is assigned as the default gateway.

## 2. Planning Assumptions

The campus contains 158 wired endpoints:

| Building | Computers | Printers | Total |
|---|---:|---:|---:|
| Building A | 58 | 18 | 76 |
| Building B | 38 | 14 | 52 |
| Building C | 19 | 11 | 30 |
| Total | 115 | 43 | 158 |

The assignment does not specify the exact number of devices assigned to each department. Therefore, departmental host counts are planning estimates that maintain the required building totals.

Additional planning estimates include 60 wireless clients, 8 internal server devices, 2 DMZ servers, and 12 network management devices. Infrastructure counts will be confirmed during implementation.

## 3. VLSM Host Requirements

Projected host requirements are calculated by multiplying the estimated current host count by 1.25 and rounding up. One additional usable address is required for the default gateway.

Usable host capacity is calculated using 2^h - 2, where h represents the number of host bits.

| VLAN | Purpose | Current Hosts | Hosts After Growth | Required Including Gateway | Host Bits | CIDR | Usable Capacity |
|---|---|---:|---:|---:|---:|---|---:|
| 40 | Campus Wireless | 60 | 75 | 76 | 7 | /25 | 126 |
| 10 | Computer Science | 25 | 32 | 33 | 6 | /26 | 62 |
| 12 | Engineering | 30 | 38 | 39 | 6 | /26 | 62 |
| 11 | Business | 23 | 29 | 30 | 5 | /27 | 30 |
| 13 | Mathematics and Science | 22 | 28 | 29 | 5 | /27 | 30 |
| 14 | Humanities | 17 | 22 | 23 | 5 | /27 | 30 |
| 15 | Arts and Communication | 13 | 17 | 18 | 5 | /27 | 30 |
| 16 | Administration | 20 | 25 | 26 | 5 | /27 | 30 |
| 99 | Network Management | 12 | 15 | 16 | 5 | /27 | 30 |
| 17 | IT Sandbox | 8 | 10 | 11 | 5 | /27 | 30 |
| 20 | Internal Servers | 8 | 10 | 11 | 4 | /28 | 14 |
| 30 | DMZ | 2 | 3 | 4 | 3 | /29 | 6 |

The IT Sandbox was intentionally allocated a /27 rather than a /28 to provide additional flexibility for future lab devices.

## 4. VLAN Addressing Table

| VLAN | Network Address | CIDR | Subnet Mask | First Usable | Last Usable | Default Gateway | Broadcast |
|---|---|---|---|---|---|---|---|
| 40 | 10.50.0.0 | /25 | 255.255.255.128 | 10.50.0.1 | 10.50.0.126 | 10.50.0.1 | 10.50.0.127 |
| 10 | 10.50.0.128 | /26 | 255.255.255.192 | 10.50.0.129 | 10.50.0.190 | 10.50.0.129 | 10.50.0.191 |
| 12 | 10.50.0.192 | /26 | 255.255.255.192 | 10.50.0.193 | 10.50.0.254 | 10.50.0.193 | 10.50.0.255 |
| 11 | 10.50.1.0 | /27 | 255.255.255.224 | 10.50.1.1 | 10.50.1.30 | 10.50.1.1 | 10.50.1.31 |
| 13 | 10.50.1.32 | /27 | 255.255.255.224 | 10.50.1.33 | 10.50.1.62 | 10.50.1.33 | 10.50.1.63 |
| 14 | 10.50.1.64 | /27 | 255.255.255.224 | 10.50.1.65 | 10.50.1.94 | 10.50.1.65 | 10.50.1.95 |
| 15 | 10.50.1.96 | /27 | 255.255.255.224 | 10.50.1.97 | 10.50.1.126 | 10.50.1.97 | 10.50.1.127 |
| 16 | 10.50.1.128 | /27 | 255.255.255.224 | 10.50.1.129 | 10.50.1.158 | 10.50.1.129 | 10.50.1.159 |
| 99 | 10.50.1.160 | /27 | 255.255.255.224 | 10.50.1.161 | 10.50.1.190 | 10.50.1.161 | 10.50.1.191 |
| 17 | 10.50.1.192 | /27 | 255.255.255.224 | 10.50.1.193 | 10.50.1.222 | 10.50.1.193 | 10.50.1.223 |
| 20 | 10.50.1.224 | /28 | 255.255.255.240 | 10.50.1.225 | 10.50.1.238 | 10.50.1.225 | 10.50.1.239 |
| 30 | 10.50.1.240 | /29 | 255.255.255.248 | 10.50.1.241 | 10.50.1.246 | 10.50.1.241 | 10.50.1.247 |

## 5. Routed Transit Networks

OSPF area 0 will be configured between the core switch and the three building distribution switches.

Each point-to-point connection uses a /30 subnet with two usable IP addresses and two host bits.

| Connection | Network/CIDR | Subnet Mask | First Device IP | Second Device IP | Broadcast |
|---|---|---|---|---|---|
| Core to Building A | 10.50.2.0/30 | 255.255.255.252 | 10.50.2.1 | 10.50.2.2 | 10.50.2.3 |
| Core to Building B | 10.50.2.4/30 | 255.255.255.252 | 10.50.2.5 | 10.50.2.6 | 10.50.2.7 |
| Core to Building C | 10.50.2.8/30 | 255.255.255.252 | 10.50.2.9 | 10.50.2.10 | 10.50.2.11 |
| Core to Firewall | 10.50.1.248/30 | 255.255.255.252 | 10.50.1.249 | 10.50.1.250 | 10.50.1.251 |
| Firewall to ISP | 203.0.113.0/30 | 255.255.255.252 | 203.0.113.1 | 203.0.113.2 | 203.0.113.3 |

The core-to-firewall and firewall-to-ISP connections use static routing rather than OSPF.

## 6. Default Gateway Locations

| Device | VLAN Gateways |
|---|---|
| Building A Distribution Switch | 10, 11, 16, 17, 20 |
| Building B Distribution Switch | 12, 13 |
| Building C Distribution Switch | 14, 15 |
| Core Switch | 40, 99 |
| ASA Firewall | 30 |

## 7. Planned Static IP Assignments

| Device | IP Address | CIDR | Default Gateway |
|---|---|---|---|
| Central DHCP Server | 10.50.1.226 | /28 | 10.50.1.225 |
| DMZ Web Server | 10.50.1.242 | /29 | 10.50.1.241 |
| DMZ Proxy Server | 10.50.1.243 | /29 | 10.50.1.241 |
| KMS Admin Workstation | 10.50.1.162 | /27 | 10.50.1.161 |
| Simulated External Web Server | 198.51.100.10 | /24 | 198.51.100.1 |

Remaining static infrastructure addresses will be assigned during Packet Tracer implementation. The DHCP service may be hosted on an existing internal server.

The external networks use documentation-only IPv4 address ranges for simulation purposes.

## 8. Addressing Validation

The proposed VLAN and routed transit subnets have been reviewed for valid network boundaries, subnet masks, usable host ranges, and broadcast addresses.

No allocated subnets overlap. Each VLAN has sufficient usable address capacity for its estimated host requirements, projected growth, and default gateway.

The remaining address space within 10.50.0.0/16 is available for future expansion.

Final device assignments, DHCP operation, and network connectivity will be verified during Packet Tracer implementation.

## 9. AI Assistance

GitHub Copilot was used to assist with the initial VLSM calculations and addressing design. The recommendations were reviewed and modified to accommodate additional IT Sandbox capacity, routed OSPF connections, and separate simulated external addressing.

See copilot-design-log.md for the original prompts, recommendations, design decisions, and technical reasoning.
