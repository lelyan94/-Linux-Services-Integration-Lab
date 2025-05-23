# 🐧 Linux Services Integration Lab

This lab focuses on migrating core services — web hosting, FTP, and file sharing — from Windows Server to a Linux server integrated with Active Directory. The Linux server is joined to the Windows domain and configured to authenticate domain users, while hosting websites, FTP, and Samba shares with proper permissions and encryption. Internal and remote access were tested using multiple domain users.

![Image](https://github.com/user-attachments/assets/3705e2aa-1a7f-4e65-9ef1-c3e705bd8d73)

---


## 🛠️ Tools & Technologies

- Ubuntu Linux Server
- Windows Server (AD, DNS)
- Windows 10 Internal Client
- Domain Users: Erica, Trish, Ernie
- Services: Apache2, vsftpd with SSL, Samba, Kerberos/SSSD
- Tools: RSAT, PuTTY, MySQL

---

## 📁 Summary of What Was Done

- ✅ Joined Linux server to the Windows domain using Kerberos
- ✅ Migrated and configured:
  - Apache web services with virtual hosts
  - FTP server with SSL and permission-based access
  - SMB shares with custom access levels
- ✅ Verified domain user access to all services (web, shares, FTP)
- ✅ Set permissions using domain and local users
- ✅ Enabled remote Linux access via SSH and Windows RSAT tools
- ✅ Tested access for domain users from internal client

## 🧩 Project Overview

| Component        | Description                                                            |
|------------------|------------------------------------------------------------------------|
| Windows Client   | Used for RSAT management and domain login verification                  |
| Linux Server     | Hosts Apache websites, FTP service, SMB shares; joined to Windows domain |
| Domain Users     | Access tested for permissions and restrictions                          |

---

## 🖥️ Internal Client (Administrator Access)

### 🔹 RSAT – Server Manager

Added both the Domain Controller and VPN Server to Server Manager from the Internal Client. Performance monitoring is enabled.


![Image](https://github.com/user-attachments/assets/ddee36c1-b61f-44d6-b4f1-f078443e6915)

---

### 🔹 Active Directory Users and Computers

Confirmed the Linux server I added to Active Directory as a computer object.

![Image](https://github.com/user-attachments/assets/aa477bd2-20c3-4792-acf7-9f094fc0a6b0)

---

## 🔐 Domain-Based SSH Access

### 🔹 SSH to Linux as Domain User

Logged in via SSH as `erica@domain`, then switched to root using `su -l`.  
The `id` command confirms domain-based identity.

![Image](https://github.com/user-attachments/assets/de50b85d-ea26-4cf3-8742-136132c53eb7)

![Image](https://github.com/user-attachments/assets/17e512e3-9748-4c5e-a8cb-22dc16011069)

---

## 🌐 Apache Web Server Configuration

### 🔹 Virtual Host Setup & Bindings

Two websites configured using Apache:
- **linwww** (open to all, with MySQL-backed form)
- **linstaff** (restricted to specific users)

Screenshots show:
- Apache site folders
- Virtual host files
- Bindings to domain-based hostnames

![Image](https://github.com/user-attachments/assets/b7827dee-fd30-4d65-8925-82b4eb2f3704)

---

## 🔒 FTP Server with SSL

### 🔹 Configuration with Certificate

Configured `vsftpd` with SSL support.  
FTP access limited to `Simon` and `Trish`, using domain or local accounts.

![Image](https://github.com/user-attachments/assets/5e6c5d2c-0cc1-410f-b204-9a7cb023690a)

![Image](https://github.com/user-attachments/assets/35bd8e9e-4f70-4022-93f9-64f11558a85b)

---

## 📂 SMB Shares Configuration

### 🔹 Share Setup and Access

Two shares created:
- `honeytoo` – read-only for everyone
- `stinger` – read/write for Erica and Ernie only

![Image](https://github.com/user-attachments/assets/dad296c4-6a07-49a8-83aa-e9c6c2e50437)

---

### 🔹 testparm Output

Confirms that the Samba config syntax is correct and all shares are readable.

![Image](https://github.com/user-attachments/assets/4edf2c74-a979-45a1-a87c-20561b258ea4)

---


### 🔹 realm list Output

Displays current domain join status and SSSD config from Linux.

![Image](https://github.com/user-attachments/assets/a7243fd0-0e2d-446a-aade-55782494468d)

---

### 🔹 File Permissions (Apache & FTP)

Linux file ownership and permission settings for Apache and FTP directories are shown.

![Image](https://github.com/user-attachments/assets/8a2668e5-74e1-4440-be1b-d149d96ad5fd)

![Image](https://github.com/user-attachments/assets/8f5418e1-1d62-4e4a-8d0b-0dba674eca5c)

---

## 👩‍💻 Internal User Testing (Trish)

### 🔹 whoami Output

Confirms Trish is logged in with her domain credentials.

![Image](https://github.com/user-attachments/assets/f1062687-ec8a-4126-8ef1-8ab573e250b0)

---

### 🔹 Accessing `linwww`

Login prompt appears for form submission.  
Trish is able to submit and view form input data.

![Image](https://github.com/user-attachments/assets/9a8258f5-ae73-4a61-b4bd-7c6c96c6ae66)
![Image](https://github.com/user-attachments/assets/0b5f2da5-01bd-4d51-8a1f-dd4b5dfe6c1e)

---

### 🔹 Accessing `linstaff`

Successfully logs in and accesses restricted site.

![Image](https://github.com/user-attachments/assets/0495bb5f-68f4-443d-a73c-77bfbcb1b154)

![Image](https://github.com/user-attachments/assets/3090c9cd-a3fd-41b6-b419-eb0f499e31c6)

---

### 🔹 FTP Write Access

Trish can log in to the FTP server and upload files.

![Image](https://github.com/user-attachments/assets/cb5a4df6-850f-49fc-9c92-f206a5e82e80)
![Image](https://github.com/user-attachments/assets/5bfbebdc-91c6-41e8-8b6d-38711841d082)

---

### 🔹 Access to `honeytoo` (Read-Only)

Can browse and read, but not write.

![Image](https://github.com/user-attachments/assets/ad773cd4-5dcd-4b57-b619-60e53645ff80)

---

## 👨‍💻 Internal User Testing (Ernie)

### 🔹 Accessing `linstaff` (Denied)

Attempt to access restricted staff site fails.

![Image](https://github.com/user-attachments/assets/e20a54c1-bf13-4267-b7e7-4ef8ace8d9a8)

![Image](https://github.com/user-attachments/assets/49448366-5aa8-41a7-8286-cfe4bdd3e41a)

---

### 🔹 Accessing `linwww` (Allowed)

Public website opens without issue.

![Image](https://github.com/user-attachments/assets/2cc964d4-2bfe-4c95-adb2-021a436e2f46)

![Image](https://github.com/user-attachments/assets/e0296c7d-deb3-43d9-852d-9e01e9f070ed)

---

### 🔹 Accessing `stinger` (Full Access)

Has read/write permissions on stinger share.

![Image](https://github.com/user-attachments/assets/2950fb5c-9e6d-4733-945f-b269ed5cb4a8)

---

### 🔹 SSH Access via PuTTY

Successfully logs into Linux with domain credentials using PuTTY.

![Image](https://github.com/user-attachments/assets/af694fa4-24ba-47cc-9466-1a60f5b0846a)

---
## 🧾 Final Summary

This lab successfully demonstrates how to migrate and host key services — web, FTP, and file sharing — on a Linux server fully integrated with a Windows domain environment. Each service was configured to respect domain-level authentication and access control, providing a realistic enterprise-ready setup.

Key outcomes:
- ✅ Full domain integration of the Linux server with Kerberos authentication
- ✅ Seamless Apache virtual host deployment and secure form handling
- ✅ SSL-secured FTP server with user-specific permissions
- ✅ Domain-aware Samba shares with tiered access levels
- ✅ Remote access and administrative management using RSAT and SSH
- ✅ User-based testing validated all permission levels and access boundaries

This lab provides a comprehensive look at hybrid infrastructure design, where Linux and Windows services coexist securely and efficiently within the same network.






