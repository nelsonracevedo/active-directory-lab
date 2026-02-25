# 🛡️ Windows Active Directory Domain Security Lab

**Nelson R. Acevedo**  
Cybersecurity Student  

---

## 📌 Overview
This project demonstrates the deployment and hardening of a Windows Active Directory domain using **Windows Server 2022** in a virtualized environment. The lab simulates a small enterprise infrastructure with centralized user management, Group Policy enforcement, access control, and security monitoring.

---

## 🎯 Project Goals
- Create and configure a Windows Active Directory domain  
- Join a client device to the domain for testing  
- Centrally manage users and groups using Active Directory  
- Improve security and access control using Group Policy and auditing  

---


## 🧰 Tools & Technologies
- VMware Workstation  
- Windows Server 2022  
- Windows 11 (Domain Client)  
- Active Directory Domain Services (AD DS)  
- DNS  
- Group Policy Management  

---

## ⚙️ Setup Steps
1. Installed Windows Server 2022
2. Promoted to Domain Controller
3. Created OU structure: IT, HR, Users
4. Configured DNS
5. Joined Windows 11 client to domain
6. Created groups & assigned permissions  

---

## 🏗️ Environment Design

### Domain
- **Domain Name:** `nelcorp.local`

### Virtual Machines
- **DC01** – Windows Server 2022 (Domain Controller)  
- **CLIENT01** – Windows 11 (Domain-Joined Client)

> <img width="308" height="178" alt="image" src="https://github.com/user-attachments/assets/645edb96-3e40-40d4-9a75-fae82739705b" />
> Screenshot: CLIENT01 successfully joined to the domain


---

## 🌐 Network Design
- **VMware Internal Network:** VMnet2 (`192.168.10.0/24`)
- **DC01 Static IP:** `192.168.10.10`
- **DNS Configuration:**  
  - DNS points to **DC01** (including DC01 itself)



><img width="360" height="344" alt="image" src="https://github.com/user-attachments/assets/8898a69f-4262-4315-af60-a593c77a502e" />
><img width="309" height="350" alt="image" src="https://github.com/user-attachments/assets/7c91e24b-10b6-46e8-883f-d03652a46499" />
>Screenshots: VMware network configuration and DC01 network settings

---

## 🗂️ Active Directory Structure

### Organizational Units (OUs)
- IT  
- HR  
- Users  

This structure allows targeted Group Policy application, keeps the environment organized, and reflects real-world enterprise design.

> <img width="226" height="190" alt="image" src="https://github.com/user-attachments/assets/b8073afb-a82f-4b8c-b81b-2552a7dec3e7" /> Screenshot: OU structure in Active Directory Users and Computers

---

## 👥 Users, Groups & Access Control

### Users
- `it.admin`  
- `john.hr`  
- `mary.user`  

### Groups
- **IT_Admins** → `it.admin`  
- **HR_Users** → `john.hr`  

Users and groups were created within their respective Organizational Units. Group membership was used to apply Group Policies and control access to shared resources.

---

## 🔐 Group Policy & Security Implementation

The following Group Policies and security measures were implemented:

- Strong password policy  
- Disabled Control Panel for standard users  
- Automatic workstation lock after inactivity  
- Windows Defender Firewall enforced via GPO  
- Default Administrator account disabled  
- Audit logon and logoff events enabled  
- Default Guest account disabled  

These controls improve domain security and provide visibility into user activity.

**Note:**  
The default Administrator account was disabled after creating a dedicated administrative account named **it.admin**. If this account were not available, the default Administrator account could have been renamed instead.

><img width="259" height="270" alt="image" src="https://github.com/user-attachments/assets/3460be91-8264-4cf9-9399-591cd78d4063" />
><img width="311" height="272" alt="image" src="https://github.com/user-attachments/assets/8bee8d39-b1ca-4e0a-87a6-1d4d712635ba" />
>Screenshots: Group Policy Management Console and audit events in Event Viewer

---

## 📁 File Server & Permissions
A secure shared folder was created using **NTFS** and **share permissions**:

- **HR_Users** and **IT_Admins** → Access Allowed  
- **Other users** → Access Denied  

This demonstrates role-based access control using group membership.

><img width="261" height="235" alt="image" src="https://github.com/user-attachments/assets/0e232008-8ee2-4558-851e-8293ec21bad0" />
><img width="639" height="229" alt="image" src="https://github.com/user-attachments/assets/eff9deaa-f7ea-4aed-8778-2e4bdf89f14f" />
> Screenshots: Share permissions and access denied message

---

## 🧪 Testing & Validation
The following tests were performed to ensure proper functionality:

- Confirmed Group Policies applied only to intended users  
- Tested file share access with authorized and unauthorized accounts  
- Verified firewall and GPO enforcement on CLIENT01  
- Confirmed audit logon and logoff events were recorded on DC01  

><img width="567" height="294" alt="image" src="https://github.com/user-attachments/assets/0345550a-8429-409a-99c9-324f142bda82" />
> Screenshots: `Firewall status`

---

## ⚠️ Challenges & Lessons Learned

### Challenges
- #### DNS misconfigurations during setup:
    - 🚨 Challenge: DNS misconfigured — domain join failed
    - 🛠 Fix: Updated DC01 DNS settings to point to itself 
- #### Group Policies not applying due to incorrect OU placement:
    - 🚨 Challenge: I thought that having a user who was member of a group in a Organizational Unit (OU) made it part of that OU - This resulted on polocies no being applied correctly
    - 🛠 Fix: Move the users from the User OU to their respective OUs   

### Lessons Learned
- DNS is critical for Active Directory functionality  
- Group membership does **not** determine OU placement; users must be moved into the correct OU  
- All security controls must be tested and troubleshot to ensure proper enforcement  

---

## 📎 Screenshots
Screenshots are included throughout the repository to demonstrate configuration, Group Policy enforcement, access control, and validation results.
