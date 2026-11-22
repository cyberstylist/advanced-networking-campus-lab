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

Technical Reason:

I verified the calculations against the building requirements provided in the assignment. The total of 158 wired devices is correct. The suggested switches provide sufficient capacity based on an approximately even distribution of devices between floors. However, additional ports may be needed for wireless access points, uplinks, and future expansion. I will verify the switch capacity when creating the detailed network topology.
