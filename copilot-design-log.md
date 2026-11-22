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
