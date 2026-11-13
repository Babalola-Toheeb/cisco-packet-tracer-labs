Campus Network System Using Cisco Packet Tracer

A scalable campus network designed for City University with two campuses 80 miles apart — implemented in Cisco Packet Tracer using clustering for clean design.

Project Overview
City University has two campuses:
Main Campus: Building A (Admin + Faculty of Business), Building B (Faculty of Engineering/Computing + Art and Design), Building C (Student Lab + IT Department with Web Server)
City Campus: Faculty of Health and Sciences (Staff and Students on separate floors)

Goal: Provide end-to-end connectivity where each department/faculty is on its own isolated network, with secure access and centralized services.

My Topology — What I Actually Built

Root Level:
The main view shows two routers connected via a WAN link (Gig0/0/0). This represents the 80-mile distance between campuses. The Main router connects down to a distribution switch that branches into three clusters (Building A, B, C). The City router connects to a switch that branches into two clusters (Student's floor and Staff's floor).

Use of Clusters:
I used Packet Tracer clusters to hide complex parts of the network. This keeps the main workspace neat and makes it easy to present. Each building is a cluster, and inside each building there are sub-clusters for departments.

Inside the Buildings:
Building A: One access switch handling two departments — Admin staffs (VLAN 10) and Business (VLAN 20)
Building B: One access switch handling Eng-Com (VLAN 30) and Art&Design (VLAN 40)
Building C: One access switch (Switch7) handling IT (VLAN 60) which hosts the servers and Student Lab (VLAN 50)
City Campus Student's Floor: One switch with laptops for students
City Campus Staff's Floor: One switch with PCs for staff

Devices Observed:
2x Cisco 2911 Routers (Main and City)
5x Cisco 2960 Access Switches (one per building/floor)
1x Server (for Web/DNS services in IT department)
End devices: PCs, Laptops, Printers inside department clusters
Note: This differs from the initial requirement which suggested 3 routers and L3 switches — the final implementation uses Router-on-a-Stick for inter-VLAN routing, which is simpler and effective.

Logical Design Observed

VLAN Segmentation:
Each faculty/department is on its own VLAN (VLAN 10, 20, 30, 40, 50, 60) which provides isolation and better traffic management.

IP Management:
IP addressing uses the 10.0.10.0 to 10.0.60.0 range, with a /24 subnet for each VLAN
A /30 subnet is used for the WAN link between campuses
Router-based DHCP is configured to assign dynamic IPs to end devices across all VLANs
DNS server is centralized in the IT VLAN

Routing:
RIPv2 is used to share routes between Main and City campuses, ensuring devices from any building can reach the other campus.

Security & Management:
MOTD banner configured to display a warning and student/lab identification on login
Password encryption enabled (service password-encryption)
Enable secret and console/VTY login passwords set
Banner shows Student Name: Babalola Toheeb and Lab: Campus-Network-System

How It Works
A device in any building gets an IP from the router's DHCP pool for its VLAN
Inter-VLAN traffic goes through the Main router's sub-interfaces
Traffic to the other campus goes via the WAN link and RIPv2 routing
All VLANs can access the central server in the IT department

Screenshots from Packet Tracer
Root topology (Main-City WAN link)
Building A (Admin + Business)
Building B (Eng-Com + Art&Design)
Building C (IT + Student Lab)
City Campus (Student floor + Staff floor)
CLI with MOTD banner

Author
Babalola Toheeb

To Run
Open Campus-network.pkt in Cisco Packet Tracer, enter Realtime mode, and test connectivity with ping between buildings and campuses.