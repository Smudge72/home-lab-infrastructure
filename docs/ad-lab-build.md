# 🖥️ Home Lab Build – Active Directory Environment (Hyper-V)

## 📅 Date

March 2026

---

## 🎯 Objective

Build a functional Windows-based enterprise lab environment using Hyper-V, including:

* Domain Controller (DC)
* Client machine
* Active Directory structure
* Domain user authentication
* Group Policy

---

## 🧱 Infrastructure Overview

### Host Machine

* Windows 11
* Hyper-V enabled

### Virtual Machines

* **DC01** – Windows Server 2022 (Domain Controller)
* **CLIENT01** – Windows 11 Pro (Domain-joined client)

### Network

* Internal virtual switch (`Lab-Switch`)
* Isolated network (no internet)

---

## 🌐 Network Configuration

### DC01

* IP: `192.168.100.10`
* Subnet: `255.255.255.0`
* DNS: `127.0.0.1`

### CLIENT01

* IP: `192.168.100.20`
* Subnet: `255.255.255.0`
* DNS: `192.168.100.10`

---

## ⚙️ Build Steps

### 1. Hyper-V Setup

* Enabled Hyper-V and virtualisation
* Created **Internal Virtual Switch** (`Lab-Switch`)

---

### 2. Domain Controller Setup

* Installed Windows Server 2022 (Desktop Experience)
* Renamed server to `DC01`
* Configured static IP
* Installed **Active Directory Domain Services (AD DS)**
* Promoted server to Domain Controller
* Created domain: `lab.local`

---

### 3. Active Directory Configuration

Created Organisational Units:

* Servers
* Workstations
* Users
* Groups

Created user:

* Username: `euan`
* Added to domain

---

### 4. Client Machine Setup

* Installed Windows 11 Pro
* Enabled TPM in Hyper-V
* Configured static IP + DNS
* Joined domain: `lab.local`

---

### 5. Domain Join

* Successfully joined CLIENT01 to domain
* Logged in using:

  * `LAB\euan`

---

## 🔧 Troubleshooting (Key Learning)

### ❌ Issue: No connectivity between VMs

* Symptoms:

  * APIPA address (169.x.x.x)
  * Ping failure
  * No ARP entries

### ✅ Resolution:

* Recreated virtual switch (`Lab-Switch`)
* Removed and re-added VM network adapters
* Ensured both VMs connected to same switch

---

### ❌ Issue: Windows 11 setup required internet

### ✅ Resolution:

* Disconnected network adapter during setup

---

### ❌ Issue: RDP permission error on login

### ✅ Resolution:

* Disabled Enhanced Session Mode in Hyper-V

---

## 🔐 Group Policy

Created GPO:

* **Disable Control Panel**
* Applied to IT OU

---

## 🧠 Key Skills Demonstrated

* Hyper-V virtualisation
* Windows Server deployment
* Active Directory setup
* DNS configuration
* Domain join process
* Network troubleshooting (Layer 2 / ARP / switching)
* Group Policy management

---

## 🚀 Next Steps

* File shares & permissions
* Additional users & groups
* Group Policy expansion
* PowerShell automation
* Simulated helpdesk scenarios

---

## 💡 Summary

Successfully built a functional Active Directory lab from scratch, including troubleshooting real-world networking issues and implementing enterprise-level configurations.

