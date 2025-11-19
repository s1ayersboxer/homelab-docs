# Home Network Topology

## 🎯 Goal
Document the layout of my home network for troubleshooting, VLAN practice, and lab segmentation.

---

## 🏠 Network Diagram (Basic)

Router → Switch → Devices
                ↳ Homelab VMs
                ↳ Server 2022
                ↳ Test Windows Clients

---

## 🗺️ IP Scheme
| Device | IP | Purpose |
|--------|-----------|---------|
| Router | 192.168.1.1 | Gateway |
| DC01 | 192.168.1.10 | DNS/AD |
| CLIENT01 | DHCP | Domain joined |
| Linux VM | DHCP/static | Tools |

---

## 🧩 VLAN Ideas (Future)
- VLAN 10: Servers
- VLAN 20: Clients
- VLAN 30: IoT
- VLAN 40: Guest WiFi
