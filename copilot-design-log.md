GitHub Copilot Design Log

Interaction 1: Campus Device Requirements

Prompt: Calculate the number of wired computers and printers required for each of the three campus buildings and recommend appropriate access switches based on the building requirements. I am designing a Campus Area Network in Cisco Packet Tracer for three two-story academic buildings.

Building A has two computer labs with 20 and 10 computers, 10 additional classrooms with one computer each, and 18 offices with one workstation and one printer each.

Building B has one computer lab with 15 computers, 9 additional classrooms with one computer each, and 14 offices with one workstation and one printer each.

Building C has 8 classrooms with one computer each and 11 offices with one workstation and one printer each.

Calculate the total number of wired computers and printers required for each building and the entire campus. Show your calculations separately for lab computers, classroom computers, office workstations, and printers. Do not include servers, switches, routers, or wireless devices in these totals.

Recommend a reasonable number of access switches for each building, considering that each building has two floors and must have at least one switch per floor. Explain your assumptions about how devices are distributed between floors.

Copilot Recommendation:

Copilot calculated the following wired device requirements:

Building A: 58 computers and 18 printers, totaling 76 devices.

Building B: 38 computers and 14 printers, totaling 52 devices.

Building C: 19 computers and 11 printers, totaling 30 devices.

Total campus: 115 computers and 43 printers, totaling 158 wired devices.

Copilot also recommended two 48-port access switches for Building A, two 48-port switches for Building B, and two 24-port switches for Building C.

Decision: Accepted the endpoint calculations. Provisionally accepted the switch recommendations, subject to floor-level planning.

Interaction 2: VLAN Design and Department Placement

Prompt: Asked Copilot to recommend a VLAN numbering and naming scheme for the campus, including the eight required departmental networks, servers, wireless clients, DMZ, and network management. I am designing a Campus Area Network in Cisco Packet Tracer for three two-story academic buildings. The campus uses the private IPv4 address block 10.50.0.0/16.

My assignment requires separate VLANs for Computer Science, Business, Engineering, Mathematics and Science, Humanities, Arts and Communication, Administration, and IT Sandbox.

The campus also needs centralized servers in Building A, a DMZ containing a public web server and proxy server, campus-wide wireless access, and network management.

Recommend a VLAN numbering and naming scheme for this campus. Include the eight required VLANs and any additional VLANs needed for servers, wireless clients, and network management. Identify which building primarily uses each VLAN.

Do not assign IP subnets yet. Explain why each additional VLAN is needed and identify any security considerations. Keep the design manageable for a student implementing it in Cisco Packet Tracer.

Your VLAN design contains incorrect building assignments. According to my assignment, Computer Science and Business are primarily in Building A, Engineering and Mathematics and Science are primarily in Building B, and Humanities and Arts and Communication are primarily in Building C.

  Please correct your VLAN table while keeping the same VLAN IDs. Remove the optional guest wireless VLAN because my assignment only requires one campus-wide SSID.

  Keep the DMZ isolated behind the firewall rather than treating it as an ordinary internal VLAN. Explain how this corrected design better matches the campus requirements.
 Copy prompt

Copilot Recommendation:

Copilot recommended VLANs 10–17 for the required departments and administrative networks, VLAN 20 for servers, VLAN 30 for the DMZ, VLAN 40 for campus wireless, and VLAN 99 for network management. It also suggested an optional guest wireless VLAN.

However, Copilot incorrectly assigned several academic departments to the wrong buildings.

Decision: Modified the recommendation.

Technical Reason:

I compared Copilot's proposed VLAN design with the assignment requirements and identified five incorrect departmental building assignments. I asked Copilot to correct these locations while keeping the VLAN numbering scheme.

The corrected design places Computer Science and Business in Building A, Engineering and Mathematics and Science in Building B, and Humanities and Arts and Communication in Building C.

I also removed the optional guest wireless VLAN because the assignment only requires one campus-wide SSID. The DMZ will remain isolated behind the firewall rather than being treated as an ordinary internal departmental VLAN.

These changes ensure the design matches the campus requirements while keeping the Packet Tracer implementation manageable.

Technical Reason:

I verified the calculations against the building requirements provided in the assignment. The total of 158 wired devices is correct. The suggested switches provide sufficient capacity based on an approximately even distribution of devices between floors. However, additional ports may be needed for wireless access points, uplinks, and future expansion. I will verify the switch capacity when creating the detailed network topology.

Interaction 3: IPv4 Addressing and VLSM Design

Prompt: Asked Copilot to create a non-overlapping IPv4 addressing plan using the campus address block 10.50.0.0/16, with appropriate VLSM subnet sizes and 25% future growth. Copilot Prompt #3: IPv4 Addressing Plan

I am designing a three-building Campus Area Network in Cisco Packet Tracer using the private IPv4 block 10.50.0.0/16.

My VLAN design is:
VLAN 10 - Computer Science (Building A)
VLAN 11 - Business (Building A)
VLAN 12 - Engineering (Building B)
VLAN 13 - Mathematics and Science (Building B)
VLAN 14 - Humanities (Building C)
VLAN 15 - Arts and Communication (Building C)
VLAN 16 - Administration (primarily Building A)
VLAN 17 - IT Sandbox (Building A)
VLAN 20 - Internal Servers (Building A)
VLAN 30 - DMZ (separate firewall zone)
VLAN 40 - Campus Wireless (all buildings)
VLAN 99 - Network Management

The campus has 158 wired endpoints:
Building A: 58 computers and 18 printers.
Building B: 38 computers and 14 printers.
Building C: 19 computers and 11 printers.

The exact number of endpoints assigned to each department is not specified. Do not invent department counts as facts. Propose reasonable planning estimates, clearly label them as assumptions, and account for 25% future growth.

Create a complete non-overlapping IPv4 VLSM addressing plan using different subnet sizes based on estimated host requirements.

For each VLAN, include:
1. VLAN ID and purpose
2. Estimated current hosts and 25% growth allowance
3. Required host bits and CIDR prefix
4. Network address and subnet mask
5. First and last usable IP addresses
6. Default gateway
7. Broadcast address

Include appropriately sized routed backbone/transit links if the topology requires them. Explain the subnet calculations and verify that no networks overlap. Use the first usable IP address as the default gateway for each VLAN where appropriate.

Keep the design practical for Cisco Packet Tracer and explain any assumptions that need to be confirmed before implementation. Copilot Interaction #3: Follow-up

I reviewed your VLSM plan and verified that the subnet calculations and ranges do not overlap.

  Please revise the design to give the IT Sandbox VLAN 17 a /27 subnet for additional flexibility. Reallocate any subsequent subnets as needed to avoid overlap.

  Also, use a separate simulated external IPv4 network, such as 203.0.113.0/30, for the firewall-to-edge-router connection rather than using the campus private 10.50.0.0/16 block.

  Keep the other VLAN subnet sizes unchanged unless necessary, and provide the updated complete addressing table, including subnet masks, gateways, usable ranges, and broadcast addresses.

  Explain how these changes affect the network design and confirm that all subnet boundaries remain valid.

Copilot Recommendation:

Copilot recommended different subnet sizes based on estimated device requirements:

/25 for campus wireless

/26 for Computer Science and Engineering

/27 for Business, Mathematics and Science, Humanities, Arts and Communication, Administration, and Network Management

/28 for the original IT Sandbox and internal servers

/29 for the DMZ

/30 for point-to-point routed connections

Decision: Modified and accepted the revised addressing plan as a working design.

Technical Reason:

I verified that the proposed subnets had valid network addresses, subnet masks, usable host ranges, default gateways, and broadcast addresses. I also checked that the subnet ranges did not overlap.

I requested that Copilot increase the IT Sandbox from a /28 to a /27 to provide additional flexibility for future devices.

I also requested a separate simulated external network using 203.0.113.0/30 instead of assigning the firewall's outside connection an address from the campus private network.

Copilot revised the subsequent subnet allocations to avoid overlap. The final design uses different subnet sizes based on estimated host requirements and includes room for future growth.

The departmental device counts are planning assumptions and will need to be confirmed during implementation.

Interaction 4: Campus Topology and OSPF Routing

Prompt: Asked Copilot to design a hierarchical Campus Area Network topology for three two-story buildings using Cisco Packet Tracer. The design needed to include access and distribution switches, a central core, OSPF routing, wireless access points, a firewall, DMZ, and centralized servers. I am designing a Campus Area Network in Cisco Packet Tracer for three two-story academic buildings and an outdoor common area.

Building A contains the central server room, Computer Science, Business, Administration, and IT Sandbox. Building B contains Engineering and Mathematics and Science. Building C contains Humanities and Arts and Communication.

Each building must have at least one access switch in each floor's switch closet. The campus also needs a central core, building distribution or aggregation, wireless APs on both floors of every building, an outdoor AP, a firewall, a DMZ, an ISP connection, and centralized servers.

My VLANs are 10–17 for departments, 20 for servers, 30 for the firewall-isolated DMZ, 40 for campus wireless, and 99 for network management. My addressing plan uses 10.50.0.0/16 with VLSM, and the current core-to-firewall transit network is 10.50.1.248/30.

My professor recommends OSPF for routed campus/backbone links. Please recommend a simple hierarchical topology that uses OSPF meaningfully between the three buildings while keeping the design manageable for a student in Cisco Packet Tracer.

Identify the specific Cisco Packet Tracer device types to use, the number of each device, the physical/logical connections, where inter-VLAN routing occurs, and where OSPF is configured.

Recommend non-overlapping /30 transit subnets for routed building links, starting at 10.50.2.0/30, without changing the existing VLAN subnet allocations.

Explain how the single campus-wide wireless SSID and VLAN 40 will operate across the three buildings. If routed building links prevent a simple shared Layer 2 wireless VLAN, explain the tradeoff and propose a Packet Tracer-compatible solution rather than assuming it works automatically.

Include a simple text-based topology diagram. Explain how the core connects to the firewall, DMZ, and ISP. Clearly distinguish which links are trunks and which are routed links.

Avoid unnecessary redundancy or advanced features that would make this student lab difficult to configure. Your topology is a useful starting point, but my assignment explicitly requires two application servers, a primary file server, a backup file server, a print server, NAS, UPS, IDS/IPS, KMS administrative device, and hardware firewall.

  Please revise your Packet Tracer device inventory to represent every required server-room component, using labeled substitutes where exact device types are unavailable.

  Also verify that Cisco 3560 switches in Packet Tracer can support a separate routed OSPF link and Layer 2 trunk between the core and each building distribution switch. Identify where VLAN 40 and VLAN 99 gateways should reside, and explain how to avoid duplicate gateways or Layer 2 loops.

  Keep the existing addressing plan and three /30 OSPF transit links unchanged. Provide a concise, practical final device inventory and connection plan.
 Copy prompt

Copilot Recommendation:

Copilot recommended one Cisco 3560 core switch, three Cisco 3560 building distribution switches, six Cisco 2960 floor access switches, and seven wireless access points.

The design uses OSPF area 0 between the core and building distribution switches, with the following transit networks:

Building A: 10.50.2.0/30

Building B: 10.50.2.4/30

Building C: 10.50.2.8/30

Copilot also recommended separate Layer 2 trunks for VLAN 40 (campus wireless) and VLAN 99 (network management), allowing the wireless network to span all three buildings.

Decision: Modified and provisionally accepted.

Technical Reason:

The original recommendation did not identify all required server-room equipment. I requested a revised inventory that included the application servers, file servers, print server, NAS, UPS, IDS/IPS, KMS administrative workstation, and firewall.

I also asked Copilot to verify that the proposed switches could support separate routed OSPF links and Layer 2 trunks.

The revised design provides a manageable hierarchical topology while supporting inter-building routing and a shared campus wireless network.

VLAN 40 and VLAN 99 gateways will reside on the core switch, while department VLAN gateways will reside on their respective building distribution switches.

The topology will need to be tested in Packet Tracer to confirm device compatibility and correct routing behavior.

Interaction 5: Firewall, DMZ, NAT, and Network Security

Prompt: Asked Copilot to design the campus security configuration, including firewall policies, NAT/PAT, DMZ isolation, IT Sandbox restrictions, management security, DHCP, routing, and verification tests. I am completing the security design for a three-building Campus Area Network in Cisco Packet Tracer.

My topology includes one Cisco 3560 core switch, three Cisco 3560 building distribution switches, six Cisco 2960 floor access switches, seven wireless APs, an ASA 5505 firewall, a DMZ switch, centralized internal servers, and a Cisco 2911 simulated ISP router.

OSPF area 0 connects the core and three building distribution switches. The core connects to the ASA firewall using 10.50.1.248/30 (core 10.50.1.249, firewall inside 10.50.1.250). The firewall outside interface uses 203.0.113.1/30 and the ISP router uses 203.0.113.2/30.

Important VLANs and subnets:
VLAN 16 Administration: 10.50.1.128/27, gateway 10.50.1.129
VLAN 17 IT Sandbox: 10.50.1.192/27, gateway 10.50.1.193
VLAN 20 Internal Servers: 10.50.1.224/28, gateway 10.50.1.225
VLAN 30 DMZ: 10.50.1.240/29, firewall gateway 10.50.1.241
VLAN 40 Campus Wireless: 10.50.0.0/25, gateway 10.50.0.1
VLAN 99 Network Management: 10.50.1.160/27, gateway 10.50.1.161
The remaining department VLANs are also part of the internal 10.50.0.0/16 campus network.

Please create a practical security and routing plan that can be implemented and tested in Cisco Packet Tracer.

Requirements:
1. Internal clients must reach a simulated external web server using NAT/PAT.
2. An external client must reach the public web server in the DMZ using appropriate static NAT or port forwarding.
3. Unsolicited external connections to internal campus clients must be blocked.
4. VLAN 17 IT Sandbox must be blocked from accessing VLAN 16 Administration, while normal permitted traffic continues to work.
5. The DMZ must be separated from the internal server network and must not initiate unrestricted connections to internal systems.
6. Network management access must be restricted to authorized IT devices.
7. The core must have a default route toward the firewall, and the firewall must have return routes to campus networks. Explain whether the core should advertise a default route through OSPF.
8. Explain where DHCP should run, how DHCP requests from routed department VLANs reach the DHCP server, and which devices need static IP addresses.
9. Provide at least 10 specific positive and negative verification tests, including expected results.

Explain where each ACL or firewall rule should be applied. Distinguish between Layer 3 switch ACLs and ASA firewall rules. Include Packet Tracer compatibility limitations and do not assume all ASA commands or advanced firewall features are supported.

Do not change the previously approved VLAN addressing plan or OSPF transit subnets. Prefer a simple configuration that can be implemented by a student rather than an enterprise-level design.

Copilot Recommendation:

Copilot recommended using the ASA firewall for Internet access, NAT/PAT, public DMZ web-server access, and protection against unsolicited external connections.

It recommended an extended ACL on Building A's VLAN 17 interface to prevent IT Sandbox devices from accessing the Administration VLAN.

The design also includes:

A default route from the core switch to the firewall.

OSPF default-route advertisement to the building distribution switches.

A static return route from the firewall to the campus network.

Centralized DHCP with relay configuration on routed VLAN interfaces.

Restricted network-device management access.

Fifteen positive and negative verification tests.

Decision: Provisionally accepted, subject to Packet Tracer testing.

Technical Reason:

The design separates internal campus traffic from external and DMZ traffic. The IT Sandbox ACL is applied at the Layer 3 switch because traffic between internal VLANs may not pass through the firewall.

NAT/PAT allows internal clients to access external services without exposing their private IP addresses. Static port forwarding provides controlled access to the public DMZ web server.

The proposed verification tests will help demonstrate that authorized traffic succeeds while prohibited connections are blocked.

Packet Tracer's ASA firewall may not support every feature or command proposed by Copilot. I will verify compatibility during implementation and document any necessary modifications.
