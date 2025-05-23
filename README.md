# 🖥️ Active Directory Lab Project

This project demonstrates the setup of a **Windows Server 2022 Active Directory Domain Services (AD DS)** lab using **Oracle VirtualBox**. The lab includes a Domain Controller with a custom Organizational Unit (OU) and a user account
---

## 📌 Project Goals

- Build a free, local Active Directory lab
- Understand and configure AD DS roles
- Create and manage Organizational Units and users
- Join a Windows 10 client to the domain (optional)

---

## 🛠️ Tools & Technologies

| Tool              | Description                        |
|-------------------|------------------------------------|
| Oracle VirtualBox | Free virtualization software       |
| Windows Server 2022 (Eval) | Domain Controller OS     |
| Windows 10 (Optional) | Domain-joined client OS        |

---

## 📦 Prerequisites

- At least **8 GB RAM**
- Oracle VirtualBox installed
- Downloaded ISOs:
  - [Windows Server 2022 Evaluation](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022)
  - [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10) *(optional)*

---

## 🏗️ Lab Setup Overview

### 1. **Create VM in VirtualBox**
- Name: `DC01`
- OS: Windows Server 2022
- RAM: 4–6 GB
- Storage: 50+ GB
- Network: **Host-Only Adapter**

### 2. **Install Windows Server 2022**
- Select: *Standard Edition (Desktop Experience)*
- Complete the installation and login as `Administrator`.

### 3. **Set Static IP**
Example config for `DC01`:
- IP: `192.168.56.10`
- Subnet: `255.255.255.0`
- Gateway: `192.168.56.1`
- DNS: `127.0.0.1`

### 4. **Rename the Server**
```powershell

Rename-Computer -NewName "DC01" -Restart
📁 Organizational Unit & User Created
After domain setup, I manually created:

➤ Organizational Unit
Name: TestLab

➤ User
Name: Test User

Username: tuser

OU Location: OU=IT,DC=lab,DC=local

Password: Password123!


Options:

User must change password at next login: ✅

Account enabled: ✅

📚 What I Learned
Installing and configuring AD DS

Setting static IPs and DNS

Using Server Manager and PowerShell for domain setup

Managing users and OUs in Active Directory

Joining clients to a domain

Understanding domain controller roles

🔐 Group Policy Configuration
This configuration enforces strong password policies using Group Policy:

Minimum Password Length: 6 characters

Password Complexity: Enabled (requires special characters, uppercase, lowercase, and numbers)

Maximum Password Age: 20 days (users must reset their password every 20 days)

To apply these settings via Group Policy:

Open the Group Policy Management Console (GPMC).

Navigate to:
Computer Configuration > Windows Settings > Security Settings > Account Policies > Password Policy

Set the following:

Minimum password length: 6

Password must meet complexity requirements: Enabled

Maximum password age: 20 days

### 🔧 DNS Configuration

- Verified DNS role installed during AD DS promotion
- Confirmed Forward Lookup Zone `lab.local` with A records and SRV records
- Created Reverse Lookup Zone `192.168.56.0`
- Added PTR record for `dc01.lab.local` (192.168.56.10)
- Verified name resolution with `nslookup` and PowerShell


🏁 Next Steps (Future Additions)

File shares and access control

Logon scripts

Delegating control to junior admins
