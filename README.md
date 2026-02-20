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

* Root Cause Analysis: Installer lost the path to the virtual SATA optical drive

* Resolution: Removed legacy Floppy drive from BIOS boot device order
________________________________________
🔐 Phase 2: Domain Architecture & DNS
Forest Name: lab.local | Functional Level: Windows Server 2016
•	DNS Strategy: Implemented a split-brain DNS approach. Removed public DNS from NIC properties post-promotion and configured DNS Forwarders to maintain internal SRV record integrity while allowing external resolution.
•	Reverse Lookup: Configured an AD-Integrated Primary Zone for the 10.0.2.0/24 subnet. Resolved initial nslookup failures by forcing PTR record registration via ipconfig /registerdns.
________________________________________
👥 Phase 3: Identity & Access Management (IAM)
•	RBAC Model: Established a standardized OU hierarchy (LAB_Objects > Users, Groups).
•	Security Groups: Created the Accounting_Team group to demonstrate Role-Based Access Control.
•	Linux Integration: Successfully joined rockysrv01 to the domain using realmd and sssd.
o	Authorization: Mapped Windows "Domain Admins" to the Linux sudoers file, allowing seamless administrative transitions across OS boundaries.
________________________________________
📂 Phase 4: Secure Interoperability (Storage)
Goal: Mount a Windows SMB share on Rocky Linux using Kerberos (No plain-text passwords).
•	Security Hardening: Enforced a pre-authentication Security Banner via GPO to all domain-joined assets.
•	The Kerberos Challenge: Resolved Error -126 (Required key not available) by manually configuring the Linux Kernel Keyring.
•	Implementation: 1. Initialized Kerberos tickets via kinit. 2. Configured cifs.spnego upcalls in /etc/request-key.d/. 3. Mounted the Company_Share using sec=krb5.
________________________________________
🛡️ Phase 5: Governance & Security Auditing
Audit Trail: Verified the "Paper Trail" for all cross-platform file actions.
•	Configuration: Enabled Global Audit Policies via auditpol for "Object Access."
•	SACLs: Applied Advanced Auditing entries to the filesystem for the Everyone principal.
•	Validation: Captured Event ID 4663 in the Windows Security Log, confirming that the Linux user (tuser) successfully created and modified files on the Windows share.
________________________________________
🚀 Skills Demonstrated
•	Windows Server: AD DS, DNS, GPO, File Server Resource Manager (FSRM).
•	Linux Admin: RHEL-based system hardening, SSHD configuration, SSSD/Realmd.
•	Networking: Static IPv4 addressing, Subnetting, DNS SRV/PTR record management.
•	Security: Kerberos v5, NTLMv2, RBAC, System Auditing (SACLs).
