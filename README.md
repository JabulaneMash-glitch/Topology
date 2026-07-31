<img width="1091" height="581" alt="topology_cisco" src="https://github.com/user-attachments/assets/703512df-60b0-4b37-98a8-31b5e45a1563" />
🌐 Enterprise Network Design — Hybrid Ring-Star Topology

A complete office network design and Cisco Packet Tracer simulation for a business relocating into a new single-story facility (~100m × 50m), covering topology design, IP addressing, routing, security segmentation, and budgeting.

Group project — NWU CMPG315 (Computer Networks). My role on the team: Remote Access & Security Specialist.

📋 Project Brief

The business had only an ISP fiber connection (via ONT) and no internal network. The brief was to design a network for:

A boardroom and a 120-person open floor area
A technician's office and reception area
A kitchen with IoT device requirements
13 private offices

...all while keeping departmental traffic isolated for security, and sticking to a minimum-cost budget.

🏗️ Network Design

Topology: Hybrid ring-extended star

Each office cluster connects in a star to a dedicated access switch
Access switches uplink to 5 distribution routers (Routers 1–5)
Distribution routers connect in a ring to a central backbone router (Router 6)
Router 6 is both the ring's backbone and the ISP/internet entry point, and connects directly to the file server

A flat single-switch design was rejected — with 50+ devices across 7 functional zones, it would offer no redundancy and an unmanageably large broadcast domain. The ring adds router-level redundancy so no single router failure isolates a network segment.

Zones
Zone	Devices	Notes
Reception	Networked printer, 2 staff PCs, guest + staff Wi-Fi	Guest Wi-Fi restricted from internal resources
Server Room	All switches, core routers, enterprise server (DHCP/DNS/NAT/file storage)	Physically & logically isolated; technician-only access
Technician Office	2 wired PCs, direct wired link to server room, Wi-Fi for up to 8 devices	Enables monitoring/testing of core infrastructure
Working Offices (×13)	4 PCs + Wi-Fi per office	Aggregates through intermediate switches to the core
Remote Access	N/A (off-site)	Authenticated, segmented remote connections for hybrid work

Routing & Addressing
Routing protocol: RIP, enabled on every router interface to propagate routes around the ring
Addressing scheme: one /24 subnet per zone using private Class C space (192.168.x.0/24), giving 254 usable hosts per zone
All servers, printers, and network devices use static IPs; workstations are assigned from their zone's range

💰 Budget
Item	Calculation	Cost (ZAR)
Switches	R1,700 × 10	R17,000
Wireless Routers	R740 × 4	R2,960
Modem	R450 × 1	R450
PT Routers	R3,500 × 6	R21,000
Telephone	R2,700 × 1	R2,700
Access Points	R1,200 × 87	R104,400
Hardware Subtotal		R148,510
Labor (7 members × 2 days × R6,982/day)		R97,748
Total		R246,258

Access points make up the bulk of hardware cost, reflecting the number of untrusted Wi-Fi devices the design needs to support across the building.

🛠️ Tools & Methods
Simulation: Cisco Packet Tracer 9.0.0
Build approach: core infrastructure (Router 6, servers, core switches) was built and connectivity-tested first, then the router ring, then one office zone at a time — each zone verified with ping tests to the file server and to a PC in a different zone
Remote collaboration: WhatsApp for coordination and decisions, GitHub as the shared repository for .pkt files and documentation drafts, with peer-teaching used to fill topology/Packet Tracer knowledge gaps across the team
📂 Repository Contents
├── cisco12333.pkt                        # Cisco Packet Tracer network simulation file
├── Documentation Group 17.docx           # Full design report (topology, budget, IP schema, reflection)
└── Presentation_Document_Group17.pptx     # Project presentation slides

To open the simulation, download and install Cisco Packet Tracer (free with a Cisco Networking Academy account), then open the .pkt file.

🔍 Key Challenges & Learnings
Managing IP allocation and full connectivity across multiple subnets while integrating RIP on every router took significant iteration — routing inconsistencies and "host unreachable" errors were common early on
Packet Tracer's simplified feature set (limited VLAN depth, simplified wireless/firewall config) meant some real-world design decisions had to be adapted to what the simulator supports
The project reinforced the value of a clear core-distribution-access hierarchy and of documenting design decisions as they're made, not after the fact

👥 Team
Role	Contributor
Group Leader	                            LT Nkosiyaphantsi
Topology Designer                      	  TD Mohapi
Documentation Lead	                      TP Kekana
Budget Analyst	                          T van Wyk
Remote Access & Security Specialist    	  J Mashinini (me)
Packet Tracer Implementation Specialist	  IK Ngobeni
Quality Assurance & Review Lead	          KK Khanye
📄 License

This project is shared for portfolio/educational purposes.
