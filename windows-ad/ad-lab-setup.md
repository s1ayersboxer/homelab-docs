# Active Directory Lab Setup

## 🎯 Goal
Set up a basic Active Directory domain in my homelab to practice user management, group policy, and authentication.

---

## 🧱 Lab Topology

- **Hypervisor:** VirtualBox
- **Domain Controller VM:**
  - OS: Windows Server 2022 Datacenter (Eval)
  - RAM: 4GB (adjust as needed)
  - CPU: 2 cores
  - Disk: 60GB
- **Client VM:**
  - OS: Windows 10 / 11
  - RAM: 4GB
  - Joined to domain: `lab.local` (example)

---

## 🔌 Step 1 — Create the Domain Controller VM

1. Create a new VM in VirtualBox:
   - Name: `DC01`
   - Type: Windows
   - Version: Windows Server 2022
2. Attach the ISO and install Windows.
3. Set a strong local Administrator password.
4. Set a **static IP**, for example:
   - IP: `192.168.1.10`
   - Subnet: `255.255.255.0`
   - Gateway: (your router or leave blank for lab)
   - DNS: `192.168.1.10` (itself, once DNS is installed)

---

## 🧩 Step 2 — Install Active Directory Domain Services

1. Open **Server Manager**
2. Click **Add roles and features**
3. Choose:
   - Role-based installation
   - Select this server
   - Check **Active Directory Domain Services**
4. Complete the wizard and **restart if prompted**

---

## 🌐 Step 3 — Promote to Domain Controller

1. In Server Manager, click the flag notification
2. Click **Promote this server to a domain controller**
3. Choose:
   - **Add a new forest**
   - Root domain name: `lab.local` (or your choice)
4. Set DSRM password
5. Accept defaults and complete the wizard
6. Server reboots as a **Domain Controller**

---

## 💻 Step 4 — Join a Client to the Domain

1. Create another VM in VirtualBox:
   - Name: `CLIENT01`
   - OS: Windows 10 / 11
2. Make sure it’s on the same network as `DC01`
3. Set DNS on the client to `192.168.1.10`
4. On the client:
   - Right-click **This PC → Properties**
   - Click **Rename this PC (advanced)** or **Change settings**
   - Click **Change…**
   - Select **Domain** and enter: `lab.local`
5. When prompted, enter domain credentials (e.g. `lab\Administrator`)
6. Restart client

---

## 🧪 Step 5 — Test the Domain

- Log in as a **domain user**
- Test:
  - `ping dc01`
  - `nslookup dc01` 
- Create a few test users in **Active Directory Users and Computers**

---

## 📝 Notes / Issues Hit

- Example: “Had DNS misconfigured, client couldn’t find domain”
- Example: “Forgot to set static IP on DC”
- Example: “VirtualBox networking: switched from NAT to Internal Network”

---

## ✅ Next Steps

- Set up **OU structure**
- Create **Group Policies**
- Practice **user/group management**
- Add another client VM