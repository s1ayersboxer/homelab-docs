# VLAN Setup Guide

## 🎯 Objective
Explain and document how to design, configure, and test VLANs in a homelab environment using a virtual or physical router/switch.  
This guide helps build foundational networking skills for IT, sysadmin, and ServiceNow roles.

---

# 🧠 What is a VLAN?

A **VLAN (Virtual LAN)** splits one physical network into multiple logical networks.

Benefits:
- Better security (isolate devices)
- Reduced broadcast traffic
- Easier network organization
- Ability to separate servers, clients, IoT, and lab machines

---

# 🗂️ Example VLAN Plan

| VLAN | Name        | Purpose               | Subnet           | Notes |
|------|-------------|------------------------|-------------------|-------|
| 10   | Servers     | AD DS, DNS, VMs        | 192.168.10.0/24   | DC01, file server, etc. |
| 20   | Clients     | Windows clients, lab PCs| 192.168.20.0/24   | Domain-joined clients |
| 30   | IoT         | Cameras, smart home    | 192.168.30.0/24   | Segmented from LAN |
| 40   | Guest WiFi  | Guests & mobile        | 192.168.40.0/24   | Internet only |
| 99   | Management  | Switch/router access    | 192.168.99.0/24   | Admin only |

---

# 🔧 Requirements

You can test VLANs using:

### ✔ Physical gear  
- A managed switch (Netgear, TP-Link, UniFi, Cisco)  
- A router with VLAN support (pfSense, OPNsense, UniFi, MikroTik)

### ✔ OR Virtual Lab  
- pfSense VM  
- VirtualBox “Internal Network” or “Host-Only”  
- Virtual switches in Proxmox/VMware

Either setup works perfectly for learning.

---

# 🛠️ Step 1 — Create VLANs on the Router

### pfSense Example (GUI)

1. Login to pfSense
2. Go to **Interfaces → Assignments**
3. Click **VLANs**
4. Add new VLANs:
   - Parent interface: `em0` or `vtnet0`
   - VLAN Tag: `10`
   - Description: `Servers`

Repeat for 20, 30, 40, 99.

---

# 🧱 Step 2 — Assign Subnets & DHCP

For each VLAN:

Example for VLAN 10:

- Subnet: `192.168.10.0/24`
- Gateway: `192.168.10.1` (router)
- DHCP Range: `192.168.10.100 – 192.168.10.200`

Repeat for every VLAN.

---

# 🔌 Step 3 — Configure Managed Switch (Trunks & Access Ports)

### Key Concepts

- **Access Port** → belongs to ONE VLAN  
  Example: Windows client on VLAN 20  
- **Trunk Port** → carries MANY VLANs  
  Example: Router ↔ Switch connection  

### Example Switch Settings

**Port 1 (to pfSense router)**  
- Mode: Trunk  
- VLANs Allowed: 10, 20, 30, 40, 99  
- Native VLAN: 1 or 99 (depending on your design)

**Port 5 (server DC01)**  
- Mode: Access  
- VLAN: 10

**Port 8 (Windows client)**  
- Mode: Access  
- VLAN: 20

---

# 🧪 Step 4 — Test VLAN Connectivity

### Test 1: Verify IP Assignment
On each client:
- VLAN 10 device should get `192.168.10.x`
- VLAN 20 device should get `192.168.20.x`
- VLAN 30 device should get `192.168.30.x`

### Test 2: Ping Gateway
From each device:

```cmd
ping 192.168.10.1
ping 192.168.20.1

