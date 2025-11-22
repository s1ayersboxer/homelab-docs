🖥️ Lab 02 – Join a Windows Client to the Domain

Purpose:
Join a Windows 10/11 client machine to the Active Directory domain created in Lab 01.

Prerequisites:

Domain Controller (DC01) is powered on

DNS running on DC01

Windows client VM installed (CLIENT01)

Both VMs on the same network (Host-Only or Internal Network)

--

✅ 1. Verify Network Connectivity
Check IP Configuration

On CLIENT01:

ipconfig /all


Make sure:

IP: 192.168.50.x (or your lab subnet)

Subnet: 255.255.255.0

Gateway: (optional depending on your setup)

DNS Server: should be DC01’s IP

If DNS points to anything else (like your real router), fix it:

Control Panel > Network > Change adapter settings
Right-click adapter → Properties
Internet Protocol Version 4 → Properties
Set DNS to: <DC01 IP>

🧪 2. Test Name Resolution

CLIENT01 must be able to find the Domain Controller by name.

Test the domain:

nslookup <your-domain-name>


Example:

nslookup homelab.local


You should see:

Server:  DC01.homelab.local
Address: 192.168.50.10


If this fails:

DNS on CLIENT01 is wrong

DC01 DNS service might not be running

Wrong network mode in VirtualBox

🔐 3. Join CLIENT01 to the Domain

Go to:

Settings → System → About → Rename this PC (advanced)


Or old version:

Control Panel → System → Change Settings


Click:

Computer Name → Change


Select:

Member of: Domain


Enter your domain name:

homelab.local


You should be prompted for domain credentials.

Enter:

Username: Administrator

Password: (your DC01 admin password)

You should see:

Welcome to the homelab.local domain.


Restart when prompted.

🖥️ 4. Verify Domain Membership

After reboot, log in using domain credentials:

homelab\Administrator


Or your domain user if you created one.

Check:

System → About → Domain: homelab.local


Or CLI:

whoami


Output:

homelab\administrator

🧰 5. Verify in Active Directory Users and Computers (ADUC)

On DC01:

Open:

Server Manager → Tools → Active Directory Users and Computers


Navigate to:

Computers


You should see:

CLIENT01


Optional:
Move it into a proper OU like:

Homelab > Computers > Workstations

🚨 6. Troubleshooting Guide
✔ “Domain controller not found”

DNS on CLIENT01 is wrong

DC01 name resolution failing

Client and server on different networks

✔ “Incorrect username or password”

Use:

Administrator


Not:

Administrator@domain


Unless doing UPN-style join.

✔ “No such domain exists”

DNS → DNS → DNS
99% of the time, DNS is the issue.

🎯 7. What You Learned

How domain join works

DNS dependency for Active Directory

Identity and authentication flow

How to verify and troubleshoot domain join failures

This lab prepares you for:

Group Policies

Login scripts

OU structures

User/computer management

Real help desk troubleshooting scenarios