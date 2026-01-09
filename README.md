# WindowsServerHomeLab
Active Directory, DNS, DHCP, NAT, VMware, Lan Isolation

 Active Directory Lab — Network Architecture & Configuration
This project documents the design and deployment of a fully isolated, dual‑NIC Active Directory lab built using VMware Workstation and Windows Server. The environment supports secure internal networking, DNS, DHCP, and full internet access for domain‑joined clients through a routed Domain Controller.

🚀 Overview
I built a production‑style AD environment that is:
- Isolated from my home network
- Routed through a dual‑NIC Domain Controller
- DNS‑driven with forwarders for external resolution
- DHCP‑enabled for automated client configuration
- NAT‑enabled so clients can access the internet securely
- VMware‑based, using VMnet1 (Host‑Only) and VMnet8 (NAT)
This setup mirrors real enterprise networking and demonstrates advanced Windows Server and virtualization skills.

🏗️ Network Architecture
VMnet1 — Host‑Only Network (Internal AD LAN)
- Subnet: 192.168.50.0/24
- DC IP: 192.168.50.1
- Clients: 192.168.50.x
- No gateway (isolated)
- Used for: AD DS, DNS, DHCP, domain traffic
VMnet8 — NAT Network (Internet Uplink)
- Subnet: 192.168.10.0/24
- DC NAT NIC: 192.168.10.x
- Gateway: 192.168.10.2 (VMware NAT router)
- Used for: Internet access

🔧 Domain Controller Configuration
1. Active Directory Domain Services
- Deployed a new forest: localdomain.com
- Configured DNS integrated with AD
2. DHCP Server
Scope: 192.168.50.0/24
Options:
- 003 Router → 192.168.50.1
- 006 DNS Server → 192.168.50.1
- Automatic IP assignment for all domain clients
3. DNS Forwarding
Forwarders added:
- 8.8.8.8
- 1.1.1.1
Enables internal clients to resolve external domains.
4. NAT + Routing
Enabled NAT on the DC so clients can reach the internet while staying isolated.
- Enabled IP forwarding on both NICs
- Created NAT rule for 192.168.50.0/24
- Validated routing path:
Client → DC (Host‑Only NIC) → DC (NAT NIC) → Internet

🧪 Validation & Testing
✔ Client can ping external IPs
ping 8.8.8.8


✔ Client can resolve external domains
nslookup google.com


✔ Client receives correct DHCP lease
- IP: 192.168.50.x
- Gateway: 192.168.50.1
- DNS: 192.168.50.1
✔ DC routes traffic correctly
- NAT active
- IP forwarding enabled
- DNS forwarders functioning

🧠 Skills Demonstrated
- VMware Workstation advanced networking
- Dual‑NIC Windows Server configuration
- DHCP scope design and deployment
- DNS zone management + forwarders
- Windows Server NAT + routing
- Network isolation and segmentation
- Troubleshooting DNS, routing, and NAT
- Enterprise‑grade lab documentation

📌 Summary
This project showcases the design and implementation of a secure, isolated, internet‑enabled Active Directory environment using enterprise‑grade networking principles. It demonstrates proficiency in Windows Server, DNS, DHCP, NAT, routing, and virtualization — all essential skills for systems administration, IT infrastructure, and cybersecurity roles.
