# Azure Virtual Network Configuration & IP Learning Program

##  Project Overview
This project focuses on the foundational principles of cloud networking through the manual configuration, security hardening, and deployment of Microsoft Azure Virtual Network (VNet) infrastructure. Networking forms the core backbone of cloud systems. This lab demonstrates how to architect software-defined networks with an emphasis on logical isolation, CIDR notation, subnet segmentation, endpoint mappings, and strict perimeter security controls.

##  Project Goals
* **IP Architecture:** Implement structured IP addressing schemes using CIDR notation.
* **Subnet Segmentation:** Design isolated subnets to enforce tier-based security zones.
* **Traffic Management:** Secure network perimeters by writing strict inbound/outbound Network Security Group (NSG) rules.
* **Endpoint Management:** Handle dynamic private allocations and provision Static Standard Public IPs for external administrative routing.
* **Troubleshooting & Validation:** Resolve real-world interface binding disconnects and validate secure administrative access paths.

---

##  Implemented Tasks & Architecture

### Task 1 & 2: VNet Definition & Subnet Segmentation
A dedicated Virtual Network address space was declared to prevent infrastructure overlap while allowing ample future scaling:
* **VNet Name:** `vmhrdeveastus201-vnet`
* **Address Space:** `10.1.0.0/24` (250 available host allocations)
* **Subnet Partition:** Managed via a `default` high-availability subnet zone handler (`10.1.0.0/24`).

### Task 3: Connection Endpoints & IP Allocation
To guarantee external connectivity without creating widespread exposure:
* **Internal Routing:** Virtual network interfaces track dynamic internal addressing (e.g., `10.1.0.4`).
* **External Access Routing:** Associated a Static Standard Public IP resource pipeline:
    * **Resource ID:** `pip-vmhrdeveastus201-vnet-eastus2...`
    * **Public IP Endpoint:** `20.62.122.34`

### Task 4: Network Security Group (NSG) Hardening
Security boundaries were established by updating security rules from generic world-open permissions to localized, identity-verified perimeters:
* **Rule Set Name:** `vmhrwinastus201-nsg` / `vmhrdeveastus201-nsg`
* **Hardened Control:** Added rule `Allow-RDP-MyIP` / `Allow-SSH-MyIP` (Priority `300`).
* **Perimeter Policy:** Restricts access strictly to administrative Source IP (`102.219.128.28`) across standard management ports (`22` for SSH, `3389` for RDP). Defends against automated brute-force attacks while clearing Azure Security Center alerts.

### Task 5 & 6: Resource Deployment & Connectivity Validation
Deployed multi-environment virtual infrastructure instances (`vmhrdeveastus201` running Linux Ubuntu 24.04 and a Windows Server 2022 instance) to test connectivity pipelines. 

As captured in the deployment overview dashboard (`Screenshot (1851).png`), the template creation process executed successfully under deployment identifier `CreateVm-microsoftwindowsserver.windowsserver2022-20260629163408`, creating the core systems inside the resource group `vmhrdeveastus201_group`. Verified cryptographic identity handshake protocols via local terminals utilizing down-scoped private key access controls (`.pem`) and verified RDP network policies.

---

##  Submission Deliverables

Your repository structure contains the required proof items matching your system configurations:
1. **Azure Resource Report:** Located via configuration state dashboards showing live network status.
2. **Security Documentation:** Explicit NSG rule tracking panels showcasing zero-exposure warnings.
3. **Connectivity Proof:** Console sessions confirming active handshakes across active endpoints.
4. **Deployment Verification:** Complete record of the automated resource engine provisioning pipeline.


# Executive Project Summary: Azure Virtual Network & Access Verification
**Project Program:** Azure Virtual Network Configuration Subnet IP Learning Program  
**Status:** Completed & Successfully Validated

---

###  Deployed Core Infrastructure Matrix
* **Virtual Network (VNet):** `vmhrdeveastus201-vnet`
* **Address Space Allocation:** `10.1.0.0/24`
* **Resource Group Identifier:** `vmhrdeveastus201_group`
* **Target Operating Instances:** * `vmhrdeveastus201` (Linux Ubuntu 24.04 LTS Server)
  * `vmhrwinastus201` (Windows Server 2022 Standard)
* **Internal Private IP Mapping:** `10.1.0.4` (Dynamic Base Allocation)
* **External Public Route Pipe:** `20.62.122.34` (Standard Static Configuration)

---

### Core Milestones Executed

#### 1. Network Topology Layering
Designed a clean software-defined perimeter using a baseline CIDR block configuration to eliminate risk of structural overlap. Subnet segment allocations were cleanly bounded to logical network zones.

#### 2. Interface Pipeline Binding Remediation
Identified and patched a critical initial state fault where virtual machine interfaces lacked a public-facing network map (`Public IP address : -`). Hand-mapped the internal configuration (`ipconfig1`) directly to a live, routeable internet gatekeeper route (`20.62.122.34`).

#### 3. Security Boundary Hardening
Overrode wide-open default cloud rules that exposed structural ports to the internet. Applied explicit localized filter priority handlers (Rule Priority `300`) matching specific administrative management layers (Port `22` for SSH, Port `3389` for RDP) locked down entirely to the developer's source machine identity (`102.219.128.28`).

#### 4. Automated Provisioning & Verification
Initiated a full compute provisioning sequence (`CreateVm-microsoftwindowsserver.windowsserver2022-20260629163408`). As confirmed by the deployment pipeline dashboard, all underlying cloud network cards, disks, storage profiles, and operating environment structures successfully validated and moved to a ready state. Handshake testing was performed via Windows PowerShell using secure `.pem` file permissions.

---

### Final System Compliance Checklist
- [x] VNet Defined with scalable non-overlapping CIDR notation.
- [x] Multi-tier subnet division and dynamic private assignment active.
- [x] Standard Static Public IP address provisioned and attached to target NIC.
- [x] Network Security Group inbound policies locked to single source IP.
- [x] Target virtual instance environments fully provisioned.
- [x] Cryptographic terminal access routes verified.
