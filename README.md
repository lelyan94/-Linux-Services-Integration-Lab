# 🐧 Linux Services Integration Lab

This lab focuses on integrating a Linux server into a Windows domain environment and deploying key services such as Apache, FTP, and SMB file sharing. It includes domain authentication, remote management, service configuration, and access control testing across multiple user roles.

![Image](https://github.com/user-attachments/assets/3705e2aa-1a7f-4e65-9ef1-c3e705bd8d73)

---

## 🛠️ Tools Used

- VMware Workstation
- Ubuntu Linux Server
- Windows Server (with RSAT tools)
- Windows 10 Clients
- Domain Users: `Erica`, `Trish`, `Ernie`

---

## 🧩 Project Overview

| Component        | Description                                                            |
|------------------|------------------------------------------------------------------------|
| Windows Client   | Used for RSAT management and domain login verification                  |
| Linux Server     | Hosts Apache websites, FTP service, SMB shares; joined to Windows domain |
| Domain Users     | Access tested for permissions and restrictions                          |

---

## 🖥️ Internal Client (Domain Administrator)

### 🔹 Server Manager

Opened via RSAT tools to verify both Windows and Linux servers are listed and managed.

![Image](https://github.com/user-attachments/assets/ddee36c1-b61f-44d6-b4f1-f078443e6915)

---

### 🔹 Active Directory Users and Computers

Shows that the Linux machine has been successfully added to the domain.

![Image](https://github.com/user-attachments/assets/aa477bd2-20c3-4792-acf7-9f094fc0a6b0)

---

### 🔹 SSH to Linux Server as Domain User

Logged into Linux from a Windows client using SSH as `erica@domain`, then switched to root. Below is the output of the `id` command confirming domain integration.

![Image](https://github.com/user-attachments/assets/de50b85d-ea26-4cf3-8742-136132c53eb7)

![Image](https://github.com/user-attachments/assets/17e512e3-9748-4c5e-a8cb-22dc16011069)

---

## 🔧 Linux Server – Service Configuration

### 🔹 Apache Configuration

This section shows:
- Apache virtual host directory structure
- Website bindings 
- Virtual host configurations with domain integration

![Image](https://github.com/user-attachments/assets/b7827dee-fd30-4d65-8925-82b4eb2f3704)

---

### 🔹 FTP Server with TLS

Displays:
- FTP site configuration
- Certificate used for secure FTP access

![Image](https://github.com/user-attachments/assets/5e6c5d2c-0cc1-410f-b204-9a7cb023690a)

![Image](https://github.com/user-attachments/assets/35bd8e9e-4f70-4022-93f9-64f11558a85b)

---

### 🔹 SMB File Shares

Screenshots of:
- Shares created (e.g., honeytoo, stinger)
- Share-level permissions

![Image](https://github.com/user-attachments/assets/dad296c4-6a07-49a8-83aa-e9c6c2e50437)

---

### 🔹 `testparm` Output

Displays the effective Samba configuration and validates the syntax.

![Image](https://github.com/user-attachments/assets/4edf2c74-a979-45a1-a87c-20561b258ea4)

---

### 🔹 `realm list` Output

Verifies Linux machine is enrolled in the domain and lists SSSD configuration.

![Image](https://github.com/user-attachments/assets/a7243fd0-0e2d-446a-aade-55782494468d)

---

### 🔹 File Permissions for Apache & FTP Content

Shows Linux folder-level permissions for hosted content directories.

![Image](https://github.com/user-attachments/assets/8a2668e5-74e1-4440-be1b-d149d96ad5fd)

![Image](https://github.com/user-attachments/assets/8f5418e1-1d62-4e4a-8d0b-0dba674eca5c)

---

## 👩‍💻 Internal Client: User Trish

### 🔹 whoami

Confirms domain identity of logged-in user.

![Image](https://github.com/user-attachments/assets/f1062687-ec8a-4126-8ef1-8ab573e250b0)

---

### 🔹 Accessing Linwww Website

Browser prompt and successful login to `linwww` with database interaction capabilities (e.g., adding a user).

![Image](https://github.com/user-attachments/assets/9a8258f5-ae73-4a61-b4bd-7c6c96c6ae66)
![Image](https://github.com/user-attachments/assets/0b5f2da5-01bd-4d51-8a1f-dd4b5dfe6c1e)

---

### 🔹 Accessing Linstaff

User `Trish` accesses restricted `linstaff` site with appropriate role.

![Image](https://github.com/user-attachments/assets/0495bb5f-68f4-443d-a73c-77bfbcb1b154)

![Image](https://github.com/user-attachments/assets/3090c9cd-a3fd-41b6-b419-eb0f499e31c6)

---

### 🔹 FTP Upload Access

Trish is able to log in and write to the FTP directory.

![Image](https://github.com/user-attachments/assets/cb5a4df6-850f-49fc-9c92-f206a5e82e80)
![Image](https://github.com/user-attachments/assets/5bfbebdc-91c6-41e8-8b6d-38711841d082)

---

### 🔹 Access to honeytoo Share (Read-Only)

Can browse and read from the share but cannot modify or write.

![Image](https://github.com/user-attachments/assets/ad773cd4-5dcd-4b57-b619-60e53645ff80)

---

## 👨‍💻 Internal Client: User Ernie

### 🔹 Linstaff Website (Access Denied)

Ernie is denied access to the staff-only site, verifying role-based restriction.

![Image](https://github.com/user-attachments/assets/e20a54c1-bf13-4267-b7e7-4ef8ace8d9a8)

![Image](https://github.com/user-attachments/assets/49448366-5aa8-41a7-8286-cfe4bdd3e41a)

---

### 🔹 Linwww Website (Access Allowed)

Ernie is allowed to access the public Linwww website.

![Image](https://github.com/user-attachments/assets/2cc964d4-2bfe-4c95-adb2-021a436e2f46)

![Image](https://github.com/user-attachments/assets/e0296c7d-deb3-43d9-852d-9e01e9f070ed)

---

### 🔹 Stinger Share (Read/Write)

Ernie has full access to the stinger share, including write capability.

![Image](https://github.com/user-attachments/assets/2950fb5c-9e6d-4733-945f-b269ed5cb4a8)

---

### 🔹 SSH to Linux via PuTTY

Logged in using domain credentials, proving Linux accepts domain-based SSH logins.

![Image](https://github.com/user-attachments/assets/af694fa4-24ba-47cc-9466-1a60f5b0846a)

---






