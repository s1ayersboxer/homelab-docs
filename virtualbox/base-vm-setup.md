# Virtualbox Lab Setup

## 🎯 Purpose
Create repeatable VM templates for Windows Server, Windows 10, and Linux to speed up lab deployments.

---

## 🖥️ Recommended VM Settings

### Windows Server Template
- 2 CPUs
- 4–8GB RAM
- 60GB disk
- Network: Host-Only or Internal
- Snapshot after base install

### Windows 10 Template
- 2 CPUs
- 4GB RAM
- 40GB disk
- Network: NAT + Host-Only
---

## 🌐 Networking Options
- **NAT:** Internet access only  
- **Bridged:** Appears on LAN  
- **Host-Only:** Talk to host only  
- **Internal:** VMs talk to each other only  

---

## 📸 Snapshot Strategy
- Snapshot 1: Fresh OS install  
- Snapshot 2: After updates  
- Snapshot 3: Before joining domain