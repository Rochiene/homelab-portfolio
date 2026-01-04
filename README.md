# homelab-portfolio
# 🖥️ Windows Server & Active Directory Homelab Portfolio  
**Built by Shaine**  
Role Focus: System Administrator / M365 Admin / Infrastructure Engineer

---

## 📌 Overview  
This repository documents my complete hands-on homelab project where I built a functional Windows Server Active Directory environment using Hyper-V.  
The goal is to demonstrate my practical skills in identity, networking, automation, and system administration.

This lab includes:

- Hyper-V VM Creation (DC01)
- Windows Server 2022 Domain Controller  
- DNS, DHCP, Group Policy  
- File Server with NTFS and share permissions  
- Windows 10 workstation joined to the domain  
- PowerShell automation scripts  
- Clean, enterprise-style OU structure  
- Documentation and screenshots of every major task

---

## 🗺️ Lab Architecture  
**Hypervisor:** Hyper-V  
**Network:** Internal switch (LAB-SWITCH)  
**Domain:** `lab.shaine.local`  
**Static IP:** 10.0.0.10 (DC01)

```
┌─────────────────────┐
│ Hyper-V │
│ Internal Switch │
└──────────┬──────────┘
│
┌──────────┴──────────┐
│ DC01 │
│ Windows Server 2022 │
│ AD DS, DNS, DHCP │
└──────────┬──────────┘
│
┌──────────┴──────────┐
│ SRV02 │
│ File Server / GPO │
└──────────┬──────────┘
│
┌──────────┴──────────┐
│ WIN10-CLI01 │
│ Workstation │
└─────────────────────┘
```

## 📁 Sections

0. Hyper-V VM Creation (DC01)
1. Domain Controller Deployment
2. Organizational Unit Structure
3. User & Group Management
4. Windows 10 Domain Join
5. Group Policies
6. DHCP Configuration
7. File Server (SRV02)
8. PowerShell Automation

---

### **0. Hyper-V VM Creation (DC01)**
This section shows the process of creating the first virtual machine in Hyper-V, which becomes the Domain Controller for lab.shaine.local.

✔ Tasks Performed
- Created a new virtual machine (DC01)
- Created a new Internal switch (LAB-SWITCH)
- Assigned it to an isolated internal network (LAB-SWITCH)
- Configured virtual hardware (memory, CPU, VHDX)
- Mounted Windows Server 2022 ISO
- Prepared DC01 for OS installation

### 📸 Screenshots  
#### Hyper-V Manager
![Hyper-V Manager](screenshots/hyperv/hyperv_manager.png)

#### Internal Switch Creation (LAB-SWITCH)
![Internal Switch Creation (LAB-SWITCH)](screenshots/hyperv/internal_switch.png)

#### VM Name & Location
![VM Name](screenshots/hyperv/new_vm_name.png)

#### Generation 2 Selection
![Generation 2](screenshots/hyperv/generation2.png)

#### Memory Allocation
![Memory Allocation](screenshots/hyperv/memory_alloc.png)

#### LAB-SWITCH Networking
![LAB-SWITCH Selection](screenshots/hyperv/network_switch.png)

#### VHDX Setup
![VHDX Setup](screenshots/hyperv/vhdx_setup.png)

#### ISO Installation Source
![ISO Selection](screenshots/hyperv/install_iso.png)

#### VM Summary Before Creation
![VM Summary](screenshots/hyperv/vm_summary.png)

#### Windows Server Setup Boot Screen
![Windows Setup](screenshots/hyperv/windows_setup.png)

---

### **1. Domain Controller Deployment (DC01)**
This section covers the installation and configuration of the Domain Controller for the lab.shaine.local domain.
It includes static IP setup, AD DS + DNS installation, domain creation, and verification of SYSVOL and DNS health.

✔ Tasks Performed
- Installed Windows Server 2022
- Assigned static IP (10.0.0.10)
- Installed AD DS and DNS roles
- Promoted server to new forest: lab.shaine.local
- Verified DNS records and SYSVOL replication

### 📸 Screenshots
- **Server Manager – DC01 Overview**  
  ![DC01 Server Manager](screenshots/ad/server_manager_dc01.png)

- **Static IPv4 Configuration**  
  ![Static IP](screenshots/ad/static_ip_config.png)

- **AD DS + DNS Roles Installed**  
  ![Roles Installed](screenshots/ad/server_manager_roles.png)

- **Active Directory Users and Computers – Domain View**  
  ![ADUC Domain](screenshots/ad/aduc_domain_view.png)

- **DNS Forward Lookup Zone – lab.shaine.local**  
  ![DNS Zone](screenshots/ad/dns_forward_zone.png)

- **SYSVOL Folder Verification**  
  ![SYSVOL Folder](screenshots/ad/sysvol_folder.png)



---

### **2. OU Unit Structure**
This section documents the creation of a clean, professional Active Directory OU layout used to separate users, computers, groups, and administrative accounts.
A well-designed OU structure is the foundation for scalable Group Policy management and enterprise-ready domain organization.

✔ Tasks Performed
- Created top-level OUs for Users, Computers, and Groups
- Added sub-OUs for Admin Accounts, Standard Users, Servers, and Workstations
- Adopted an enterprise-style naming standard for clear management
- Prepared the structure for Group Policy, user provisioning, and workstation domain joins

```
lab.shaine.local
│
├── LAB Users
│     ├── Admin Accounts
│     └── Standard Users
│
├── LAB Computers
│     ├── Servers
│     └── Workstations
│
└── LAB Groups
      ├── Security Groups
      └── Distribution Groups
```

### 📸 Screenshots
- **OU Structure (Full AD Tree Expanded)**  
  ![OU Structure](screenshots/ad/ou_full_structure.png)

- **New OU Creation Window**  
  ![Create OU Window](screenshots/ad/ou_create.png)

---

### **3. User & Group Management**
This section documents the creation of administrative and standard user accounts within the new Active Directory domain.
A separate admin account ensures best security practices, while a standard user account allows testing of Group Policy, permissions, and workstation domain joins.

✔ Tasks Performed
- Created a privileged admin account (shaine.admin)
- Added shaine.admin to:
- Domain Admins
- Enterprise Admins
- Schema Admins (lab-only)
- Created a standard user (test.user1)
- Placed accounts into proper Organizational Units
- Followed enterprise identity management practices

### 📸 Screenshots

- **Admin Account Creation (shaine.admin)**  
  ![Admin Account Creation](screenshots/ad/admin_account_create.png)

- **Admin Account – Group Memberships**  
  ![Admin Account Groups](screenshots/ad/admin_account_groups.png)

- **Standard User Account Creation (test.user1)**  
  ![Standard User Creation](screenshots/ad/test_user_create.png)

---
### **4. Windows 10 Domain Join**

This section documents the deployment and configuration of the Windows 10 workstation (WIN10-CLI01) and its successful integration into the Active Directory domain `lab.shaine.local`.  
A domain-joined client is essential for testing Group Policies, permissions, login scripts, and real-world sysadmin workflows.

✔ **Tasks Performed**
- Created and configured the WIN10-CLI01 virtual machine
- Completed OS installation and initial setup
- Renamed the PC to match lab naming standards
- Assigned a static IP address
- Joined the workstation to the domain `lab.shaine.local`
- Verified domain authentication
- Confirmed the workstation object appears in the correct AD OU

---

### 📸 Screenshots

- **WIN10-CLI01 – VM Summary in Hyper-V**  
  ![WIN10 VM Summary](screenshots/win10/win10vm_summary.png)

- **Windows 10 Installation Complete**  
  ![WIN10 Installation Complete](screenshots/win10/win10_install_complete.png)

- **PC Renamed to WIN10-CLI01**  
  ![PC Rename](screenshots/win10/rename_win10.png)

- **Static IPv4 Configuration (WIN10-CLI01)**  
  ![Static IP](screenshots/win10/win10_static_ip.png)

- **Domain Join Process (lab.shaine.local)**  
  ![Domain Join](screenshots/win10/domain_join_success.png)

- **WIN10-CLI01 in Active Directory (Workstations OU)**  
  ![WIN10 in AD](screenshots/win10/win10_in_ad.png)

- **WIN10-CLI01 Login Screen – “Sign in to: LAB”**  
  ![Domain Login Screen](screenshots/win10/win10_domain_login_screen.png)

- **System Information Showing Domain Membership**  
  ![System Domain](screenshots/win10/win10_system_domain.png)

---

### **5. Group Policies (GPO)**

This section documents the creation, configuration, and validation of Group Policies used to enforce security baselines, manage user environments, and centrally control domain-joined systems within `lab.shaine.local`.  
Both policy-side configuration and client-side results are captured to demonstrate end-to-end GPO implementation.

✔ **Tasks Performed**
- Configured password and account security policies via Default Domain Policy  
- Implemented a login banner for legal and security compliance  
- Created drive mapping using Group Policy Preferences (GPP)  
- Applied Control Panel restrictions for standard users  
- Deployed desktop wallpaper via GPO  
- Implemented security baseline GPOs for servers, workstations, and users  
- Verified policy application on client machine (WIN10-CLI01)  

---

### 📸 Screenshots

- **Password Policy Configuration (Default Domain Policy)**  
  ![Password Policy](screenshots/gpo/password_policy.png)

- **Login Banner GPO Configuration**  
  ![Login Banner GPO](screenshots/gpo/gpo-login-banner.png)

- **Login Banner Applied on Client (WIN10-CLI01)**  
  ![Login Banner Result](screenshots/gpo/login_banner.png)

- **Drive Mapping GPO Configuration (Group Policy Preferences)**  
  ![Drive Mapping Created](screenshots/gpo/gpo-drive-mapping-created.png)

- **Client Drive Mapping Applied Successfully**  
  ![Drive Mapping Success](screenshots/gpo/client-drive-mapping-success.png)

- **Control Panel Restrictions – GPO Configuration**  
  ![Control Panel Configuration](screenshots/gpo/gpo_control_panel_configuration.png)

- **Control Panel Restrictions – Security Filtering / Scope**  
  ![Control Panel Filtering](screenshots/gpo/gpo_control_panel_security_filtering.png)

- **Desktop Wallpaper Policy Configuration**  
  ![Wallpaper Policy](screenshots/gpo/wallpaper_policy.png)

- **Server Security Baseline GPO**  
  ![Server Hardening](screenshots/gpo/Server-Hardening.png)

- **Workstation Security Baseline GPO**  
  ![Workstation Baseline](screenshots/gpo/Workstation-Baseline.png)

- **User Security Baseline GPO**  
  ![User Security Baseline](screenshots/gpo/User-Security-Baseline.png)


---

### **6. DHCP Configuration**

This section documents the deployment and configuration of the Dynamic Host Configuration Protocol (DHCP) role within the Active Directory environment.  
DHCP was configured to automatically assign IP addresses to domain-joined clients, with reservations used to ensure consistent addressing for critical machines.

✔ **Tasks Performed**
- Installed the DHCP Server role on DC01  
- Authorized the DHCP server in Active Directory  
- Created and activated a DHCP scope  
- Configured IP address reservations for WIN10-CLI01  
- Verified dynamic IP assignment on the client machine  

---

### 📸 Screenshots

- **DHCP Role Installed on DC01**  
  ![DHCP Feature Installed](screenshots/dhcp/dhcp_feature_installed.png)

- **DHCP Scope Created and Activated**  
  ![DHCP Scope Active](screenshots/dhcp/dhcp_scope_active.png)

- **DHCP Reservation for WIN10-CLI01**  
  ![DHCP Reservation](screenshots/dhcp/dhcp_reservation_win10.png)

- **WIN10-CLI01 Receiving IP Address via DHCP (ipconfig /all)**  
  ![WIN10 DHCP Lease](screenshots/dhcp/win10_dhcp_lease_ipconfig_all.png)

---

### **7. File Server (SRV02)**
- Shared folders  
- NTFS vs share permissions  
- Access-based enumeration  
- Mapped drives via GPO  

Screenshots → `/screenshots/srv02/`

---

### **8. PowerShell Automation Scripts**
Located in `/scripts/powershell/`

Includes:
- Bulk user creation  
- Exporting locked-out accounts  
- Password reset automations  
- AD reporting scripts  

---

## 🧠 Summary
This homelab demonstrates my hands-on ability to deploy and manage a complete Active Directory environment. It showcases my skills in:

- Identity & Access  
- Windows Server  
- Networking  
- Group Policy  
- File Server management  
- Troubleshooting  
- PowerShell automation  

This portfolio is actively updated as I progress in my System Administrator journey.
