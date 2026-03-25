# Build Log

## Phase 1 – Planning
- Defined VLAN structure
- Designed network topology
- Selected hardware (CWWK N97 firewall appliance)

## Phase 2 – Firewall Deployment (In Progress)
- Waiting for hardware delivery
- Prepared OPNsense installation media
- Planned interface mapping

- PC Rebuild & Hardware Upgrade (AM4 Platform)
Overview

This project documents the full dismantling, upgrade, and rebuild of a desktop PC using a new motherboard, CPU, and air cooler. The goal was to validate hardware functionality by achieving a successful POST and BIOS access.

Objectives
Replace motherboard and CPU
Remove AIO liquid cooler and install air cooler
Rebuild system with correct wiring
Troubleshoot hardware issues
Achieve successful POST (Power-On Self-Test)
Hardware Used
Component	Model
Motherboard	MSI B550M PRO-VDH
CPU	AMD Ryzen (AM4)
Cooler	Arctic Freezer (Air Cooler)
GPU	NVIDIA GeForce RTX (ASUS)
RAM	DDR4 (Dual Channel)
PSU	ATX Power Supply
Storage	SATA SSD
Build Process
1. System Dismantling
Actions:
Powered down and unplugged system
Removed GPU
Disconnected all cables
Removed AIO cooler (radiator + pump)
Removed motherboard and CPU
Key Challenge:

AIO radiator would not detach initially.

Root Cause:

Hidden screws under top case panel

Fix:

Removed top panel
Accessed and removed radiator screws
2. New Hardware Assembly (Outside Case)
CPU Installation
[CPU Socket]
   ▲ Align triangle
   ▼ Lock arm
Installed CPU using alignment markers
No force applied
RAM Installation
Slots: [1] [2] [3] [4]
        ❌  ✅  ❌  ✅

Use: A2 + B2
Installed in dual-channel configuration
Ensured full seating (click on both sides)
Cooler Installation
[Fan] → → → [Heatsink] → → → Rear Exhaust
Removed AMD plastic brackets
Kept stock backplate
Mounted cooler using cross-tightening pattern
Connected to CPU_FAN header
3. Motherboard Installation
Installed motherboard into case
Aligned with standoffs
Secured with screws
4. Wiring & Connections
Power Connections
CPU Power (EPS)
Top-left of motherboard
[ 4 + 4 PIN ]
Initially missed → identified as critical issue
Installed correctly
24-Pin Motherboard Power
Right side of motherboard
[ 24 PIN ]
Fully seated until click
CPU Cooling
CPU fan connected to:
CPU_FAN header
GPU Installation
[PCIe Slot]
     ↓
 [ GPU ]
     ↓
 [PCIe Power 6+2]
Steps:
Installed GPU into top PCIe slot
Secured with screws
Connected PCIe power cable
Issue:

Mistook USB 3.0 header for GPU power

Fix:

Identified correct cable (PCIe labelled)
Front Panel (Power Button)
JFP1 Header Layout:

[ PWR SW ] → Top row (pins 3 & 4)
Connected POWER SW
Orientation not required
Storage (Deferred)
Identified:
SATA Data → motherboard
SATA Power → PSU
Skipped for initial POST
Troubleshooting Log
Issue	Cause	Resolution
Radiator stuck	Hidden screws	Removed top panel
No CPU power	EPS cable missing	Installed 4+4 CPU cable
GPU no display risk	No PCIe power	Connected correct cable
Cable confusion	Multiple unused PSU cables	Focused on required only
Front panel uncertainty	Pin layout unclear	Used JFP1 + POWER SW
First Boot
Result:
POST Successful

BIOS message:

Press F1 to run setup
Press F2 to load default values
Action Taken:
Selected F2 (Load Defaults)
Outcome
System successfully rebuilt
All critical components installed correctly
POST achieved
BIOS accessible
Command Line / PowerShell

No command-line or PowerShell usage was required.

This project focused on:

Hardware assembly
BIOS-level validation
Physical troubleshooting
System Architecture Diagram
        +----------------------+
        |        CPU           |
        +----------+-----------+
                   |
             +-----v-----+
             |  Cooler   |
             +-----------+
                   |
+--------+   +-----v-----+   +--------+
|  RAM   |---| Motherboard|---|  GPU   |
+--------+   +-----+-----+   +--------+
                   |
         +---------v----------+
         |   Power Supply     |
         +---------+----------+
                   |
             +-----v-----+
             |   SSD     |
             +-----------+
Key Learnings
Always verify CPU power (EPS) early
AIO coolers may have hidden mounting points
Not all PSU cables are required
GPU requires dedicated PCIe power
First boot does not require storage
Build outside case for easier installation
Next Steps
BIOS configuration (XMP / DOCP)
Install Windows OS
Install drivers
Integrate into home lab environment
Reflection

This project demonstrates:

Hardware troubleshooting under uncertainty
Logical step-by-step validation
Ability to diagnose and resolve build issues
Practical system integration skills
