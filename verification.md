# Network Verification and Testing Plan

## 1. Purpose

This verification plan is designed to evaluate the functionality, connectivity, routing, and security of the Campus Area Network.

Both positive and negative tests will be performed to confirm that authorized network traffic succeeds and unauthorized traffic is blocked.

## 2. Verification Checklist

| Test ID | Test Description | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| T01 | Verify OSPF neighbor relationships between the core and building distribution switches. | All three OSPF adjacencies reach the FULL state. | Pending | Not Tested |
| T02 | Verify the routing tables on the building distribution switches. | Each distribution switch learns the default route through OSPF. | Pending | Not Tested |
| T03 | Access the simulated external web server at 198.51.100.10 from an internal client. | Connection succeeds using NAT/PAT. | Pending | Not Tested |
| T04 | Access the public DMZ web server from an external client using 203.0.113.1. | HTTP traffic is forwarded to 10.50.1.242 successfully. | Pending | Not Tested |
| T05 | Attempt an unsolicited connection from an external client to an internal campus device. | Connection is blocked. | Pending | Not Tested |
| T06 | Attempt to access an unauthorized port on the firewall's outside address. | Connection is denied. | Pending | Not Tested |
| T07 | Attempt communication from IT Sandbox VLAN 17 to Administration VLAN 16. | Traffic is blocked by the extended ACL. | Pending | Not Tested |
| T08 | Attempt communication from IT Sandbox VLAN 17 to an authorized non-Administration destination. | Permitted traffic succeeds. | Pending | Not Tested |
| T09 | Attempt to initiate communication from a DMZ server to an internal server. | Traffic is blocked by the firewall policy. | Pending | Not Tested |
| T10 | Attempt to access an approved DMZ service from an internal client. | Authorized service succeeds while unauthorized services are blocked. | Pending | Not Tested |
| T11 | Attempt SSH management access from the authorized IT management workstation. | SSH connection succeeds. | Pending | Not Tested |
| T12 | Attempt SSH management access from an unauthorized department or wireless client. | Management access is denied. | Pending | Not Tested |
| T13 | Request an IPv4 address using DHCP from a departmental client. | Client receives a valid IP address, subnet mask, and default gateway for its VLAN. | Pending | Not Tested |
| T14 | Verify the IPv4 configuration of a wireless client. | Client receives an address within 10.50.0.0/25 and gateway 10.50.0.1. | Pending | Not Tested |
| T15 | Connect wireless clients to the campus SSID in different buildings. | Clients successfully connect to VLAN 40 and reach permitted destinations. | Pending | Not Tested |

## 3. Additional Campus Connectivity Tests

| Test ID | Test Description | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| T16 | Verify connectivity between two devices within the same departmental VLAN. | Communication succeeds. | Pending | Not Tested |
| T17 | Verify authorized inter-VLAN communication within a building. | Communication succeeds through the distribution switch. | Pending | Not Tested |
| T18 | Verify authorized communication between devices in different buildings. | Communication succeeds through OSPF routing. | Pending | Not Tested |
| T19 | Access an authorized centralized internal server from a departmental client. | Connection succeeds. | Pending | Not Tested |

## 4. Verification Commands

The following commands will be used where supported by the selected Packet Tracer devices:

- show vlan brief
- show interfaces trunk
- show ip interface brief
- show ip route
- show ip ospf neighbor
- show access-lists
- show route (ASA)
- show xlate (ASA)
- ping
- traceroute or tracert
- ipconfig

Web browser testing and Packet Tracer Simulation Mode will also be used to verify application connectivity and firewall behavior.

## 5. Evidence Collection

Evidence will be collected during implementation and testing.

Evidence may include:

- Screenshots of the completed network topology.
- VLAN and trunk configuration outputs.
- OSPF neighbor and routing table outputs.
- Successful connectivity tests.
- Blocked unauthorized connectivity tests.
- DHCP client configurations.
- Wireless connectivity tests.
- Firewall and NAT verification outputs.

Screenshots and configuration excerpts will be included in the GitHub repository.

## 6. Packet Tracer Limitations

Some physical equipment and advanced security features may not be fully supported in Cisco Packet Tracer.

These limitations may include UPS operation, IDS/IPS inspection, wireless roaming, and certain ASA firewall or NAT features.

Any unsupported functionality will be documented rather than reported as successfully tested.

## 7. Final Verification Summary

Total planned tests: 19

Tests passed: Pending

Tests failed: Pending

Tests not performed: Pending

Final results and any necessary configuration corrections will be documented after implementation.

## 8. AI Assistance

GitHub Copilot assisted in developing the initial verification plan during Interaction 5. The recommendations were reviewed and expanded to include additional campus connectivity tests.

See copilot-design-log.md for additional information.
