# 🖥️ Active Directory Home Lab (Hyper-V)

## 📌 Overview

Designed and built a fully functional on-premises-style Active Directory environment using Hyper-V to simulate real enterprise infrastructure.

This lab demonstrates core system administration skills including domain services, networking, security, and troubleshooting.

---

## 🧱 Architecture

* **DC01** – Windows Server 2022 (Domain Controller, DNS)
* **CLIENT01** – Windows 11 Pro (Domain-joined workstation)
* **Network** – Internal Hyper-V switch (192.168.100.0/24)

---

## ⚙️ Key Features

* Active Directory Domain Services (AD DS)
* Organisational Unit (OU) design (Users, Groups, Workstations)
* Domain user authentication
* Security group-based access control (IT-Admins)
* Group Policy (GPO) for system restrictions and firewall rules
* File share with NTFS + share permissions
* Delegated local admin rights via AD groups

---

## 🔧 Troubleshooting & Key Challenges

### 🔹 VM Connectivity Failure

* Issue: No communication between VMs (APIPA, ARP failure)
* Root Cause: Broken Hyper-V switch / NIC binding
* Resolution: Rebuilt virtual switch and reattached network adapters

---

### 🔹 Asymmetric Network Connectivity

* Issue: Client → DC worked, DC → Client failed
* Root Cause: Windows Firewall blocking inbound ICMP
* Resolution: Enabled firewall rules and implemented via GPO

---

## 📸 Screenshots

*(Add images here)*

* Active Directory structure
* Group Policy configuration
* Hyper-V virtual machines
* File share access

---

## 🧠 Skills Demonstrated

* Hyper-V virtualisation
* Windows Server administration
* Active Directory configuration
* DNS and IP networking
* Firewall and security configuration
* Group Policy management
* Structured troubleshooting methodology

---

## 📁 Documentation

Detailed build notes:
docs/ad-lab-build.md

---

## 🚀 Next Steps

* Automate drive mapping via GPO
* Introduce additional roles (HR, restricted users)
* Implement PowerShell automation
* Simulate helpdesk scenarios

---
