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

## 🏗️ Environment Design

### Domain
- **Domain Name:** `nelcorp.local`

### Virtual Machines
- **DC01** – Windows Server 2022 (Domain Controller)  
- **CLIENT01** – Windows 11 (Domain-Joined Client)

> <img width="308" height="178" alt="image" src="https://github.com/user-attachments/assets/645edb96-3e40-40d4-9a75-fae82739705b" />
> 📸 Screenshot: CLIENT01 successfully joined to the domain


---

## 🌐 Network Design
- **VMware Internal Network:** VMnet2 (`192.168.10.0/24`)
- **DC01 Static IP:** `192.168.10.10`
- **DNS Configuration:**  
  - DNS points to **DC01** (including DC01 itself)

> 📸 Screenshots: VMware network configuration and DC01 network settings

---

## 🗂️ Active Directory Structure

### Organizational Units (OUs)
- IT  
- HR  
- Users  

This structure allows targeted Group Policy application, keeps the environment organized, and reflects real-world enterprise design.

> 📸 Screenshot: OU structure in Active Directory Users and Computers

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

> 📸 Screenshot: Group membership configuration

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

> 📸 Screenshots: Group Policy Management Console and audit events in Event Viewer

---

## 📁 File Server & Permissions
A secure shared folder was created using **NTFS** and **share permissions**:

- **HR_Users** and **IT_Admins** → Access Allowed  
- **Other users** → Access Denied  

This demonstrates role-based access control using group membership.

> 📸 Screenshots: Share permissions and access denied message

---

## 🧪 Testing & Validation
The following tests were performed to ensure proper functionality:

- Confirmed Group Policies applied only to intended users  
- Tested file share access with authorized and unauthorized accounts  
- Verified firewall and GPO enforcement on CLIENT01  
- Confirmed audit logon and logoff events were recorded on DC01  

> 📸 Screenshots: `gpresult` output and Event Viewer logs

---

## ⚠️ Challenges & Lessons Learned

### Challenges
- DNS misconfigurations during setup  
- Group Policies not applying due to incorrect OU placement  

### Lessons Learned
- DNS is critical for Active Directory functionality  
- Group membership does **not** determine OU placement; users must be moved into the correct OU  
- All security controls must be tested and troubleshot to ensure proper enforcement  

---

## 📎 Screenshots
Screenshots are included throughout the repository to demonstrate configuration, Group Policy enforcement, access control, and validation results.
