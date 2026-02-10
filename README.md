# Enterprise-AD-Linux-Windows-Integration
Identity Management | Kerberos Authentication | Cross-Platform Storage | Security Auditing

## Project Overview
This project involved architecting a hybrid enterprise environment from the ground up. I provisioned a Windows Server 2022 Domain Controller and integrated a Rocky Linux 10 workstation into the Active Directory forest. The lab demonstrates real-world competencies in Identity & Access Management (IAM), DNS architecture, GPO enforcement, and secure cross-platform storage integration using Kerberos v5.

## Technical Stack
* Directory Services: Microsoft Active Directory (Windows Server 2022)
* Linux Distribution: Rocky Linux 10 (RHEL-based)
* Authentication: Kerberos v5, NTLMv2, SSSD, Realmd
* File Protocol: SMB/CIFS (version 3.1.1)
* Auditing: Windows Object Acces Auditing (Event ID 4663)

## Key Implementation Phases

### Phase 1: Infrastructure Provisioning 
Hypervisor: Oracle VirtualBox

* DC01 (Windows Server 2022): 4GB RAM, 2vCPUs, 50GB VHD.

* RockySrv01 (Rocky Linux 10.1): 2GB RAM, 1vCPU, 20GB VDI.

* CL01 (Windows 10 Client): Domain-joined workstation for validation.

🛠️ Key Troubleshooting: The "Ghost Floppy" Error
* Issue: Windows Installer failed with a "Missing Media Driver" error.

* Root Cause Analysis: Installer lost the path to the virtual SATA optical drive due to legacy BIOS polling.

* Resolution: Disabled the virtual Floppy Drive in VirtualBox Motherboard settings; forced the installer to prioritize the SATA ISO mapping.
