# 🖥️ Active Directory Home Lab (Hyper-V)

## 📌 Overview

Built a fully functional Windows enterprise lab environment using Hyper-V, including a Domain Controller, domain-joined client, and centralised management via Active Directory.

---

## 🧱 Infrastructure

* **DC01** – Windows Server 2022 (Domain Controller)
* **CLIENT01** – Windows 11 Pro (Domain-joined)
* **Internal Network** – 192.168.100.0/24 (Hyper-V virtual switch)

---

## ⚙️ Key Features

* Active Directory Domain Services (AD DS)
* Organisational Unit (OU) structure
* Domain user and group management
* Group Policy implementation
* File share with NTFS permissions
* Centralised admin rights via security groups

---

## 🔧 Troubleshooting Highlights

* Resolved VM connectivity issues (Layer 2 / virtual switch binding)
* Diagnosed APIPA addressing and ARP failures
* Identified and fixed asymmetric connectivity (firewall rules)
* Implemented firewall rules via Group Policy

---

## 📁 Documentation

Full build notes:
docs/ad-lab-build.md

---

## 🚀 Skills Demonstrated

* Virtualisation (Hyper-V)
* Windows Server administration
* Active Directory configuration
* DNS and networking fundamentals
* Group Policy management
* Troubleshooting methodology

---

## 📌 Next Steps

* Automated drive mapping via GPO
* Additional user roles (HR / restricted access)
* PowerShell automation
* Simulated helpdesk scenarios

---
